---
id: STG-2-RMT
title: "Stage 2: RMT subsystem cycle (optional)"
status: draft
owner: Braden Toone (builder)
last_updated: 2026-10-06
subsystem: SUB-RMT
optional: true
spark: not yet decided
source_sections: [8, 10, 13]
---

# STG-2-RMT: Remote and wireless cycle (optional)

This is a stub. RMT is a parking-lot idea, considered only after the core subsystems are done.

## Purpose

Explore a remote kill, speed limiting, and wireless configuration, with safe failsafe behavior.

## Inputs

- [Subsystem cycle template](../project/PROJECT.md#subsystem-cycle)
- [RMT subsystem definition](../subsystems/SUBSYSTEMS.md#rmt-remote-and-wireless-optional)

**Neighbors to review:** VCU (speed limiting and torque removal), NET (wireless gateway), PACK (safe state).

## Goals

- Design a remote kill with a failsafe that removes torque.

## Requirements

| ID | Requirement | Target | How to check | Source |
| --- | --- | --- | --- | --- |
| REQ-RMT-001 | Loss of the wireless link fails toward de-energized. | TBD | Failsafe test | Sections 10, 12 |

## Tasks

- [ ] Step 1, learning burst: wireless link basics (ELRS or BLE), failsafe behavior, wireless safety.
- [ ] Step 2, needs and MVP sketch: draft MVP is a wireless link between two dev boards with a failsafe test. Pass or fail criterion TBD (proposed, builder to confirm).
- [ ] Step 3, concepts: two or three link options. Scoring left blank.
- [ ] Step 4, paper proof of concept: design the remote kill concept and its failsafe behavior.
- [ ] Step 5, spend checkpoint: go, adjust, or park.
- [ ] Step 6, subsystem MVP: build the link and run the failsafe test.
- [ ] Step 7, fold-back: update goals, interfaces, and hazards.

## Deliverables

- A remote kill design and failsafe test results.

## Spend

Rough first spend: $30 to $60.

## Risks and hazards

RSK-002 (unintended acceleration) and RSK-007 (injury while driving) are related. See the [register](../subsystems/SUBSYSTEMS.md#seed-hazard-and-risk-register).

## Decisions to make

- Whether to start RMT at all.
- Wireless link type.

## Checkpoint questions

Use the spend and fold-back questions in [PROJECT.md](../project/PROJECT.md#checkpoints).

## Out of scope

- Replacing the hardware E-stop. A remote kill is an addition, not a substitute.

## Open items

| # | Open item | Owner |
| --- | --- | --- |
| 1 | Target for REQ-RMT-001 | Builder decision |
