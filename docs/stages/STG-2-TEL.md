---
id: STG-2-TEL
status: Not started
updated: 2026-10-06
stage_type: cycle
subsystem: TEL
spark: not yet decided
---

# STG-2-TEL: Telemetry and apps

## Purpose

Build a logger and web dashboard, first on simulated data and then on live CAN data.

## Entry and exit

- Entry: the VCU fold-back chose TEL.
- Exit: the fold-back checkpoint is answered, or the cycle is parked at the spend checkpoint.

## Inputs and neighbors

- The DBC from NET, as far as it exists.
- Neighbors: NET, VCU, PACK, DRV. Interfaces are in [SUBSYSTEMS.md](../architecture/SUBSYSTEMS.md#tel-telemetry-and-apps).

## Goals

- A data schema and dashboard views.
- A dashboard and debug view on simulated, then live, CAN data.

## System goals served

None yet. TEL may need a system goal.

## Tasks

### Step 1: Learning burst

- [ ] Study CAN logging and data formats.
- [ ] Study a live data transport, such as WebSocket or MQTT.
- [ ] Study simple web dashboards and Python analysis of logs.

### Step 2: Needs and MVP sketch

- [ ] Create `subsystems/TEL/docs/` from the subsystem templates.
- [ ] Write REQUIREMENTS.md. TEL has listen-only authority, and its failure must not affect driving.
- [ ] Confirm the draft MVP below.

| MVP | Draft (proposed, builder to confirm) |
| --- | --- |
| Prototype | PRT-TEL-01: a logger and web dashboard with a debug view |
| Test | TST-TEL-001 |
| Pass or fail | The dashboard shows simulated and then live CAN data, and the log can be analyzed in Python. Data rates TBD. |

### Step 3: Concepts

- [ ] Compare LEDs only, a small embedded display, and a phone or laptop web app.

### Step 4: Paper proof of concept

- [ ] Mock up the dashboard and debug views.
- [ ] Define a data schema, and test it on simulated data.

### Step 5: Spend checkpoint

- [ ] Decide whether a software-only start is enough for now.

### Step 6: Subsystem MVP

- [ ] Build PRT-TEL-01 on simulated data, then on live data, and run TST-TEL-001.

### Step 7: Fold-back

- [ ] Feed schema and message changes back to NET and VCU.

## Deliverables

Standard cycle deliverables, plus the dashboard mock-ups and the data schema.

## Spend

$10 to $30. A software-only start is free.

## Risks

None in the register.

## Decisions

| Decision | Shared with | DEC |
| --- | --- | --- |
| Dashboard approach | VCU | |
| Live data transport | NET | |

## Checkpoint additions

- Can the builder diagnose a fault from the dashboard and logs alone?

## Out of scope

- Any control authority.
- A configuration app (a later skills target).

## Open items

| # | Open item | Owner |
| --- | --- | --- |
| 1 | Whether TEL needs a system goal | Builder decision |
| 2 | CAN hardware for live data, shared with NET | This cycle, with NET |
| 3 | Whether TEL is part of Spark | Builder decision |
