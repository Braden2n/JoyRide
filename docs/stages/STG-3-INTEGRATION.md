---
id: STG-3
status: Not started
updated: 2026-10-06
stage_type: integration
subsystem: none
spark: no
---

# STG-3: Integration and the kart MVP

## Purpose

Connect subsystems as they mature, ending first in a drivable kart, the kart MVP and Bronze evidence. The kart MVP drives at low speed under its own power, with a working E-stop, a protected battery, and controlled throttle. That definition is for the builder to confirm. Placeholders fill any subsystem that has not had its turn.

## Entry and exit

- Entry: at least two subsystems work on the bench.
- Exit for the first milestone: the kart MVP checkpoint is answered. Upgrades continue after that.

## Inputs and neighbors

- Fold-back results from each STG-2 cycle.
- Neighbors: all subsystems. Interfaces are in [SUBSYSTEMS.md](../architecture/SUBSYSTEMS.md#interfaces).

## Goals

- A kart that drives safely at low speed.
- A list of placeholders to replace next.

## System goals served

Verifies REQ-SYS-001 to REQ-SYS-004 and REQ-SAF-001 to REQ-SAF-004 on the kart.

## Tasks

### Integration ladder

Move up a rung when the previous one feels solid.

1. [ ] Bench: two subsystems at a time on a current-limited supply, with CAN traffic logged.
2. [ ] Rig: the full electrical system on the kart, drive wheels off the ground, E-stop within reach.
3. [ ] Low-speed field test: a clear private area, a helmet, and a speed limit in the VCU or controller.
4. [ ] Performance: speed, acceleration, range, and thermal behavior, with data logged.
5. [ ] Endurance: repeated runs, inspection after each, and a data review in Python.

### Before the kart moves

- [ ] Create the root TST-SYS test folder.
- [ ] Buy kart MVP parts, funded by rollover.
- [ ] Confirm each subsystem on the kart meets its safety basics.
- [ ] Test the E-stop and the BMS cutoffs at every rung.

### Refinement and upgrades

- [ ] Turn every failed test into a cause and a fix, or a DEC to accept it.
- [ ] Update the architecture, interfaces, and goals after each test campaign.
- [ ] Replace placeholders one at a time, as drop-in replacements in form, fit, and function.

Test types to plan for:

| Type | Examples |
| --- | --- |
| Electrical | Continuity, insulation, voltage drop, load and temperature rise |
| Functional | Start-up sequence, state transitions, driving modes |
| Fault injection | Cell limit trips, E-stop, sensor disconnect, CAN loss, stuck throttle |
| Performance | Top speed, acceleration, run time, efficiency |
| Reliability | Thermal soak, vibration, connector and fastener inspection |
| Usability | Operating and diagnosing from the dashboard and logs |

## Deliverables

- A TST-SYS report for each rung.
- A short demo recording or log for the portfolio.
- An updated architecture and a placeholder replacement list.

## Spend

$700 to $1,350 for kart MVP parts: a used frame, a placeholder motor and controller, pack, contactor, fuses, and wiring.

## Risks

RSK-002, RSK-003, RSK-005, RSK-006, RSK-007.

## Decisions

| Decision | Shared with | DEC |
| --- | --- | --- |
| Final kart MVP definition and placeholders | All | |
| Field test location and speed limit | VCU | |
| Which placeholder to replace first | All | |

## Checkpoint additions

None beyond the kart MVP checkpoint.

## Out of scope

- Road use, certification, or high speed.
- Replacing more than one placeholder at a time.

## Open items

| # | Open item | Owner |
| --- | --- | --- |
| 1 | Field test location and local rules | Builder decision |
