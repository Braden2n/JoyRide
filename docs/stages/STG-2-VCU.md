---
id: STG-2-VCU
status: Not started
updated: 2026-10-06
stage_type: cycle
subsystem: VCU
spark: not yet decided
---

# STG-2-VCU: Vehicle control unit

## Purpose

Design the vehicle state machine and run it on a dev board with redundant throttle and status LEDs.

## Entry and exit

- Entry: the CHS fold-back chose VCU.
- Exit: the fold-back checkpoint is answered, or the cycle is parked at the spend checkpoint.

## Inputs and neighbors

- PACK control states and DRV interfaces from their cycles.
- Neighbors: PACK, DRV, TEL, NET. Interfaces are in [SUBSYSTEMS.md](../architecture/SUBSYSTEMS.md#vcu-vehicle-control-unit).

## Goals

- A state machine with derate and safe states, tested on a computer.
- A dev board that reaches a safe state on any throttle disagreement or simulated fault.

## System goals served

REQ-SAF-004.

## Tasks

### Step 1: Learning burst

- [ ] Study embedded C or C++, RTOS tasks, and state machines.
- [ ] Study sensor plausibility checks, and derate and safe-state patterns.
- [ ] Study LED status indication.

### Step 2: Needs and MVP sketch

- [ ] Create `subsystems/VCU/docs/` from the subsystem templates.
- [ ] Write REQUIREMENTS.md, including torque removal on a lost signal, lost heartbeat, or watchdog trip.
- [ ] Confirm the draft MVP below.

| MVP | Draft (proposed, builder to confirm) |
| --- | --- |
| Prototype | PRT-VCU-01: a dev board reading two potentiometers as redundant throttle, against simulated PACK and DRV messages, driving status LEDs |
| Test | TST-VCU-001 |
| Pass or fail | Every state transition behaves as designed, and any throttle disagreement or simulated fault ends in a safe state with zero torque request. Thresholds TBD. |

### Step 3: Concepts

- [ ] Compare MCU families and RTOS options, for example STM32 with FreeRTOS or Zephyr, or another dev board.

### Step 4: Paper proof of concept

- [ ] Draw the state machine, including derate and safe states.
- [ ] Define throttle processing and the LED indications.
- [ ] Test the logic on a computer.
- [ ] Send VCU message needs to NET.
- [ ] Draft the FMEA.

### Step 5: Spend checkpoint

- [ ] Write the question the purchase answers.

### Step 6: Subsystem MVP

- [ ] Set up the embedded toolchain.
- [ ] Build PRT-VCU-01 and run TST-VCU-001.

### Step 7: Fold-back

- [ ] Feed changes back to PACK, DRV, TEL, NET, GOALS, and RISKS.

## Deliverables

Standard cycle deliverables, plus the state machine diagram and the LED indication table.

## Spend

$30 to $60.

## Risks

RSK-002, RSK-007.

## Decisions

| Decision | Shared with | DEC |
| --- | --- | --- |
| MCU family and RTOS | NET | |
| Dashboard approach: LEDs only, a small display, or a web app | TEL | |

## Checkpoint additions

- Does every injected throttle or message fault end in a safe state?
- Are the LED indications clear without a dashboard?

## Out of scope

- The hardware E-stop path (PACK).
- Detailed driver and debug views (TEL).
- Remote kill (RMT).

## Open items

| # | Open item | Owner |
| --- | --- | --- |
| 1 | Whether VCU is part of Spark | Builder decision |
