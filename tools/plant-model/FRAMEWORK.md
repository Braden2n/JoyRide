---
id: PLANT-FRAMEWORK
status: draft
updated: 2026-10-16
---

# Plant model reference framework

The plant is a chain of blocks that share one contract. This file is tool-neutral. Scilab Xcos and OpenModelica both build the blocks, and FMI is the boundary between them and the embedded code ([DEC-014](../../docs/decisions/DEC-014-plant-model-in-xcos.md), proposed). The same blocks run alone for sizing and behind a co-simulation boundary for embedded code. This is a reference, not an implementation. Every parameter value is TBD.

## Architecture

Power flows left to right. Speed and voltage flow back.

```text
Drive cycle -> Driver -> Controller -> Motor and inverter -> Driveline -> Vehicle
                            |               ^   |                             |
                            |          DC bus   DC current                    |
                            v               |   v                             |
                        Power path <------- Battery                           |
                                                                              |
Thermal (optional) <- losses from every block       speed feedback <----------+
```

| Approach | How it works | Use |
| --- | --- | --- |
| Backward-facing | A speed trace sets acceleration; each block computes the torque, power, and current needed. | Fast sizing sweeps |
| Forward-facing | A driver model issues commands; the plant integrates its states forward in time. | Co-simulation, and checking that limits are met |

Build every block forward-facing. A sizing sweep then runs the same blocks with the speed held to the trace.

## Blocks

| Block | Sizing fidelity | Co-simulation fidelity | Owner |
| --- | --- | --- | --- |
| Drive cycle and driver | Speed trace per scenario ([DEC-011](../../docs/decisions/DEC-011-useful-session-definition.md)). Driver is a speed-error controller producing pedal position. | Same, plus brake and scripted fault events | System |
| Vehicle | Longitudinal force balance (below) | Add tire slip and brake force | CHS |
| Driveline | Fixed ratio and efficiency | Add backlash and compliance | DRV |
| Motor and inverter | Torque-speed envelope and an efficiency map or loss model | Averaged dq-axis model, or brushed DC model, with current limits | DRV |
| Battery | Internal-resistance cell model, scaled by series and parallel count | 1 or 2 RC equivalent circuit per cell group, with cell spread | PACK |
| Power path | Lumped wire and fuse resistance | Contactors, precharge, DC-link capacitance, fuse, E-stop | PACK |
| Thermal | Not needed | Lumped thermal mass per component, used for derating | TMS |
| Controller | Ideal: pedal to torque request, clipped to motor and battery limits | Replaced by compiled embedded code | VCU |

Core equations:

| Physics | Relation |
| --- | --- |
| Vehicle | `m_eff * dv/dt = F_wheel - 0.5*rho*CdA*v^2 - Crr*m*g*cos(theta) - m*g*sin(theta)`, with `m_eff = m + J_total / r_wheel^2` |
| Driveline | `w_motor = N * w_wheel`, and `T_wheel = N * eta * T_motor` (eta inverts during regen) |
| Motor, sizing | `T <= T_max(w, V_bus)`, and `P_dc = T * w / eta(T, w)` |
| Motor, dq | `v_d = R*i_d + L_d*di_d/dt - w_e*L_q*i_q`; `v_q = R*i_q + L_q*di_q/dt + w_e*(L_d*i_d + lambda)`; `T = 1.5*p*(lambda*i_q + (L_d - L_q)*i_d*i_q)` |
| Battery | `V_pack = n_s * (OCV(SOC) - I_cell*R0 - V_rc)`, `I_cell = I_pack / n_p`, and `dSOC/dt = -I_cell / Q` |
| Power path | Precharge: `dV_link/dt = (V_pack - V_link) / (R_pre * C_link)`. Fuse trips on `I^2*t`. |
| Thermal | `C_th * dT/dt = P_loss - (T - T_amb) / R_th` |

