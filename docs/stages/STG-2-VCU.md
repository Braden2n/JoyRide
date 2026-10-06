---
id: STG-2-VCU
title: "Stage 2: VCU subsystem cycle"
status: draft
owner: Braden Toone (builder)
last_updated: 2026-10-06
subsystem: SUB-VCU
spark: not yet decided
source_sections: [7, 8, 9, 10, 12, 13]
---

# STG-2-VCU: Vehicle control unit cycle

## Purpose

This cycle takes VCU from a learning burst to a dev board running the vehicle state machine. VCU owns most of the application-layer logic and state, including the driver-facing LEDs.

## Inputs

- [Subsystem cycle template](../project/PROJECT.md#subsystem-cycle)
- [VCU subsystem definition](../subsystems/SUBSYSTEMS.md#vcu-vehicle-control-unit)
- [System goals](STG-1-ARCHITECTURE.md#requirements)
- PACK control states from [STG-2-PACK](STG-2-PACK.md) and DRV interfaces from [STG-2-DRV](STG-2-DRV.md)
- [Safety approach](../project/PROJECT.md#safety-approach)

**Neighbors to review.** No subsystem is defined in isolation. This cycle reviews these interfaces and feeds changes back.

| Neighbor | What to review |
| --- | --- |
| [PACK](../subsystems/SUBSYSTEMS.md#pack-battery-pack-bms-and-power-distribution) | Pack state messages and the control states they define |
| [DRV](../subsystems/SUBSYSTEMS.md#drv-motor-and-drive) | Torque requests and DRV status |
| [TEL](../subsystems/SUBSYSTEMS.md#tel-telemetry-and-apps) | Status and fault reports; dashboard decision |
| [NET](../subsystems/SUBSYSTEMS.md#net-network-and-harness) | Message needs; MCU family and RTOS decision |

## Goals

- Build working vocabulary in embedded C or C++, RTOS tasks, and state machines.
- Design and test the vehicle state machine on a computer.
- Run the state machine on a dev board with redundant throttle and status LEDs.

## Requirements

Values are TBD unless the builder fixed them.

| ID | Requirement | Target | How to check | Source |
| --- | --- | --- | --- | --- |
| REQ-VCU-001 | No single sensor or software fault commands unintended acceleration (system goal) | Per [STG-1](STG-1-ARCHITECTURE.md#requirements); fault behavior defined in this cycle | Fault-injection test | Section 7 |
| REQ-VCU-002 | VCU processes throttle input with a plausibility check. | TBD | Test | Sections 8, 10, 12 |
| REQ-VCU-003 | VCU sends torque requests to DRV. | TBD | Test | Section 8 boundaries |
| REQ-VCU-004 | VCU runs a vehicle state machine with driving modes, derate, and safe states. | TBD | Functional test | Sections 8, 10 |
| REQ-VCU-005 | VCU reads PACK state and reports to TEL. | TBD | Test | Section 8 boundaries |
| REQ-VCU-006 | VCU drives simple driver-facing status LEDs. | TBD | Inspection | Section 8 responsibilities |
| REQ-VCU-007 | VCU removes torque on a lost signal, lost heartbeat, or watchdog trip. | TBD | Fault-injection test | Section 12 principles |

## Tasks

### Step 1: Learning burst (3 to 7 days, free)

- [ ] Study embedded C or C++ and RTOS tasks.
- [ ] Study state machines.
- [ ] Study sensor plausibility checks.
- [ ] Study derate and safe-state patterns.
- [ ] Study LED status indication.
- [ ] Keep a "what I still don't understand" list.

### Step 2: Needs and MVP sketch (1 to 2 days, free)

- [ ] Write a one-page needs sketch: what VCU must do, key numbers, interfaces to neighbors, and safety concerns.
- [ ] Note VCU's safe state and failure behavior.
- [ ] Confirm or change the draft subsystem MVP below.

Draft subsystem MVP (proposed, builder to confirm):

| Item | Draft |
| --- | --- |
| Prototype | PRT-VCU-01: a dev board reading two potentiometers as redundant throttle |
| Setup | The state machine runs against simulated PACK and DRV messages and drives status LEDs |
| Test | TST-VCU-001 |
| Pass or fail criterion | Pass if every state transition behaves as designed. A throttle disagreement or a simulated fault must also drive the state machine to a safe state with zero torque request. Thresholds TBD. |

### Step 3: Concepts (1 to 3 days, free)

- [ ] Sketch two or three options (buy, adapt open source, build) and compare them informally. Weigh learning value, cost, and fit.
- [ ] Treat safety as a pass or fail screen.
- [ ] Log the choice and the rejected options in the decision log.

Concept scoring is left blank on purpose. The rows are examples from the launch document.

| ID | Concept | Learning value | Cost | Fit | Safety screen |
| --- | --- | --- | --- | --- | --- |
| CON-VCU-A | STM32 with FreeRTOS | | | | |
| CON-VCU-B | STM32 with Zephyr | | | | |
| CON-VCU-C | Another dev board family | | | | |

### Step 4: Paper proof of concept (1 to 2 weeks, free)

- [ ] Draw the vehicle state machine, including derate and safe states.
- [ ] Define throttle processing and the LED indications.
- [ ] Test the logic on a computer.
- [ ] Draft VCU message needs and hand them to NET.
- [ ] Start a short FMEA, since VCU is safety-relevant.

### Step 5: Spend checkpoint (an hour, free)

- [ ] Answer the [spend checkpoint](../project/PROJECT.md#checkpoints) questions.
- [ ] Write down the one question the purchase answers.
- [ ] Decide go, adjust, or park.

### Step 6: Subsystem MVP (2 to 6 weeks)

- [ ] Set up the embedded toolchain for the chosen board.
- [ ] Buy the dev board and parts, and log each purchase with the VCU code.
- [ ] Build PRT-VCU-01 and run TST-VCU-001.
- [ ] Judge the result against the pass or fail criterion.

### Step 7: Fold-back (1 to 2 days, free)

- [ ] Answer the [fold-back checkpoint](../project/PROJECT.md#checkpoints) questions.
- [ ] Update the system goals, interfaces, and hazard list.
- [ ] Feed interface changes back to PACK, DRV, TEL, and NET.
- [ ] Do the enjoyment check, and choose the next subsystem.
- [ ] Write a short process retrospective.

## Deliverables

- Journal entries and a one-page needs sketch.
- State machine diagram, throttle processing definition, and LED indication table.
- Concept comparison and logged decision.
- Bench results for TST-VCU-001.
- Updated goals, interfaces, hazard list, and budget tracker.

## Spend

Steps 1 to 5 are free. The rough first spend is $30 to $60. See [PROJECT.md](../project/PROJECT.md#budget-and-purchasing).

## Risks and hazards

RSK-002 (unintended acceleration) and RSK-007 (injury while driving) apply. See the [register](../subsystems/SUBSYSTEMS.md#seed-hazard-and-risk-register).

## Decisions to make

| Decision | Shared with |
| --- | --- |
| MCU family and RTOS | NET |
| Dashboard approach | TEL |
| Fault behavior for REQ-VCU-001 | None |

## Checkpoint questions

Use the spend and fold-back questions in [PROJECT.md](../project/PROJECT.md#checkpoints). VCU adds:

- Does every injected throttle or message fault end in a safe state?
- Are the LED indications clear without a dashboard?

## Out of scope

- The hardware E-stop path. It belongs to PACK and works without VCU.
- Detailed driver and debug displays. They belong to TEL.
- Remote kill and wireless configuration. They belong to the optional RMT.

## Open items

| # | Open item | Owner |
| --- | --- | --- |
| 1 | Targets for REQ-VCU-002 to REQ-VCU-007 | Builder decision |
| 2 | Pass or fail thresholds for TST-VCU-001 | Builder decision |
| 3 | Whether VCU is part of Spark | Builder decision |
