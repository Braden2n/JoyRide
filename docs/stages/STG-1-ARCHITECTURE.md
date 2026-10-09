---
id: STG-1
status: In progress
updated: 2026-10-09
stage_type: system
subsystem: none
spark: yes
---

# STG-1: Architecture

## Purpose

Define the system before any spend. This stage sets up tools, gets rough numbers, sets the system goals, splits the kart into subsystems, and picks the starting point. It is free and takes about 3 weeks.

## Entry and exit

- Entry: project start.
- Exit: the architecture checkpoint is answered in a journal entry.

## Inputs and neighbors

- [Charter, constraints, and assumptions](../project/PROJECT.md)
- [GOALS.md](../project/GOALS.md), [RISKS.md](../project/RISKS.md), and [SUBSYSTEMS.md](../architecture/SUBSYSTEMS.md)
- Neighbors: all subsystems.

## Goals

- Rough numbers for power, pack voltage, and energy.
- System goals with targets, minimums, and owners.
- A subsystem architecture with rough interfaces, a kart MVP definition, and a confirmed starting subsystem.

## System goals served

Sets every system REQ in GOALS.md.

## Tasks

### 1a. Setup (a few days)

- [ ] Confirm or correct the [assumptions](../project/PROJECT.md#assumptions).
- [ ] Install free tools as they become useful, for example KiCad with ngspice, FreeCAD, and Python with Jupyter. Leave embedded toolchains until the first MVP.
- [ ] Write the first journal entry.
- [ ] Sketch the workspace safety plan: charging and storage spot, ventilation, and fire response. Buy nothing yet.
- [ ] Create the week-1 [tracking artifacts](../project/PROJECT.md#tracking-artifacts-to-create).
- [ ] Done when KiCad opens, a Python notebook runs, and a journal entry is committed.

### 1b. System-level research (about 1 week)

Spend about 3 to 4 hours per stream, and end each with a short note on what it means for JoyRide.

- [ ] Reference builds: what 3 to 5 DIY karts and small EVs use for frame, motor, voltage, and battery, and what went wrong.
- [ ] Drivetrain sizing: build Python sizing model v0 for power, voltage, gearing, and energy from the starting inputs in GOALS.md.
- [ ] Safety basics: list the main hazards below 60 V DC and the protections that matter most. Update RISKS.md.
- [ ] Open-source landscape: list open projects for motor control, battery management, CAN tools, and dashboards (names only).
- [ ] Done when there are rough numbers for power, pack voltage, and energy.

### 1c. System goals (3 to 4 days)

- [ ] Write 8 to 12 NEED rows in GOALS.md.
- [ ] Set targets and minimums for REQ-SYS-001 to REQ-SYS-005 from the sizing model: design mass, top speed, run time, power, energy.
- [ ] Grow the list to 10 to 15 system goals, and confirm each owner.
- [ ] Done when the goals describe the kart the builder wants. They do not need to be perfect.

### 1d. Architecture (about 1 week)

- [ ] Map each function to a subsystem. Functions: store energy, distribute and protect power, convert power, read driver intent, stop safely, communicate, inform, carry loads.
- [ ] Confirm the architecture in SUBSYSTEMS.md, including the safe state and its hardware path.
- [ ] Sketch each interface (power, data, mechanical, human) as an ICD row in SUBSYSTEMS.md. Write ICD files only where useful.
- [ ] Optionally start a DBC skeleton.
- [ ] Estimate a rough cost per subsystem.
- [ ] Confirm the kart MVP definition in [STG-3](STG-3-INTEGRATION.md#purpose) and which subsystems may be placeholders.
- [ ] Confirm the starting subsystem ([DEC-005](../decisions/DEC-005-subsystem-order.md)).
- [ ] Hold the architecture checkpoint.

### 1e. Documentation system (runs alongside 1a)

- [x] Write [CLAUDE.md](../../CLAUDE.md).
- [x] Create GOALS.md, RISKS.md, and the decision log.
- [x] Slim PROJECT.md and SUBSYSTEMS.md.
- [x] Create the templates and the task issue form.
- [x] Conform the stage documents to the stage template.
- [x] Dissolve the launch document ([DEC-007](../decisions/DEC-007-dissolve-launch-document.md)).
- [x] Done when every multi-file folder conforms to its template.

## Deliverables

- Journal entries, the workspace safety note, and the tracking artifacts.
- Benchmark table, sizing model v0, and the open-source link list.
- NEED rows and system goals in GOALS.md.
- Architecture, interface sketches, and an optional DBC skeleton.
- Updated RISKS.md, a rough cost per subsystem, and the kart MVP definition.

## Spend

$0. Nothing is bought.

## Risks

RSK-004, RSK-008, RSK-009.

## Decisions

| Decision | Shared with | DEC |
| --- | --- | --- |
| System goal values | All | |
| Kart MVP definition and placeholders | All | |
| Starting subsystem | All | DEC-005 |
| Workspace safety plan | PACK | |
| Subsystem home structure | All | DEC-009 |
| Folder structure for non-subsystem work | All | DEC-010 |
| Definition of a useful session | PACK | DEC-011 (resolved in #11) |

## Checkpoint additions

- Do the sizing numbers fit below 60 V DC?
- Is the workspace safety plan good enough for the first physical iteration?

## Out of scope

- Buying anything.
- Deep research on silicon, cell chemistry, frames, or local rules. Each waits for its cycle.
- Creating subsystem homes or submodules.

## Open items

| # | Open item | Owner |
| --- | --- | --- |
| 1 | Workspace ventilation and charging area. An earlier assumption said a safe lithium workspace exists; the builder says ventilation is poor. | Builder decision |
| 2 | "One cycle at a time" versus starting the DRV and PACK paper proofs in the first weeks | Builder decision |
| 3 | Confirm the TST-SYS code in the [templates](../templates/README.md). Status vocabularies confirmed in #13. | Builder decision |
| 4 | Folder structure for non-subsystem work ([DEC-010](../decisions/DEC-010-non-subsystem-work-structure.md), raised in #12) | Builder decision |