Sizing outputs: peak and continuous power, peak torque, gear ratio range, energy per cycle, pack voltage and current, and run time. Each output checks against a REQ in [GOALS.md](../../docs/project/GOALS.md#system-requirements). Full-charge pack voltage checks against REQ-SAF-002.

## Block contract

Every block follows one contract, whichever tool builds it. The contract mirrors an FMI component, so any block can later be exported as an FMU or wrapped as C code.

```text
block <Name>
  params                                   fixed values from params/
  state                                    integrated quantities, such as v, SOC, i_d, T
  inputs                                   signals from neighbors or actuators
  outputs                                  signals to neighbors or sensors
  init(params)                -> state
  derivatives(t, state, in)   -> d(state)/dt
  outputs(t, state, in)       -> out
  events(t, state, in)        -> discrete changes, such as contactor open or fuse trip
```

Signals between blocks, in SI units:

| From | To | Signals |
| --- | --- | --- |
| Driver | Controller | Pedal position, brake |
| Controller | Motor and inverter | Torque request, enable |
| Controller | Power path | Contactor and precharge commands |
| Battery | Power path | Pack voltage |
| Power path | Motor and inverter | DC bus voltage |
| Motor and inverter | Power path, Battery | DC current |
| Motor and inverter | Driveline | Shaft torque |
| Driveline | Motor and inverter | Shaft speed |
| Driveline | Vehicle | Wheel torque |
| Vehicle | Driveline, Driver | Wheel speed, vehicle speed |
| Every block | Thermal | Power loss |
| Thermal | Every block | Temperature |

## Tool mapping

Each tool realizes the contract in its own terms. The mapping is the same for every block.

| Contract element | Scilab Xcos | OpenModelica |
| --- | --- | --- |
| params | Block parameters and diagram context, values from `params/` | Model parameters, values from `params/` |
| state | Continuous states of the blocks inside a superblock | Continuous states of the model's equations |
| inputs and outputs | Superblock ports | Connectors and input or output declarations |
| events | Event and zero-crossing blocks | `when` equations and events |
| Physics | Block equations per block | Equations, often acausal, with the Modelica Standard Library |
| Co-simulation export | FMI export of the top-level diagram | FMI export of the model |

Source files live in `xcos/` or `modelica/`. Which tool builds which block is open item 2 in [README.md](README.md).

## Co-simulation boundary

The plant exposes only what real hardware exposes: sensor outputs and actuator inputs.

| Embedded code | Plant gives it | Plant takes from it |
| --- | --- | --- |
| VCU | Pedal, brake, wheel speed, pack and motor status messages | Torque request, drive enable |
| BMS | Cell voltages, pack current, temperatures, contactor feedback | Contactor, precharge, and balancing commands |
| Motor control | Phase currents, DC bus voltage, rotor angle or Hall states | Phase voltage or duty commands |

Messages between nodes follow the DBC once it exists (REQ-SYS-005). Embedded code builds for the host as a shared library, with a hardware abstraction stub replacing drivers. The library exposes a small C interface: `init`, `step(t, sensors) -> actuators`, `terminate`. How the plant calls that library, by direct link or by a wrapper FMU, is open item 4 in [README.md](README.md).

Run loops, tool-neutral:

```text
standalone(params, cycle):
  load the plant from xcos/ or modelica/ with params and cycle
  simulate over the cycle time span with the tool's solver
  report sizing outputs against the REQs in GOALS.md

cosim(params, cycle, controller_lib):
  load the plant with controller_lib wired to its boundary
  controller_lib.init()
  every controller tick (fixed step, the code's task rate):
    sensors   = plant outputs at the boundary
    actuators = controller_lib.step(t, sensors)
    advance plant to the next tick with fixed substeps, actuators held
  log signals; check faults and limits
```

## Build tools

Scilab Xcos and OpenModelica are the candidate tools ([DEC-014](../../docs/decisions/DEC-014-plant-model-in-xcos.md), proposed). Both must export FMI co-simulation units. Version, FMI export and import, and FMU loading on macOS are open item 3 in [README.md](README.md).
