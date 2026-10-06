---
id: STG-1
title: "Stage 1: Architecture"
status: draft
owner: Braden Toone (builder)
last_updated: 2026-10-06
source_sections: [5, 6, 7, 8, 13, 17]
---

# STG-1: Architecture

## Purpose

Stage 1 is a short, free, high-level pass that runs once, over about 3 weeks. It sets up tools, gathers rough numbers, defines the system requirements, and splits the kart into subsystems. Nothing is bought.

Stage 1 is where the system requirements (weight, speeds, power, energy, run time, and so on) get defined. This document lists them as tasks and open items, not values.

## Inputs

- [Charter and current aim](../project/PROJECT.md#charter)
- [Constraints](../project/PROJECT.md#constraints) and [repository strategy](../project/PROJECT.md#repository-strategy)
- [Builder answers](../project/PROJECT.md#builder-answers), including the starting inputs for driver mass, kart mass, and top speed
- [Safety approach](../project/PROJECT.md#safety-approach)
- [Architecture overview](../subsystems/SUBSYSTEMS.md#architecture-overview) and [subsystem summary](../subsystems/SUBSYSTEMS.md#subsystem-summary)
- [Seed hazard and risk register](../subsystems/SUBSYSTEMS.md#seed-hazard-and-risk-register)

## Goals

- Be able to learn, simulate, and take notes on a computer from day one.
- Get rough numbers for power, pack voltage, and energy, and a short hazard list.
- Write system goals loose enough to change, so every subsystem has something to aim at.
- Split the kart into subsystems with rough interfaces, define the kart MVP, and choose where to start.

## Requirements

This table is the single home of the system goals from launch section 7. Other documents reference them by ID. Every value the builder did not fix is TBD.

| ID | Requirement | Target | How to check | Source |
| --- | --- | --- | --- | --- |
| REQ-SYS-001 | The kart reaches a useful top speed on level pavement. | TBD, defined in Stage 1. Starting input: about 30 mph. | GPS test | Section 7, builder answer |
| REQ-SYS-002 | The kart runs long enough for a useful session. | TBD, defined in Stage 1. | Test | Section 7 |
| REQ-SYS-003 | The kart carries its design load, driver plus kart. | TBD, defined in Stage 1. Starting inputs: about 300 lb driver, about 200 lb kart. | Test and analysis | Section 7, builder answer |
| REQ-SYS-004 | Power and energy are sized for the speed, load, and run time above. | TBD, defined in Stage 1 from the sizing model. | Analysis and test | Section 7 |
| REQ-PACK-001 | The battery stays below the shock-hazard voltage ceiling at full charge. | Below 60 V DC (fixed constraint) | Measurement | Section 7, section 3 |
| REQ-PACK-002 | The battery system protects its cells and disconnects safely on faults. | TBD, fault list defined in the PACK cycle. | Fault-injection test | Section 7 |
| REQ-SAF-001 | An emergency stop removes traction power independent of software. | Hardware path only | Test and inspection | Section 7 |
| REQ-VCU-001 | A single sensor or software fault cannot command unintended acceleration. | TBD, fault behavior defined in the VCU cycle. | Fault-injection test | Section 7 |
| REQ-NET-001 | Subsystems communicate over a shared network. | TBD, protocol and rates defined during subsystem work. | Test | Section 7 |
| REQ-COST-001 | Spend stays within the budget plan. | $150 per month, rollover allowed (fixed constraint) | Budget tracker | Section 7, section 13 |

These are illustrative goal themes, not specifications. Stage 1 may change, add, or drop goals. The suggested final list is 10 to 15 goals. Proposed subsystem tags are in [SUBSYSTEMS.md](../subsystems/SUBSYSTEMS.md#system-goal-tags).

## Tasks

Tasks are recommended, not mandatory. Skip or shorten any that are not helping, and note why in the journal.

### 1a. Setup (a few days, free)

- [ ] Confirm or correct the [assumptions](../project/PROJECT.md#assumptions) and answer the [flagged contradictions](../project/PROJECT.md#gaps-and-contradictions-in-the-launch-document).
- [ ] Ask the orchestration LLM to generate the [starter tracking set](../project/PROJECT.md#tracking-artifacts-to-create-later) (rows 1 to 10).
- [ ] Create the main GitHub repository for documentation and planning. Add submodules later, when each atomic piece starts.
- [ ] Install free or open-source tools as they become useful. Examples are KiCad with ngspice, FreeCAD or an Onshape free tier, and Python with Jupyter.
- [ ] Leave embedded toolchains until the first physical iteration.
- [ ] Start the journal and the decision log, even as plain text files.
- [ ] Sketch a workspace safety plan on paper: where cells are charged and stored, ventilation, and fire response. Buy nothing yet.
- [ ] Start an empty tool shopping list.
- [ ] Done when the builder can open KiCad, run a Python notebook, and commit a journal entry.

### 1b. System-level research (about 1 week)

Spend roughly 3 to 4 hours on each stream. Finish each with a short note on what it means for JoyRide.

- [ ] Reference builds: what do successful DIY electric karts and small EVs use for frame, motor, voltage, and battery? What went wrong for others? Output: benchmark table of 3 to 5 builds.
- [ ] Drivetrain sizing: what power, voltage, gearing, and energy give a useful top speed and run time for the starting inputs? Output: Python sizing model v0.
- [ ] Safety basics: what are the main hazards below 60 V DC, and which protections matter most? Output: seed hazard list.
- [ ] Open-source landscape: which open projects exist for motor control, battery management, CAN tools, and dashboards? Output: link list per subsystem, names only.
- [ ] Defer silicon choices, cell chemistry, frames, and local rules to the subsystem cycle that needs them.
- [ ] Done when there are rough numbers for power, pack voltage, and energy, plus a short hazard list.

### 1c. System goals (3 to 4 days)

- [ ] List 8 to 12 plain "I want..." statements covering driving, learning, safety, and cost. Mark each must-have or nice-to-have.
- [ ] Define the system requirements from the sizing model: design mass, top speed, run time, power, and energy.
- [ ] Turn the wants into 10 to 15 system goals, each with a target, a minimum, and, if useful, how it is checked.
- [ ] Tag each goal with its most responsible subsystem. Confirm or change the [proposed tags](../subsystems/SUBSYSTEMS.md#system-goal-tags).
- [ ] Assign owners for REQ-SAF-001 and REQ-COST-001, which use non-subsystem codes.
- [ ] Done when the builder is happy the goals describe the kart they want. They do not need to be perfect.

### 1d. Architecture and subsystem definition (about 1 week)

- [ ] Functional decomposition: list what the kart must do and map each function to a subsystem. Functions are store energy, distribute and protect power, convert power, read driver intent, stop safely, communicate, inform the driver, and carry loads.
- [ ] Confirm the architecture style: one central VCU plus CAN nodes, with a gateway to wireless. Three to five nodes is plenty to start.
- [ ] Write safety concept v0. Define the overall safe state (traction power off) and the hardware path that reaches it. Each subsystem will document its own safe state and failure behavior.
- [ ] Sketch interfaces for each pair of subsystems that touch: power, data, mechanical, and human. Formalize them only when it helps.
- [ ] Optionally start a DBC skeleton with rough CAN message ideas.
- [ ] Estimate a rough cost per subsystem, so spending stays a choice.
- [ ] Define the kart MVP and decide which subsystems may be commercial placeholders. See [STG-3](STG-3-INTEGRATION.md#the-kart-mvp).
- [ ] Choose the starting subsystem. The recommended order starts with [DRV](STG-2-DRV.md).
- [ ] Update the hazard list.
- [ ] Hold the architecture checkpoint.

## Deliverables

| Deliverable | Task group |
| --- | --- |
| Repository, journal, decision log, and an empty shopping list | 1a |
| A one-paragraph workspace safety note | 1a |
| Benchmark table, sizing model v0, seed hazard list, open-source link list | 1b |
| A plain-language wants list and a goals list with a subsystem tag on each goal | 1c |
| Architecture diagram and a subsystem list with a one-line responsibility each | 1d |
| Rough interface sketches and an optional DBC skeleton | 1d |
| Safety concept v0 and an updated hazard list | 1d |
| Rough cost per subsystem | 1d |
| The kart MVP definition and the chosen starting subsystem | 1d |

## Spend

Stage 1 costs $0. Nothing is bought. See [Budget and purchasing](../project/PROJECT.md#budget-and-purchasing).

## Risks and hazards

The relevant seed risks are RSK-004 (ventilation), RSK-008 (budget overrun), and RSK-009 (lost interest). Stage 1 also produces the first full hazard list. See the [register](../subsystems/SUBSYSTEMS.md#seed-hazard-and-risk-register).

## Decisions to make

| Decision | Type |
| --- | --- |
| System requirement values (design mass, top speed, run time, power, energy) | Builder decision |
| Subsystem tags for each goal | Builder decision |
| Kart MVP definition and which subsystems may be placeholders | Builder decision |
| Starting subsystem | Builder decision |
| Workspace safety plan, including ventilation | Builder decision |
| How to handle the "never work alone on the battery" rule | Builder decision |

## Checkpoint questions

Answer the [architecture checkpoint](../project/PROJECT.md#checkpoints) questions in the journal. Stage 1 also asks:

- Do the sizing numbers fit below the 60 V DC ceiling?
- Is the workspace safety plan good enough to start the first physical iteration later?

## Out of scope

- Buying anything.
- Detailed research on silicon choices, cell chemistry, frames, and local rules.
- Formal interface definitions, unless they help.
- Creating Git submodules before the work that needs them starts.

## Open items

| # | Open item | Owner |
| --- | --- | --- |
| 1 | Values for REQ-SYS-001 to REQ-SYS-004 | Builder decision |
| 2 | Additional system goals to reach 10 to 15 | Builder decision |
| 3 | Owners for REQ-SAF-001 and REQ-COST-001 | Builder decision |
| 4 | Workspace ventilation and charging area | Builder decision |
| 5 | Run time definition for a "useful session" | Builder decision |
| 6 | Whether learning bursts for DRV and PACK overlap Stage 1, given "one cycle at a time" | Builder decision |
