---
id: STG-2-TEL
title: "Stage 2: TEL subsystem cycle"
status: draft
owner: Braden Toone (builder)
last_updated: 2026-10-06
subsystem: SUB-TEL
spark: not yet decided
source_sections: [8, 9, 10, 13]
---

# STG-2-TEL: Telemetry and apps cycle

## Purpose

This cycle builds a logger and web dashboard, first on simulated data and then on live CAN data. TEL is the hub for monitoring, debugging, and validation.

## Inputs

- [Subsystem cycle template](../project/PROJECT.md#subsystem-cycle)
- [TEL subsystem definition](../subsystems/SUBSYSTEMS.md#tel-telemetry-and-apps)
- [System goals](STG-1-ARCHITECTURE.md#requirements)
- The DBC from [STG-2-NET](STG-2-NET.md), as far as it exists

**Neighbors to review.** No subsystem is defined in isolation. This cycle reviews these interfaces and feeds changes back.

| Neighbor | What to review |
| --- | --- |
| [NET](../subsystems/SUBSYSTEMS.md#net-network-and-harness) | DBC as the data contract; CAN hardware for live data |
| [VCU](../subsystems/SUBSYSTEMS.md#vcu-vehicle-control-unit) | Status and fault reports; dashboard decision |
| [PACK](../subsystems/SUBSYSTEMS.md#pack-battery-pack-bms-and-power-distribution), [DRV](../subsystems/SUBSYSTEMS.md#drv-motor-and-drive) | Data they publish on the bus |

## Goals

- Build working vocabulary in CAN logging, data formats, and simple web dashboards.
- Define a data schema and dashboard views.
- Show simulated, then live, CAN data on a dashboard with a debug view.

## Requirements

No section 7 system goal is tagged to TEL yet. Values are TBD.

| ID | Requirement | Target | How to check | Source |
| --- | --- | --- | --- | --- |
| REQ-TEL-001 | TEL logs data from the CAN bus. | TBD | Test | Section 8 responsibilities |
| REQ-TEL-002 | TEL shows detailed and debug information on a web or mobile dashboard. | TBD | Demo | Section 8 responsibilities |
| REQ-TEL-003 | TEL supports analysis of logged data in Python. | TBD | Demo | Section 8 responsibilities |
| REQ-TEL-004 | TEL listens on the bus without control authority. | Listen only | Inspection | Section 8 boundaries |

## Tasks

### Step 1: Learning burst (3 to 7 days, free)

- [ ] Study CAN logging and data formats.
- [ ] Study WebSocket or MQTT, or another way to move live data.
- [ ] Study simple web dashboards.
- [ ] Review Python analysis of logged data.
- [ ] Keep a "what I still don't understand" list.

### Step 2: Needs and MVP sketch (1 to 2 days, free)

- [ ] Write a one-page needs sketch: what TEL must do, key numbers, interfaces to neighbors, and safety concerns.
- [ ] Note TEL's failure behavior. TEL failing must not affect driving.
- [ ] Confirm or change the draft subsystem MVP below.

Draft subsystem MVP (proposed, builder to confirm):

| Item | Draft |
| --- | --- |
| Prototype | PRT-TEL-01: a logger and web dashboard |
| Setup | Simulated CAN data first, then live CAN data |
| Test | TST-TEL-001 |
| Pass or fail criterion | Pass if the dashboard and debug view show simulated data and then live CAN data, and the log can be analyzed in Python. Data rates TBD. |

### Step 3: Concepts (1 to 3 days, free)

- [ ] Sketch two or three options (buy, adapt open source, build) and compare them informally. Weigh learning value, cost, and fit.
- [ ] Treat safety as a pass or fail screen.
- [ ] Log the choice and the rejected options in the decision log.

Concept scoring is left blank on purpose. The rows are the dashboard options from the launch document.

| ID | Concept | Learning value | Cost | Fit | Safety screen |
| --- | --- | --- | --- | --- | --- |
| CON-TEL-A | LEDs only | | | | |
| CON-TEL-B | A small embedded display | | | | |
| CON-TEL-C | A phone or laptop web app | | | | |

### Step 4: Paper proof of concept (1 to 2 weeks, free)

- [ ] Mock up the dashboard and debug views.
- [ ] Define a data schema.
- [ ] Test the mock-up on simulated data.

### Step 5: Spend checkpoint (an hour, free)

- [ ] Answer the [spend checkpoint](../project/PROJECT.md#checkpoints) questions.
- [ ] Decide whether a software-only start is enough for now.
- [ ] Decide go, adjust, or park.

### Step 6: Subsystem MVP (2 to 6 weeks)

- [ ] Build the logger and dashboard on simulated data.
- [ ] Buy any hardware needed for live data, and log each purchase with the TEL code.
- [ ] Run TST-TEL-001 and judge the result against the pass or fail criterion.

### Step 7: Fold-back (1 to 2 days, free)

- [ ] Answer the [fold-back checkpoint](../project/PROJECT.md#checkpoints) questions.
- [ ] Update the system goals, interfaces, and hazard list.
- [ ] Feed schema and message changes back to NET and VCU.
- [ ] Do the enjoyment check, and choose the next subsystem.
- [ ] Write a short process retrospective.

## Deliverables

- Journal entries and a one-page needs sketch.
- Dashboard mock-ups and a data schema.
- Concept comparison and logged decision.
- A working logger and dashboard, with TST-TEL-001 results.
- Updated goals, interfaces, hazard list, and budget tracker.

## Spend

Steps 1 to 5 are free. The rough first spend is $10 to $30, and a software-only start is free. See [PROJECT.md](../project/PROJECT.md#budget-and-purchasing).

## Risks and hazards

No seed risk applies directly to TEL. Review the [register](../subsystems/SUBSYSTEMS.md#seed-hazard-and-risk-register) at fold-back.

## Decisions to make

| Decision | Shared with |
| --- | --- |
| Dashboard approach | VCU |
| Live data transport | NET |

## Checkpoint questions

Use the spend and fold-back questions in [PROJECT.md](../project/PROJECT.md#checkpoints). TEL adds:

- Can the builder diagnose a fault from the dashboard and logs alone?

## Out of scope

- Control authority of any kind.
- A configuration app. That is a later target in the skills table.

## Open items

| # | Open item | Owner |
| --- | --- | --- |
| 1 | Targets for REQ-TEL-001 to REQ-TEL-003 | Builder decision |
| 2 | Whether TEL needs a section 7 system goal | Builder decision |
| 3 | CAN hardware for live data, shared with NET | TEL with NET |
| 4 | Whether TEL is part of Spark | Builder decision |
