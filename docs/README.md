---
id: README
title: JoyRide documentation index
status: draft
owner: Braden Toone (builder)
last_updated: 2026-10-06
source_sections: [1, 4]
---

# JoyRide documentation

JoyRide is an open-source, hobby electric go-kart project. The journey is the goal. These documents were drawn from the [launch document](launch/JoyRide-Launch-Document.md).

## Documents

| Document | What it covers |
| --- | --- |
| [PROJECT.md](project/PROJECT.md) | How work is done: charter, constraints, approach, cycle template, safety, budget, learning, and checkpoints |
| [SUBSYSTEMS.md](subsystems/SUBSYSTEMS.md) | What each subsystem is responsible for, plus the risk register |
| [STG-1-ARCHITECTURE.md](stages/STG-1-ARCHITECTURE.md) | Stage 1: setup, research, system goals, and architecture |
| [STG-2-DRV.md](stages/STG-2-DRV.md) | Stage 2 cycle for motor and drive |
| [STG-2-PACK.md](stages/STG-2-PACK.md) | Stage 2 cycle for battery pack, BMS, and power distribution |
| [STG-2-CHS.md](stages/STG-2-CHS.md) | Stage 2 cycle for chassis and mechanical |
| [STG-2-VCU.md](stages/STG-2-VCU.md) | Stage 2 cycle for the vehicle control unit |
| [STG-2-TEL.md](stages/STG-2-TEL.md) | Stage 2 cycle for telemetry and apps |
| [STG-2-NET.md](stages/STG-2-NET.md) | Stage 2 cycle for network and harness |
| [STG-2-TMS.md](stages/STG-2-TMS.md) | Stage 2 cycle for thermal management (optional stub) |
| [STG-2-RMT.md](stages/STG-2-RMT.md) | Stage 2 cycle for remote and wireless (optional stub) |
| [STG-3-INTEGRATION.md](stages/STG-3-INTEGRATION.md) | Stage 3: integration and the kart MVP |
| [JoyRide-Launch-Document.md](launch/JoyRide-Launch-Document.md) | The original launch document, kept for reference |

## Recommended reading order

1. [PROJECT.md](project/PROJECT.md), for how the project works.
2. [SUBSYSTEMS.md](subsystems/SUBSYSTEMS.md), for what is being built.
3. [STG-1-ARCHITECTURE.md](stages/STG-1-ARCHITECTURE.md), for what to do first.
4. The STG-2 documents, in the recommended order: DRV, PACK, CHS, VCU, TEL, NET.
5. [STG-3-INTEGRATION.md](stages/STG-3-INTEGRATION.md), when two subsystems work.

## Stage IDs

| ID | Stage | Part of Spark |
| --- | --- | --- |
| STG-1 | Architecture | Prerequisite |
| STG-2-DRV | Motor and drive | Yes |
| STG-2-PACK | Battery pack, BMS, and power distribution | Yes |
| STG-2-CHS | Chassis and mechanical | No |
| STG-2-VCU | Vehicle control unit | Not yet decided |
| STG-2-TEL | Telemetry and apps | Not yet decided |
| STG-2-NET | Network and harness | Not yet decided |
| STG-2-TMS | Thermal management (optional) | Not yet decided |
| STG-2-RMT | Remote and wireless (optional) | Not yet decided |
| STG-3 | Integration and the kart MVP | Not required |
