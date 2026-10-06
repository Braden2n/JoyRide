---
id: SUBSYSTEMS
title: JoyRide subsystems
status: draft
owner: Braden Toone (builder)
last_updated: 2026-10-06
source_sections: [2, 7, 8, 9, 10, 12, 13, 17]
---

# JoyRide subsystems

This document defines what each subsystem is responsible for. How and when work is done lives in [PROJECT.md](../project/PROJECT.md) and the stage documents.

Everything named here as a part, tool, protocol, method, or value is an example to consider, not a decision. Only the high-level requirements and the builder's fixed constraints are binding.

## Architecture overview

The kart has six core subsystems on one CAN bus, plus two optional additions. The launch document's architecture diagram did not export, so this section describes it in words.

**Power flow.** Energy is stored in PACK. It leaves the pack through the main fuse, precharge, and contactors, which are physically part of the pack. It then reaches DRV, which converts it to torque at the wheels. CHS carries both and provides brakes that work independently of the electrics.

**CAN bus.** The suggested style is one central VCU plus CAN nodes, with a gateway to wireless. Three to five nodes is plenty to start. VCU reads PACK state, sends torque requests to DRV, and reports to TEL. TEL listens on the bus and links wirelessly to web or mobile dashboards. NET owns the bus itself and records every message and interface as a contract.

**Safe state.** The system-level safe state is traction power off. A hardware path reaches it without help from software. That path is the BMS-controlled contactors plus a mechanical E-stop loop. Lost signals, lost heartbeats, and watchdog trips also remove torque.

**Folded roles.** Two roles do not get their own subsystem:

- Power distribution (main fuse, contactors, precharge) is folded into PACK, because it is physically part of the pack.
- The driver-facing HMI role (simple status LEDs) is folded into VCU. Detailed driver and debug information lives in TEL, not on the kart.

**Optional additions.** TMS and RMT are dashed boxes on the diagram. They become subsystems only if needed.

**Nested, not siloed.** No subsystem is defined in complete isolation. Each section below lists its neighbors, and each cycle reviews them.

## Subsystem summary

Subsystems are listed in the builder's recommended order. The order is the builder's call and can change at any fold-back.

| Order | Code | Subsystem | One-line responsibility | Part of Spark | Rough first spend | Stage document |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | SUB-DRV | Motor and drive | Turns electrical power into torque at the wheels | Yes | $40 to $90 (small learning motor) or $150 to $400 (real motor and controller) | [STG-2-DRV](../stages/STG-2-DRV.md) |
| 2 | SUB-PACK | Battery pack, BMS, and power distribution | Stores energy, protects cells, and switches traction power | Yes | $100 to $250 | [STG-2-PACK](../stages/STG-2-PACK.md) |
| 3 | SUB-CHS | Chassis and mechanical | Carries loads, steers, brakes, and mounts everything | No | $0 to $50 | [STG-2-CHS](../stages/STG-2-CHS.md) |
| 4 | SUB-VCU | Vehicle control unit | Turns driver intent into safe torque requests | Not yet decided | $30 to $60 | [STG-2-VCU](../stages/STG-2-VCU.md) |
| 5 | SUB-TEL | Telemetry and apps | Logs, displays, and analyzes data | Not yet decided | $10 to $30 (a software-only start is free) | [STG-2-TEL](../stages/STG-2-TEL.md) |
| 6 | SUB-NET | Network and harness | Owns the bus, message contracts, and wiring | Not yet decided | $60 to $120 | [STG-2-NET](../stages/STG-2-NET.md) |
| Optional | SUB-TMS | Thermal management | Monitors heat and supports derating | Not yet decided | $0 to $30 | [STG-2-TMS](../stages/STG-2-TMS.md) |
| Optional | SUB-RMT | Remote and wireless | Remote kill, speed limiting, wireless configuration | Not yet decided | $30 to $60 | [STG-2-RMT](../stages/STG-2-RMT.md) |

Spend figures are approximate planning ranges from launch section 10. They exclude shared tools such as a multimeter. Check current prices before buying.

## System goal tags

