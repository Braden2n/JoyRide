---
id: STG-2-TMS
status: Not started
updated: 2026-10-06
stage_type: cycle
subsystem: TMS
spark: not yet decided
---

# STG-2-TMS: Thermal management (optional)

## Purpose

Decide whether passive cooling plus a derate strategy is enough. Until a need appears, this work happens inside the PACK, DRV, and VCU cycles.

## Entry and exit

- Entry: monitoring in PACK or DRV shows a thermal need, after the core subsystems.
- Exit: the fold-back checkpoint is answered, or the cycle is parked.

## Inputs and neighbors

- The sizing model and the PACK cell model.
- Neighbors: PACK, DRV, VCU. Interfaces are in [SUBSYSTEMS.md](../architecture/SUBSYSTEMS.md#tms-thermal-management-optional).

## Goals

- A written answer on whether TMS is needed.

## System goals served

None yet.

## Tasks

### Step 1: Learning burst

- [ ] Study cell and motor thermal limits, derating curves, and simple temperature sensing.

### Step 2: Needs and MVP sketch

- [ ] Draft MVP: monitoring and derate logic inside the PACK and VCU MVPs. Pass or fail TBD (proposed, builder to confirm).

### Step 3: Concepts

- [ ] Compare passive cooling plus derating with active cooling.

### Step 4: Paper proof of concept

- [ ] Estimate heating from the sizing and cell models.

### Step 5: Spend checkpoint

- [ ] Decide whether a separate subsystem is needed.

### Step 6: Subsystem MVP

- [ ] Only if step 5 says so.

### Step 7: Fold-back

- [ ] Feed changes back to PACK, DRV, VCU, GOALS, and RISKS.

## Deliverables

A heating estimate and a DEC on whether TMS is needed.

## Spend

$0 to $30.

## Risks

RSK-001.

## Decisions

| Decision | Shared with | DEC |
| --- | --- | --- |
| Whether TMS becomes a separate subsystem | PACK, DRV, VCU | |

## Checkpoint additions

None.

## Out of scope

- Any work before the core subsystems are done.

## Open items

None.
