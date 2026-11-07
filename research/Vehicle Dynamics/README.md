---
id: RESEARCH-VEHICLE-DYNAMICS
status: active
updated: 2026-11-04
---

# Vehicle Dynamics

Sources for the plant model's vehicle, driveline, motor, and battery blocks. Findings live in [vehicle-dynamics-constants.md](vehicle-dynamics-constants.md) and [adult-racing-leagues.md](../Adult%20Racing%20Leagues/adult-racing-leagues.md).

| File | What it gives the plant model | Plant block |
| --- | --- | --- |
| [Longitudinal Dynamics Modeling of an Electric Go Kart](Longitudinal%20Dynamics%20Modeling%20of%20an%20Electric%20Go%20Kart.pdf) | Simulink kart model with regen braking profiles. Its Cd is unsupported. | Vehicle, driveline, battery |
| [Model-Based Parameters Estimation for Electric Race Vehicles](Model-Based%20Parameters%20Estimation%20for%20Electric%20Race%20Vehicles.pdf) | Road-load parameters fitted to evGrandPrix kart data; gear ratio chosen against motor efficiency | Vehicle, driveline |
| [High Performance Electric Vehicle Powertrain Modeling, Simulation and Validation](High%20Performance%20Electric%20Vehicle%20Powertrain%20Modeling,%20Simulation%20and%20Validation.pdf) | Forward model checked against a chassis dyno; motor loss equations | Driver, motor and inverter |
| [Modeling and Energy Consumption Determination of an Electric Go-Kart](Modeling%20and%20Energy%20Consumption%20Determination%20of%20an%20Electric%20Go-Kart.pdf) | 48 V kart model with battery, converter, and motor losses over a measured lap | Motor and inverter, battery |
| [Analysis of Vehicle Dynamics Parameters for Electric Go-Kart (eKart) Design](Analysis%20of%20Vehicle%20Dynamics%20Parameters%20for%20Electric%20Go-Kart%20(eKart)%20Design.pdf) | Energy sizing from lap power and race time | Sizing method |
| [Electric Vehicle Powertrain Sizing](Electric%20Vehicle%20Powertrain%20Sizing.pdf) | Basic e-bike powertrain sizing steps | Sizing method |
| [Evaluation of Aerodynamic Drag of Go-Karts by Coast Down Test and CFD](Evaluation%20of%20Aerodynamic%20Drag%20of%20Go-Karts%20by%20Coast%20Down%20Test%20and%20CFD.webloc) | Kart Cd and frontal area, from CFD and coast-down | Vehicle |
| [Go-Kart Aerodynamic Optimization by CFD and RBF Mesh Morphing](Go-Kart%20Aerodynamic%20Optimization%20by%20CFD%20and%20RBF%20Mesh%20Morphing.webloc) | Kart Cd range and the driver's share of drag | Vehicle |
| [Evaluating Rolling Resistance in Kart Racing Tires - SAE 2021-01-0936](Evaluating%20Rolling%20Resistance%20in%20Kart%20Racing%20Tires%20-%20SAE%202021-01-0936.webloc) | Kart tire rolling resistance; paywalled | Vehicle |
| [Horsepower in Go-Karts - GoKarts USA](Horsepower%20in%20Go-Karts-%20A%20Practical%20Guide%20for%20Parents%20%E2%80%93%20GoKarts%20USA%C2%AE.webloc) | Power ranges for consumer karts | Sizing method |
