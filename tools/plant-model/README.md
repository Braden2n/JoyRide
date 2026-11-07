---
id: PLANT-MODEL
status: draft
updated: 2026-11-07
---

# Plant model

A vehicle powertrain plant model for JoyRide. It starts as the sizing model v0 of [STG-1](../../docs/stages/STG-1-ARCHITECTURE.md#1b-system-level-research-about-1-week) task 1b. Later it becomes the plant for co-simulation with compiled embedded code. The model is tool-neutral: Scilab Xcos or OpenModelica builds it, and FMI connects it to the embedded code ([DEC-014](../../docs/decisions/DEC-014-plant-model-in-xcos.md)).

| Field | Value |
| --- | --- |
| Serves | REQ-SYS-001, REQ-SYS-002, REQ-SYS-003, REQ-SYS-004, REQ-SAF-002 in [GOALS.md](../../docs/project/GOALS.md#system-requirements) |
| Owners | DRV and PACK |
| Users | DRV, PACK, VCU, and TMS cycles; STG-3 integration |
| Tools | Scilab Xcos or OpenModelica, per [DEC-014](../../docs/decisions/DEC-014-plant-model-in-xcos.md) |
| Form | Plain folder until real code exists, then its own submodule ([DEC-002](../../docs/decisions/DEC-002-open-source-with-submodules.md), [DEC-010](../../docs/decisions/DEC-010-non-subsystem-work-structure.md)) |
| Design | [FRAMEWORK.md](FRAMEWORK.md), including the [fidelity levels and modes](FRAMEWORK.md#fidelity-and-modes) |

## Sizing outputs

Each output checks against a REQ in [GOALS.md](../../docs/project/GOALS.md#system-requirements). Level 1 produces everything except top speed. Symbols are defined in [FRAMEWORK.md](FRAMEWORK.md#blocks).

| Output | Definition | Mode | Min. level | Checks |
| --- | --- | --- | --- | --- |
| Energy per cycle | $E_{cycle} = \int_0^{t_{cycle}} V_{pack} I_{pack} \, dt$ | Both | 1 | REQ-SYS-002, REQ-SYS-004 |
| Regen recovered | The negative part of $E_{cycle}$ | Both | 1 | REQ-SYS-004 |
| Run time | Time until SOC or cell voltage reaches its floor, repeating the cycle | Both | 1 | REQ-SYS-002 |
| Peak and continuous power | Peak and sustained $P_{pack}$; the continuous window is TBD | Both | 1 | REQ-SYS-004 |
| Peak torque and gear ratio range | $T_m$ and $N$ that meet every cycle without a flag | Backward sweep, forward check | 1 | REQ-SYS-001, REQ-SYS-004 |
| Pack voltage and current | $V_{pack}$ range and peak $I_{pack}$ | Both | 1 | REQ-SAF-002 at full charge |
| Design load | All outputs computed at the REQ-SYS-003 mass | Both | 1 | REQ-SYS-003 |
| Top speed | Steady $v$ at full pedal on level ground | Forward | 2 | REQ-SYS-001 |

## Layout

Planned top-level structure. Create each folder only when its first file exists.

```text
tools/plant-model/
  README.md        this file
  FRAMEWORK.md     tool-neutral plant spec: physics, block contract, FMI boundary
  params/          tool-neutral parameter sets, one per configuration, read by both tools
  cycles/          drive cycles and scenarios (DEC-011)
  xcos/            Scilab Xcos diagrams and scripts
  modelica/        OpenModelica package and scripts
  sim/             runners and co-simulation setup, for either tool
  studies/         sizing studies and their results
```

Exported FMUs are generated and are not committed.
