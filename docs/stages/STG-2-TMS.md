---
id: STG-2-TMS
title: "Stage 2: TMS subsystem cycle (optional)"
status: draft
owner: Braden Toone (builder)
last_updated: 2026-10-06
subsystem: SUB-TMS
optional: true
spark: not yet decided
source_sections: [8, 10, 13]
---

# STG-2-TMS: Thermal management cycle (optional)

This is a stub. TMS becomes a subsystem only if monitoring in PACK and DRV shows it is needed. Until then, its work happens inside the PACK and VCU cycles.

## Purpose

Decide whether passive cooling plus a derate strategy is enough, and build more only if it is not.

## Inputs

- [Subsystem cycle template](../project/PROJECT.md#subsystem-cycle)
- [TMS subsystem definition](../subsystems/SUBSYSTEMS.md#tms-thermal-management-optional)
- The sizing model from [STG-1](STG-1-ARCHITECTURE.md) and the cell model from [STG-2-PACK](STG-2-PACK.md)

**Neighbors to review:** PACK and DRV (monitoring), VCU (derating).

## Goals

- Know whether passive cooling is enough.

## Requirements

| ID | Requirement | Target | How to check | Source |
| --- | --- | --- | --- | --- |
| REQ-TMS-001 | Temperatures stay within cell and motor limits, using passive cooling and derating. | TBD | Test and analysis | Sections 8, 10 |

## Tasks

- [ ] Step 1, learning burst: cell and motor thermal limits, derating curves, simple temperature sensing.
- [ ] Step 2, needs and MVP sketch: draft MVP is monitoring and derate logic inside the PACK and VCU MVPs. Pass or fail criterion TBD (proposed, builder to confirm).
- [ ] Step 3, concepts: passive cooling plus derating versus active cooling. Scoring left blank.
- [ ] Step 4, paper proof of concept: estimate heating from the sizing and cell models.
- [ ] Step 5, spend checkpoint: decide whether a separate subsystem is needed.
- [ ] Step 6, subsystem MVP: only if step 5 says so.
- [ ] Step 7, fold-back: update goals, interfaces, and hazards.

## Deliverables

- A heating estimate and a written decision on whether TMS is needed.

## Spend

Rough first spend: $0 to $30.

## Risks and hazards

RSK-001 (lithium fire) is related. See the [register](../subsystems/SUBSYSTEMS.md#seed-hazard-and-risk-register).

## Decisions to make

- Whether TMS becomes a separate subsystem.

## Checkpoint questions

Use the spend and fold-back questions in [PROJECT.md](../project/PROJECT.md#checkpoints).

## Out of scope

- Any work before the core subsystems are done, apart from monitoring inside PACK, DRV, and VCU.

## Open items

| # | Open item | Owner |
| --- | --- | --- |
| 1 | Target for REQ-TMS-001 | Builder decision |