Each system goal is defined once, in [STG-1](../stages/STG-1-ARCHITECTURE.md#requirements). Tagging each goal to its most responsible subsystem is a Stage 1 task. The tags below are proposals for Stage 1 to confirm.

| Goal | Short name | Proposed subsystem | Basis |
| --- | --- | --- | --- |
| REQ-SYS-001 | Useful top speed | DRV | Proposed |
| REQ-SYS-002 | Useful run time | PACK | Proposed |
| REQ-SYS-003 | Carries design load | CHS | Proposed |
| REQ-SYS-004 | Power and energy sized for speed, load, and run time | DRV and PACK | Proposed |
| REQ-PACK-001 | Below the voltage ceiling at full charge | PACK | ID prefix |
| REQ-PACK-002 | Protects cells and disconnects safely on faults | PACK | ID prefix |
| REQ-SAF-001 | Hardware E-stop removes traction power | PACK | Proposed, because PACK owns the E-stop loop |
| REQ-VCU-001 | No single fault commands unintended acceleration | VCU | ID prefix |
| REQ-NET-001 | Subsystems share a network | NET | ID prefix |
| REQ-COST-001 | Spend stays within the budget plan | Project-wide | Not a subsystem goal |

## Seed hazard and risk register

This is the seed register from the launch document. RSK IDs and subsystem links are new and proposed. The living version becomes the risk and hazard list described in [PROJECT.md](../project/PROJECT.md#tracking-artifacts-to-create-later).

If useful, score each risk on a simple 5 by 5 probability and impact scale.

| ID | Risk | Cause | Candidate mitigation | When it applies | Subsystems |
| --- | --- | --- | --- | --- | --- |
| RSK-001 | Lithium pack fire or thermal runaway | Cell damage, overcharge, short circuit, poor charging practice | Quality cells or a reputable pack, independent protection, main fuse near the pack, fire-safe charging area | Any lithium cell work | PACK |
| RSK-002 | Unintended acceleration | Sensor fault, firmware fault, controller fault | Redundant throttle sensing with a plausibility check, hardware E-stop, wheels-off testing, speed-limit modes | Any powered motion | VCU, DRV |
| RSK-003 | Short circuit or arc at the pack | Tool slip, wiring fault | Insulated tools, covers, fusing, precharge, a second look at wiring before power-up | Any high-current wiring | PACK, NET |
| RSK-004 | Poor ventilation for soldering fumes and lithium handling | The garage and spare bedroom lack good ventilation | Fume extraction or an open-air setup for soldering; ventilation and a fire-safe spot for charging; sorted out before the first physical iteration | Before any soldering or lithium work | Project-wide, PACK |
| RSK-005 | Loss of braking | Mechanical failure | Proven mechanical brakes that work independently of the electrics | Integration | CHS |
| RSK-006 | Structural failure | Frame crack, loose mount | Commercial frame, inspection checklist, torque marks | Integration | CHS |
| RSK-007 | Injury while driving | Speed, falls, collisions | Helmet, speed limit, a clear and closed test area | Integration | Project-wide, VCU |
| RSK-008 | Budget overrun | Parts mistakes, scrapped boards, scope growth | Monthly cap, spend checkpoints, small PCB runs | Throughout | Project-wide |
| RSK-009 | Lost interest or scope creep | Too many subsystems at once, slow progress | One subsystem at a time, an enjoyment check at fold-back, a backlog parking lot, Spark and Bronze as valid stops | Throughout | Project-wide |

## Decisions that will come up

These decisions are open unless marked decided. Each is logged with a DEC ID when it is made.

| Decision | Options to consider | Subsystems |
| --- | --- | --- |
| Nominal pack voltage | 24 V, 36 V, 48 V | PACK and DRV |
| Cell chemistry and pack source | Li-ion cells assembled by the builder (current preference), LiFePO4, or a commercial pack with its own BMS | PACK |
| Motor and controller for the kart MVP | Commercial BLDC kit, hub motor, brushed DC | DRV |
| MCU family and RTOS | STM32 with FreeRTOS or Zephyr, ESP32 for wireless, bare metal for simple nodes | NET and VCU |
| Dashboard approach | LEDs only, a small embedded display, a phone or laptop web app | VCU and TEL |
| Frame | Used kart frame, kit frame, custom welded | CHS |
| Charging approach | Commercial charger, builder-designed charger | PACK |
| Open or closed development | Decided: fully open source, with Git submodules per atomic piece | Project-wide |

## DRV: Motor and drive

SUB-DRV converts electrical power into torque at the wheels. It is first in the recommended order because motor and controller selection drives most of the other subsystem work.

**Responsibilities**

- Motor
- Controller or inverter
- Gearing
- Torque output

**Boundaries, interfaces, and authority**

- Takes torque requests from VCU over CAN.
- Takes traction power only through the PACK contactors. DRV has no authority over them.
- Removes torque on a lost signal, lost heartbeat, or watchdog trip.
- Hosts thermal monitoring for the motor and controller. Derating decisions sit in VCU.

| Neighbor | Interface | Status |
| --- | --- | --- |
| PACK | Traction power through the contactors; voltage and current compatibility | Rough, defined in Stage 1 and the DRV and PACK cycles |
| VCU | Torque requests and DRV status over CAN | Rough; message content TBD |
| CHS | Motor and gearing mount points | Set at integration |
| NET | CAN connection and harness | Recorded as a contract by NET |
| TEL | Speed, current, and status data on the bus | TBD |

**System goals tagged (proposed):** REQ-SYS-001, REQ-SYS-004.

**Hazards:** RSK-002.

**Starter guide**

| Item | Content |
| --- | --- |
| Learning burst topics | BLDC and PMSM basics, commutation, field-oriented control, current sensing, motor and controller specifications, SimpleFOC and VESC documentation |
| Paper proof of concept idea | Size motor and gearing against the Stage 1 system requirements. Shortlist motor and controller pairs. Check pack voltage and current compatibility. Make a go or no-go call on the system goals. |
| Subsystem MVP (isolated) | The chosen motor and controller, or a small learning motor, spun from a bench supply at low voltage. Speed and current are logged, and there is a safe stop. |

The DRV paper proof of concept doubles as a go or no-go check on the system goals. If DRV cannot meet them, the rest of the system probably cannot either.

**Decisions:** motor and controller for the kart MVP; nominal pack voltage (shared with PACK).

**Starting point:** commercial motor and controller first, own controller later. A builder-designed motor controller is the Gold-level outcome.

**Rough first spend:** $40 to $90 (small learning motor) or $150 to $400 (the real motor and controller).

**Spark:** part of Spark.

## PACK: Battery pack, BMS, and power distribution

SUB-PACK stores energy, protects the cells, and switches traction power. Power distribution is physically part of the pack and folded into this subsystem.

**Responsibilities**

- Cells, cell monitoring and balancing, protection, and state of charge estimation
- Main fuse, contactors, and precharge
- HVIL and IMD, only if determined necessary below 60 V DC
- The mechanical E-stop loop

**Boundaries, interfaces, and authority**

- The BMS has authority over the contactors and precharge, and over any HVIL or IMD.
- The mechanical E-stop loop works independently of software.
- The BMS and power path define most of the VCU's control states.
- Hosts thermal monitoring for the cells. Derating decisions sit in VCU.
- Detailed design of BMS authority belongs in the PACK stage documents. At this level, only ownership is recorded.

| Neighbor | Interface | Status |
| --- | --- | --- |
| DRV | Traction power through the contactors; current and energy needs | Rough; DRV's needs size the pack |
| VCU | Pack state over CAN | Rough; message content TBD |
| CHS | Pack mount points and enclosure; most chassis integration | Set at integration |
| NET | CAN connection, harness, connectors | Recorded as a contract by NET |
| TEL | Pack data on the bus | TBD |
| Driver | E-stop within reach | Placement TBD |

**System goals tagged (proposed):** REQ-PACK-001, REQ-PACK-002, REQ-SAF-001, REQ-SYS-002, REQ-SYS-004.

**Hazards:** RSK-001, RSK-003, RSK-004.

**Starter guide**

| Item | Content |
| --- | --- |
| Learning burst topics | Li-ion and LiFePO4 basics, cell limits and balancing, equivalent-circuit models, state of charge estimation, BMS front-end datasheets, fusing and wire sizing, contactors and precharge, E-stop loops, and whether HVIL or IMD is needed below 60 V DC |
| Paper proof of concept idea | Size the pack for DRV's current and energy needs. Fit a cell model to public data in Python. Calculate precharge time and resistor ratings. Size fuses and wires. Draw the BMS-controlled start-up sequence and E-stop loop in KiCad. |
| Subsystem MVP (isolated) | An isolated bench pack: a few series cells at low voltage. BMS logic controls a contactor or relay and runs the precharge and safety checks into a resistive or lamp load. It trips on injected faults, and the mechanical E-stop loop works. No motor. |

**Decisions:** nominal pack voltage (shared with DRV); cell chemistry and pack source; charging approach.

**Starting point:** assembling the pack from cells is the builder's current preference. It is still to be decided in the PACK cycle.

**Rough first spend:** $100 to $250.

**Spark:** part of Spark.

## CHS: Chassis and mechanical

SUB-CHS carries the loads and mounts everything else. Chassis constraints drive most of the PACK and DRV integration details.

**Responsibilities**

- Frame
- Steering
- Brakes
- Mounts and enclosures
- Mass distribution

**Boundaries, interfaces, and authority**

- Mount points for PACK and DRV set the integration details.
- Brakes work independently of the electrics.

| Neighbor | Interface | Status |
| --- | --- | --- |
| PACK | Pack mount points and enclosure | TBD |
| DRV | Motor and gearing mounts, drive wheel connection | TBD |
| VCU, NET | Node mounts and harness routing | TBD |
| Driver | Seating, steering, brake controls | TBD |

**System goals tagged (proposed):** REQ-SYS-003.

**Hazards:** RSK-005, RSK-006.

**Starter guide**

| Item | Content |
| --- | --- |
| Learning burst topics | Basic kart geometry, steering and braking, fasteners and welds, FreeCAD basics |
| Paper proof of concept idea | Lay out PACK and DRV mount locations and enclosures in CAD on a generic frame envelope. Estimate mass distribution at the Stage 1 design mass. |
| Subsystem MVP (isolated) | A CAD layout plus a cardboard or printed mock-up. Measure a used frame before buying one. |

**Decisions:** frame.

**Starting point:** design brackets in CAD, and buy a used frame late, at integration.

**Rough first spend:** $0 to $50.

**Spark:** not part of Spark. It must be addressed for later levels.

## VCU: Vehicle control unit

SUB-VCU turns driver intent into safe torque requests. It owns most of the application-layer logic and state.

**Responsibilities**

- Throttle processing and torque requests
- Driving modes and the vehicle state machine
- Fault handling and derate strategy
- Simple driver-facing LEDs (the folded HMI role)

**Boundaries, interfaces, and authority**

- Reads PACK state, commands DRV, and reports to TEL.
- Owns application-layer logic, but not the hardware safe-state path. The E-stop loop and contactors work without VCU.
- Owns the derate strategy, using thermal monitoring from PACK and DRV.
- May enforce a speed limit for field tests.

| Neighbor | Interface | Status |
| --- | --- | --- |
| PACK | Pack state in; control states derived from the BMS and power path | Rough; message content TBD |
| DRV | Torque requests out; DRV status in | Rough; message content TBD |
| TEL | Status and fault reports | TBD |
| NET | CAN connection, MCU family shared decision | Recorded as a contract by NET |
| Driver | Throttle input and status LEDs | TBD |

**System goals tagged (proposed):** REQ-VCU-001.

**Hazards:** RSK-002, RSK-007.

**Starter guide**

| Item | Content |
| --- | --- |
| Learning burst topics | Embedded C or C++, RTOS tasks, state machines, sensor plausibility checks, derate and safe-state patterns, LED status indication |
| Paper proof of concept idea | Draw the vehicle state machine, including derate and safe states. Define throttle processing and the LED indications. Test the logic on a computer. |
| Subsystem MVP (isolated) | A dev board reads two potentiometers as redundant throttle. It runs the state machine against simulated PACK and DRV messages and drives status LEDs. |

**Decisions:** MCU family and RTOS (shared with NET); dashboard approach (shared with TEL).

**Starting point:** own design on a dev board.

**Rough first spend:** $30 to $60.

**Spark:** not yet decided.

## TEL: Telemetry and apps

SUB-TEL logs, displays, and analyzes data. It is the hub for monitoring, debugging, and validation.

**Responsibilities**

- Data logging
- Detailed and debug information
- Web or mobile dashboards
- Analysis in Python

**Boundaries, interfaces, and authority**

- Listens on CAN. It has no control authority.
- Detailed driver and debug information lives here, not on the kart.
- Feeds any downstream capability.

| Neighbor | Interface | Status |
| --- | --- | --- |
| NET | CAN listening, DBC as the data contract | TBD |
| VCU | Status and fault reports; shared dashboard decision | TBD |
| PACK, DRV | Data on the bus | TBD |
| Builder | Wireless link to web or mobile dashboards | TBD |

**System goals tagged (proposed):** none in the section 7 list yet.

**Hazards:** none in the seed register.

**Starter guide**

| Item | Content |
| --- | --- |
| Learning burst topics | CAN logging, data formats, WebSocket or MQTT, simple web dashboards, Python analysis |
| Paper proof of concept idea | Mock up the dashboard and debug views and define a data schema, tested on simulated data. |
| Subsystem MVP (isolated) | A logger and web dashboard showing simulated, then live, CAN data, including a debug view. |

**Decisions:** dashboard approach (shared with VCU).

**Starting point:** a software-only start is free.

**Rough first spend:** $10 to $30.

**Spark:** not yet decided.

## NET: Network and harness

SUB-NET is the glue that holds everything together. It is mostly defined as the other subsystems' work proceeds, so it rarely needs much dedicated time.

**Responsibilities**

- CAN bus
- DBC and message and interface contracts
- Connectors, wiring diagrams, and labeling
- Harness

**Boundaries, interfaces, and authority**

- Interfaces are mostly defined during other subsystems' cycles. NET records them as contracts.
- NET touches every subsystem on the bus.

| Neighbor | Interface | Status |
| --- | --- | --- |
| All subsystems | Message needs, connectors, harness | Collected as each cycle defines them |
| VCU | MCU family and RTOS shared decision | Open |
| TEL | Logger and DBC consumer | TBD |

**System goals tagged (proposed):** REQ-NET-001.

**Hazards:** RSK-003 (wiring faults).

**Starter guide**

| Item | Content |
| --- | --- |
| Learning burst topics | CAN 2.0 framing and bit timing, termination, DBC files, SavvyCAN, python-can |
| Paper proof of concept idea | Starts light and grows with the other subsystems. Collect message needs as their cycles define them, draft them in a DBC, and estimate bus load for a candidate bit rate. |
| Subsystem MVP (isolated) | Two or three dev boards and a USB-CAN adapter exchanging DBC messages with a logger. |

**Decisions:** MCU family and RTOS (shared with VCU).

**Starting point:** starts light, as a DBC skeleton in Stage 1.

**Rough first spend:** $60 to $120.

**Spark:** not yet decided.

## Optional additions

These wait until the core subsystems are done. Each becomes a full subsystem only if a need appears.

### TMS: Thermal management (optional)

SUB-TMS covers passive cooling with monitoring and a derate strategy. It is not a subsystem unless monitoring shows it is needed.

- Boundaries: monitoring sits in PACK and DRV, and derating sits in VCU.
- Learning burst topics: cell and motor thermal limits, derating curves, simple temperature sensing.
- Paper proof of concept idea: estimate heating from the sizing and cell models. Decide whether passive cooling plus a derate strategy is enough.
- Subsystem MVP: temperature monitoring and derate logic prototyped inside the PACK and VCU MVPs. It becomes separate only if monitoring says it is needed.
- Rough first spend: $0 to $30.
- Spark: not yet decided.

### RMT: Remote and wireless (optional)

SUB-RMT covers remote kill, speed limiting, and wireless configuration. It is a parking-lot idea, considered only after the core subsystems.

- Learning burst topics: wireless link basics (ELRS or BLE), failsafe behavior, wireless safety.
- Paper proof of concept idea: design the remote kill concept and its failsafe behavior.
- Subsystem MVP: a wireless link between two dev boards with a failsafe test.
- Rough first spend: $30 to $60.
- Spark: not yet decided.
