---
id: STG-3
title: "Stage 3: Integration and the kart MVP"
status: draft
owner: Braden Toone (builder)
last_updated: 2026-10-06
source_sections: [11, 12, 13, 16]
---

# STG-3: Integration and the kart MVP

## Purpose

Stage 3 connects subsystems as they mature and grows over time. It starts as soon as two subsystems work. Its first milestone is a drivable kart, the kart MVP. That kart uses the builder's own subsystems plus commercial placeholders for any subsystem that has not had its turn.

Integration is not required for Spark. The kart MVP is the Bronze evidence.

## Inputs

- [Stages and entry conditions](../project/PROJECT.md#stages)
- [Safety approach](../project/PROJECT.md#safety-approach)
- [Architecture overview](../subsystems/SUBSYSTEMS.md#architecture-overview) and every [subsystem definition](../subsystems/SUBSYSTEMS.md#subsystem-summary)
- [System goals](STG-1-ARCHITECTURE.md#requirements)
- Fold-back results from each STG-2 cycle

## Goals

- End up with a kart that drives safely at low speed.
- Keep a clear list of which placeholders to replace next.

## The kart MVP

The kart MVP is a kart that drives at low speed under its own power. It has a working E-stop, a protected battery, and controlled throttle. This definition is for the builder to confirm.

Which parts are the builder's own and which are commercial placeholders is decided at the architecture checkpoint. It is revisited after each subsystem cycle.

| Kart MVP criterion | Related goals |
| --- | --- |
| Drives at low speed under its own power | REQ-SYS-001, REQ-SYS-003 |
| Working E-stop | REQ-SAF-001 |
| Protected battery | REQ-PACK-001, REQ-PACK-002 |
| Controlled throttle | REQ-VCU-001 |

## Requirements

Stage 3 verifies the system goals on the vehicle. Targets are defined once, in STG-1.

| ID | Requirement | Target | How to check | Source |
| --- | --- | --- | --- | --- |
| REQ-SYS-001 | Useful top speed | Per [STG-1](STG-1-ARCHITECTURE.md#requirements) | GPS test | Section 7 |
| REQ-SYS-002 | Useful run time | Per [STG-1](STG-1-ARCHITECTURE.md#requirements) | Test | Section 7 |
| REQ-SYS-003 | Carries the design load | Per [STG-1](STG-1-ARCHITECTURE.md#requirements) | Test and analysis | Section 7 |
| REQ-SYS-004 | Power and energy sized for speed, load, and run time | Per [STG-1](STG-1-ARCHITECTURE.md#requirements) | Analysis and test | Section 7 |
| REQ-SAF-001 | Hardware E-stop removes traction power | Per [STG-1](STG-1-ARCHITECTURE.md#requirements) | Test and inspection | Section 7 |
| REQ-PACK-002 | Pack protects cells and disconnects safely on faults | Per [STG-1](STG-1-ARCHITECTURE.md#requirements) | Fault-injection test | Section 7 |
| REQ-VCU-001 | No single fault commands unintended acceleration | Per [STG-1](STG-1-ARCHITECTURE.md#requirements) | Fault-injection test | Section 7 |

## Tasks

### Integration ladder

Move up a rung when the previous one feels solid. A written checklist is optional.

1. [ ] Bench: two subsystems at a time, powered from a current-limited supply, with CAN traffic logged.
2. [ ] Rig: the full electrical system on the kart, drive wheels off the ground, E-stop within reach.
3. [ ] Low-speed field test: a clear, private area, a helmet, and a speed limit enforced in the VCU or controller.
4. [ ] Performance test: speed, acceleration, range, and thermal behavior, with data logged for analysis.
5. [ ] Endurance and review: repeated runs, inspection after each, and a data review in Python.

### Before the kart moves

- [ ] Buy MVP kart parts when enough subsystems work, funded by rollover.
- [ ] Confirm each subsystem on the kart meets its safety basics. One with unmet safety basics does not go on the kart.
- [ ] Test the E-stop and the BMS cutoffs at every rung.
- [ ] Hold the kart MVP checkpoint.

### Refinement and upgrades

- [ ] Turn every failed test into a short note with a cause and a fix, or a decision to accept it.
- [ ] Update the architecture, interfaces, and goals after each test campaign, and log why.
- [ ] After the kart MVP, replace placeholders one at a time with drop-in replacements in form, fit, and function.
- [ ] Keep the kart drivable. Do not remove a working part until its replacement works.

### Test types

| Type | Examples |
| --- | --- |
| Electrical | Continuity, insulation, voltage drop, load and temperature rise |
| Functional | Start-up sequence, state machine transitions, driving modes |
| Fault injection | Cell limit trips, E-stop, sensor disconnect, CAN loss, stuck throttle |
| Performance | Top speed, acceleration, run time, efficiency |
| Reliability | Thermal soak, vibration, connector and fastener inspection |
| Usability | Can the builder operate and diagnose it from the dashboard and logs? |

## Deliverables

- Test notes and results for each integration rung.
- A short demo recording or log for the portfolio.
- An updated architecture, interface notes, and a list of placeholders still to replace.

## Spend

MVP kart parts are roughly $700 to $1,350. They include a used frame, a placeholder motor and controller, pack, contactor, fuses, and wiring. See [PROJECT.md](../project/PROJECT.md#budget-and-purchasing).

## Risks and hazards

RSK-002, RSK-003, RSK-005, RSK-006, and RSK-007 apply. See the [register](../subsystems/SUBSYSTEMS.md#seed-hazard-and-risk-register).

## Decisions to make

| Decision | Type |
| --- | --- |
| Final kart MVP definition | Builder decision |
| Which subsystems use commercial placeholders | Builder decision |
| Field test location | Builder decision |
| Field test speed limit | Builder decision |
| Which placeholder to replace first | Builder decision |

## Checkpoint questions

Answer the [kart MVP checkpoint](../project/PROJECT.md#checkpoints) questions in the journal.

## Out of scope

- Road use, certification, or high speed.
- Replacing more than one placeholder at a time.

## Open items

| # | Open item | Owner |
| --- | --- | --- |
| 1 | Confirm the kart MVP definition | Builder decision |
| 2 | Field test location and local rules | Builder decision |
| 3 | Field test speed limit value | Builder decision |
