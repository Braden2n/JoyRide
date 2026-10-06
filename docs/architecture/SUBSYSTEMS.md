---
id: SUBSYSTEMS
status: draft
updated: 2026-10-06
---

# JoyRide subsystems

What each subsystem is responsible for, and how they connect. Work plans are in the [stage documents](../README.md#stages). Goal owners are in [GOALS.md](../project/GOALS.md), and risks are in [RISKS.md](../project/RISKS.md).

## Contents

- [Architecture](#architecture)
- [Interfaces](#interfaces)
- [DRV: Motor and drive](#drv-motor-and-drive)
- [PACK: Battery pack, BMS, and power distribution](#pack-battery-pack-bms-and-power-distribution)
- [CHS: Chassis and mechanical](#chs-chassis-and-mechanical)
- [VCU: Vehicle control unit](#vcu-vehicle-control-unit)
- [TEL: Telemetry and apps](#tel-telemetry-and-apps)
- [NET: Network and harness](#net-network-and-harness)
- [TMS: Thermal management (optional)](#tms-thermal-management-optional)
- [RMT: Remote and wireless (optional)](#rmt-remote-and-wireless-optional)

## Architecture

Six core subsystems share one CAN bus. Two optional subsystems become real only if a need appears.

- **Power flow.** PACK stores energy and releases it through its main fuse, precharge, and contactors to DRV. DRV turns it into torque at the wheels. CHS carries both, and its brakes work without the electrics.
- **Network.** One central VCU plus CAN nodes, with a gateway to wireless. Three to five nodes is plenty to start. VCU reads PACK state, sends torque requests to DRV, and reports to TEL. TEL listens and links wirelessly to dashboards.
- **Safe state.** Traction power off. A hardware path reaches it without software: the BMS-controlled contactors plus a mechanical E-stop loop.
- **Folded roles.** Power distribution is part of PACK. The driver-facing status LEDs are part of VCU. Detailed driver and debug information lives in TEL.

## Interfaces

Interface definitions are cross-subsystem contracts. Each one gets a file in `interfaces/` from the [interface template](../templates/interface.md). Rough sketches come from [STG-1](../stages/STG-1-ARCHITECTURE.md) task group 1d.

| ID | Between | Type | Status |
| --- | --- | --- | --- |

## DRV: Motor and drive

Converts electrical power into torque at the wheels.

**Responsibilities:** motor, controller or inverter, gearing, torque output, and motor and controller temperature monitoring.

**Boundaries and authority:**

- Acts on torque requests from VCU. It has no authority over traction power.
- Receives traction power only through the PACK contactors.
- Removes torque on a lost signal, lost heartbeat, or watchdog trip.

| Neighbor | Interface |
| --- | --- |
| PACK | Traction power; voltage and current compatibility |
| VCU | Torque requests in, status out |
| CHS | Motor and gearing mounts, drive wheel connection |
| NET | CAN node and harness |

**Starting point:** commercial motor and controller first, own controller later (Gold).

**Stage:** [STG-2-DRV](../stages/STG-2-DRV.md)

## PACK: Battery pack, BMS, and power distribution

Stores energy, protects the cells, and switches traction power.

**Responsibilities:**

- Cells, monitoring, balancing, protection, and state of charge estimation.
- Main fuse, contactors, and precharge.
- Cell temperature monitoring.
- The mechanical E-stop loop.
- HVIL and IMD, only if found necessary below 60 V DC.

**Boundaries and authority:**

- The BMS has authority over the contactors, precharge, and any HVIL or IMD.
- The E-stop loop works independently of software.
- The pack's states define most of the VCU's control states.

| Neighbor | Interface |
| --- | --- |
| DRV | Traction power; current and energy needs |
| VCU | Pack state out |
| CHS | Pack mounts and enclosure; E-stop placement |
| NET | CAN node, harness, connectors |

**Starting point:** a pack assembled from cells ([DEC-004](../decisions/DEC-004-pack-from-cells.md), proposed).

**Stage:** [STG-2-PACK](../stages/STG-2-PACK.md)

## CHS: Chassis and mechanical

Carries the loads and mounts everything else.

**Responsibilities:** frame, steering, brakes, mounts, enclosures, and mass distribution.

**Boundaries and authority:**

- Brakes work independently of the electrics.
- Mount points for PACK and DRV set the integration details.

| Neighbor | Interface |
| --- | --- |
| PACK | Pack mounts and enclosure |
| DRV | Motor and gearing mounts |
| VCU, NET | Node mounts, harness routing, driver controls |

**Starting point:** brackets in CAD. Buy a used frame late, at integration.

**Stage:** [STG-2-CHS](../stages/STG-2-CHS.md)

## VCU: Vehicle control unit

Turns driver intent into safe torque requests.

**Responsibilities:** throttle processing, torque requests, driving modes, the vehicle state machine, fault handling, the derate strategy, and driver status LEDs.

**Boundaries and authority:**

- Owns the application-layer logic and state.
- Does not own the hardware safe-state path. The E-stop loop and contactors work without VCU.
- Makes derating decisions from PACK and DRV temperature data.

| Neighbor | Interface |
| --- | --- |
| PACK | Pack state in |
| DRV | Torque requests out, status in |
| TEL | Status and fault reports out |
| Driver | Throttle in, status LEDs out |

**Starting point:** own design on a dev board.

**Stage:** [STG-2-VCU](../stages/STG-2-VCU.md)

## TEL: Telemetry and apps

Logs, displays, and analyzes data. It is the hub for monitoring, debugging, and validation.

**Responsibilities:** data logging, detailed and debug views, web or mobile dashboards, and Python analysis.

**Boundaries and authority:** listens on CAN, with no control authority.

| Neighbor | Interface |
| --- | --- |
| NET | CAN listening; DBC as the data contract |
| VCU, PACK, DRV | Data they publish |
| Builder | Wireless link to dashboards |

**Starting point:** software only, on simulated data.

**Stage:** [STG-2-TEL](../stages/STG-2-TEL.md)

## NET: Network and harness

Owns the bus and records every interface as a contract.

**Responsibilities:** CAN bus, DBC, message contracts, connectors, wiring diagrams, labeling, and the harness.

**Boundaries and authority:** message needs come from the other cycles. NET records them and owns the physical network.

| Neighbor | Interface |
| --- | --- |
| All subsystems | Messages, connectors, harness |

**Starting point:** a DBC skeleton in Stage 1, grown during the other cycles.

**Stage:** [STG-2-NET](../stages/STG-2-NET.md)

## TMS: Thermal management (optional)

Passive cooling with monitoring and a derate strategy. It becomes a subsystem only if monitoring shows a need.

**Boundaries and authority:** monitoring sits in PACK and DRV, and derating in VCU.

**Stage:** [STG-2-TMS](../stages/STG-2-TMS.md)

## RMT: Remote and wireless (optional)

Remote kill, speed limiting, and wireless configuration. It is a parking-lot idea until the core subsystems are done.

**Boundaries and authority:** additive only. It never replaces the hardware E-stop.

**Stage:** [STG-2-RMT](../stages/STG-2-RMT.md)
