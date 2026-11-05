---
id: RESEARCH-VEHICLE-CONSTANTS
status: draft
updated: 2026-11-04
---

# Vehicle Dynamics Constants

First-pass values for the plant [Vehicle equations](../../tools/plant-model/FRAMEWORK.md#vehicle), and how each was chosen. No JoyRide hardware exists to test, so each value is a best guess from kart literature, swept to bound the error.

## Contents

- [Parameter map](#parameter-map)
- [Process](#process)
- [Air density, gravity, and grade](#air-density-gravity-and-grade)
- [Drag area](#drag-area)
- [Rolling resistance](#rolling-resistance)
- [Mass and rotating mass](#mass-and-rotating-mass)
- [Open parameters](#open-parameters)
- [Sources](#sources)

## Parameter map

Symbols and parameter names match the framework's [Vehicle](../../tools/plant-model/FRAMEWORK.md#vehicle) symbol table.

| Symbol | Parameter | Baseline | Sweep | How it was set | Section |
| --- | --- | --- | --- | --- | --- |
| $\rho$ | `rho` | 1.225 kg/m³ | none | Standard value, accepted by the builder | [Air density, gravity, and grade](#air-density-gravity-and-grade) |
| $g$ | `g` | 9.81 m/s² | none | Standard value, accepted by the builder | [Air density, gravity, and grade](#air-density-gravity-and-grade) |
| $\theta$ | `theta` | 0 rad | none | Builder choice: flat track | [Air density, gravity, and grade](#air-density-gravity-and-grade) |
| $C_dA$ | `CdA` | 0.56 m² (Cd 0.8 × Af 0.70 m²) | Af 0.56, 0.65, 0.70, 0.83 m² at Cd 0.8 | Builder chose Cd 0.8; Af back-calculated from measured kart $C_dA$ | [Drag area](#drag-area) |
| $C_{rr}$ | `Crr` | 0.03 | 0.015, 0.02, 0.03, 0.04, 0.056 | Best guess, accepted by the builder | [Rolling resistance](#rolling-resistance) |
| $m$ | `m` | 246 to 276 kg | same | 136 kg driver (REQ-SYS-003) plus estimated kart mass | [Mass and rotating mass](#mass-and-rotating-mass) |
| $k_m$ | `k_m` | 1.13 | 1.0 to 1.13 | Fitted kart value, until $J_{total}$ is known | [Mass and rotating mass](#mass-and-rotating-mass) |

- Sweeps run in backward mode through the framework's `sweep()` loop. The chosen set is confirmed in forward mode ([Modeling modes](../../tools/plant-model/FRAMEWORK.md#modeling-modes), [Run loops](../../tools/plant-model/FRAMEWORK.md#run-loops)).
- Tofrowaih et al. (2025) write $C_{rr}$ as μk and split $C_dA$ into Cd and Af. Only the product $C_dA$ enters the framework.

## Process

1. Started from Table 2 of Tofrowaih et al. (2025): Cd 0.2, Af 0.66 m², μk 0.015, $m$ 150 kg.
2. Traced each value to its cited source, and judged whether the source fits a kart.
3. Searched kart literature for measured or fitted values, and saved the useful sources here.
4. Checked frontal dimensions in the [adult league regulations](../Adult%20Racing%20Leagues/adult-racing-leagues.md).
5. The builder chose the first-pass values and sweeps on 2026-11-04.
6. A JoyRide coast-down test replaces $C_dA$ and $C_{rr}$ once a kart exists.

Load at 45 mph (20.1 m/s, the REQ-SYS-001 target), from $F_{aero}$ and $F_{roll}$ in the [Vehicle](../../tools/plant-model/FRAMEWORK.md#vehicle) equations:

| Term | Baseline | Sweep range |
| --- | --- | --- |
| $F_{aero}$ | 139 N, 2.8 kW | 111 to 165 N, 2.2 to 3.3 kW |
| $F_{roll}$, at 276 kg | 81 N, 1.6 kW | 41 to 152 N, 0.8 to 3.1 kW |

$F_{roll}$ has the wider range, and it acts at every speed above standstill.

## Air density, gravity, and grade

- $\rho$ is the ISA sea-level value at 15 °C. Hotter or higher air lowers drag, so it errs high.
- $g$ is standard gravity.
- $\theta$ is 0 for a flat track. A grade case needs only a new value, since $F_{grade}$ is already in the framework.

## Drag area

Question: what $C_dA$ does a kart with an adult driver have?

Tofrowaih et al. was rejected as a source:

- Cd 0.2 cites Abdullah et al. (2023). That paper models a Proton Perdana sedan with Cd 0.31, and 0.2 appears nowhere in it.
- Their $C_dA$ of 0.13 m² is 3 to 5 times below every measured kart.

Measured or fitted karts with drivers:

| Source | Kart | Method | Cd | Af (m²) | $C_dA$ (m²) | Af at Cd 0.8 (m²) |
| --- | --- | --- | --- | --- | --- | --- |
| Biancolini, GMC 2007 | Land speed record kart | CFD at 90 km/h | 0.78 | 0.575 | 0.448 | 0.56 |
| Biancolini, GMC 2007 | Same kart | Coast-down | 0.899 | 0.575 | 0.517 | 0.65 |
| Thapa et al. 2024 | Kettering 48 V evGrandPrix kart | Fitted to track data | 0.654 | 1.019 | 0.666 | 0.83 |

Considered and not used:

| Source | Cd | Af (m²) | $C_dA$ (m²) | Reason |
| --- | --- | --- | --- | --- |
| Tofrowaih et al. 2025 | 0.2 | 0.66 | 0.13 | Cd has no kart source |
| Istardi 2009 (Chalmers) | 0.6 | 0.5 | 0.30 | Assumed, for a 110 kg kart with driver |
| Del Bene and Anello | 0.794, 0.75 to 0.9 typical | not stated | not stated | No area, so no $C_dA$ |
| League regulations | none | 1.54 upper bound | none | Envelope only: CIK-FIA 1400 mm wide; OTL Storm 1410 by 1090 mm |

Decision:

- The builder set Cd at 0.8 for the first pass. It sits in the 0.65 to 0.9 kart range.
- The builder asked for an Af that reproduces the measured $C_dA$ values at Cd 0.8. That gives 0.56 to 0.83 m².
- Baseline Af is the midpoint, 0.70 m². The sweep covers both sources.
- The 0.83 m² end is the conservative case. The driver causes about a third of kart drag (Del Bene and Anello), and JoyRide's driver is heavier.
- Kettering's fitted Cd and Af trade off against each other, so only their product is meaningful.

## Rolling resistance

Question: what $C_{rr}$ does a small bias-ply kart tire have under an adult load?

| Source | $C_{rr}$ | Basis |
| --- | --- | --- |
| Rajamani, via Tofrowaih et al. | 0.015 | Passenger-car radial tire on pavement |
| Adegbohun et al. 2021 | 0.01 | Converted passenger car, checked on a chassis dyno |
| Istardi 2009 (Chalmers) | 0.03 | Assumed for a kart, no source given |
| Fauzi et al. 2022 (UTHM) | 0.04 | Assumed for a kart, no source given |
| Thapa et al. 2024 | 0.0563 | Fitted on a kart. It absorbs driveline friction, since that model has no separate loss term. |
| Eder et al., SAE 2021-01-0936 | not public | Coast-down of bias-ply kart tires, on a rig for rims under 10 inches |

The Eder et al. values would settle this. Searches found no open copy, citation, or summary that quotes them. The abstract gives only the method.

Decision: with no measurement available, the builder accepted a best guess of 0.03.

- Small bias-ply tires lose more energy than car radials, so the car values of 0.010 to 0.015 are a lower bound.
- The two kart models that assume a value use 0.03 and 0.04.
- The framework's [Driveline](../../tools/plant-model/FRAMEWORK.md#driveline) carries $\eta_d$ separately. Thapa et al.'s 0.0563 double-counts driveline friction, so it is the upper bound.
- JoyRide's load per tire is about twice a race kart's. More deflection pushes $C_{rr}$ up, not down.
- The framework switches $F_{roll}$ off at standstill with a smooth step. That changes no value here.

## Mass and rotating mass

Question: what $m$ and $k_m$ does the sizing model carry?

$m$ is driver plus kart:

| Part | Value | Source |
| --- | --- | --- |
| Driver | 136 kg (300 lb) | REQ-SYS-003 in [GOALS.md](../../docs/project/GOALS.md#system-requirements) |
| Kart | 110 to 140 kg, estimate | BSR X4 to Rotax E20 range in [adult-racing-leagues.md](../Adult%20Racing%20Leagues/adult-racing-leagues.md#extrapolation-for-joyride) |
| Driver gear | TBD | Not yet estimated |
| Total | 246 to 276 kg | Without gear |

- Tofrowaih et al.'s 150 kg is their own prototype, so it was not used.
- The builder lowered REQ-SYS-003 from a 400 lb to a 300 lb driver on 2026-11-04.
- Kart mass waits on more analysis of the adult league data.

$k_m$ scales $m$ in the acceleration term only. It stands for the wheels, axle, sprockets, and rotor, which spin up with the kart. The framework defines it from $J_{wheel}$, $J_{rotor}$, $N$, and $r_w$ in [Vehicle](../../tools/plant-model/FRAMEWORK.md#vehicle).

- Thapa et al. fitted 1.13 on their kart. Adegbohun et al. use the same term for a car.
- JoyRide's heavier load dilutes the same inertia, so its value may sit below 1.13. A higher $N$ raises it, since the rotor counts as $N^2 J_{rotor}$.
- Sizing sets $k_m$ to 1.13 directly, and sweeps it down to 1.0. Once the motor, ratio, and wheels are chosen, compute it from $J_{total}$.

## Open parameters

Other Vehicle and Driveline symbols in the framework have no value yet:

| Symbol | Parameter | Status | Set by |
| --- | --- | --- | --- |
| $r_w$ | `r_wheel` | TBD | Wheel and tire choice. Tofrowaih et al. use 0.15 m, and Istardi uses 0.14 m. |
| $J_{wheel}$ | `J_wheel` | TBD | Wheel, axle, and wheel-side sprocket choice |
| $J_{rotor}$ | `J_rotor` | TBD | Motor and motor-side sprocket choice |
| $N$ | `N` | Sizing output | The sweep, per the framework's [Sizing outputs](../../tools/plant-model/FRAMEWORK.md#sizing-outputs) |
| $\eta_d$ | `eta_d` | TBD | Chain or belt choice |
| $v_\epsilon$ | `v_eps` | TBD | Solver tuning, once a model runs |

Values for these are tracked as open item 7 in the [plant model README](../../tools/plant-model/README.md#open-items).

## Sources

Local copies, accessed 2026-11-04:

| File | Used for |
| --- | --- |
| [Longitudinal Dynamics Modeling of an Electric Go Kart](Longitudinal%20Dynamics%20Modeling%20of%20an%20Electric%20Go%20Kart.pdf) | Tofrowaih et al. 2025, Table 2 starting values |
| [Model-Based Parameters Estimation for Electric Race Vehicles](Model-Based%20Parameters%20Estimation%20for%20Electric%20Race%20Vehicles.pdf) | Thapa et al. 2024, fitted Cd, Af, $C_{rr}$, and $k_m$ (Table 1) |
| [High Performance Electric Vehicle Powertrain Modeling, Simulation and Validation](High%20Performance%20Electric%20Vehicle%20Powertrain%20Modeling,%20Simulation%20and%20Validation.pdf) | Adegbohun et al. 2021, car $C_{rr}$ and the $k_m$ term |
| [Modeling and Energy Consumption Determination of an Electric Go-Kart](Modeling%20and%20Energy%20Consumption%20Determination%20of%20an%20Electric%20Go-Kart.pdf) | Istardi 2009, assumed kart Cd, Af, and $C_{rr}$ (Table 5.1) |
| [CIK-FIA Karting Technical Regulations 2025](../Adult%20Racing%20Leagues/CIK-FIA%20Karting%20Technical%20Regulations%202025.pdf) | Chassis envelope |
| [OTL Storm EFD Kart Technical Data Sheet 2020](../Adult%20Racing%20Leagues/OTL%20Storm%20EFD%20Kart%20Technical%20Data%20Sheet%202020.pdf) | Rental kart dimensions |

Links:

| Link | Used for |
| --- | --- |
| [Evaluation of Aerodynamic Drag of Go-Karts by Coast Down Test and CFD](Evaluation%20of%20Aerodynamic%20Drag%20of%20Go-Karts%20by%20Coast%20Down%20Test%20and%20CFD.webloc) | Biancolini, CFD and coast-down Cd, 0.575 m² area |
| [Go-Kart Aerodynamic Optimization by CFD and RBF Mesh Morphing](Go-Kart%20Aerodynamic%20Optimization%20by%20CFD%20and%20RBF%20Mesh%20Morphing.webloc) | Del Bene and Anello, kart Cd range and driver share |
| [Evaluating Rolling Resistance in Kart Racing Tires - SAE 2021-01-0936](Evaluating%20Rolling%20Resistance%20in%20Kart%20Racing%20Tires%20-%20SAE%202021-01-0936.webloc) | Kart tire rolling resistance, values not public |
| [Abdullah et al. 2023, DOI 10.15282/ijame.20.4.2023.01.0836](https://doi.org/10.15282/ijame.20.4.2023.01.0836) | Tofrowaih et al.'s reference [38]: sedan, Cd 0.31 |

Not saved: Fauzi et al. 2022 (PEAT vol. 3 no. 2), which assumes a $C_{rr}$ of 0.04 without a source.
