---
id: STG-2-CHS
status: Not started
updated: 2026-10-06
stage_type: cycle
subsystem: CHS
spark: no
---

# STG-2-CHS: Chassis and mechanical

## Purpose

Lay out where PACK and DRV mount and how the mass is distributed, before buying a frame. CHS is not part of Spark, but later levels need it.

## Entry and exit

- Entry: the PACK fold-back chose CHS.
- Exit: the fold-back checkpoint is answered, or the cycle is parked at the spend checkpoint.

## Inputs and neighbors

- PACK and DRV sizes from their cycles, and the design mass in [GOALS.md](../project/GOALS.md).
- Neighbors: PACK, DRV, VCU, NET. Interfaces are in [SUBSYSTEMS.md](../architecture/SUBSYSTEMS.md#chs-chassis-and-mechanical).

## Goals

- PACK and DRV laid out on a generic frame envelope in CAD.
- A list of what to measure before buying a used frame.

## System goals served

REQ-SYS-003.

## Tasks

### Step 1: Learning burst

- [ ] Study basic kart geometry, steering, and braking.
- [ ] Study fasteners and welds.
- [ ] Learn the basics of a free CAD tool, such as FreeCAD.

### Step 2: Needs and MVP sketch

- [ ] Create `subsystems/CHS/docs/` from the subsystem templates.
- [ ] Write REQUIREMENTS.md, including brakes independent of the electrics.
- [ ] Confirm the draft MVP below.

| MVP | Draft (proposed, builder to confirm) |
| --- | --- |
| Prototype | PRT-CHS-01: a CAD layout plus a cardboard mock-up |
| Test | TST-CHS-001 |
| Pass or fail | PACK and DRV fit with defined mount points, mass distribution is estimated, and a used-frame measurement list exists. |

### Step 3: Concepts

- [ ] Compare a used kart frame, a kit frame, and a custom welded frame.

### Step 4: Paper proof of concept

- [ ] Lay out PACK and DRV mounts and enclosures on a generic frame envelope.
- [ ] Estimate mass distribution at the design mass.
- [ ] Design brackets in CAD.

### Step 5: Spend checkpoint

- [ ] Write the question the purchase answers.

### Step 6: Subsystem MVP

- [ ] Build PRT-CHS-01 and run TST-CHS-001.
- [ ] Measure a used frame before buying one. Buy the frame at integration.

### Step 7: Fold-back

- [ ] Feed mounting changes back to PACK, DRV, VCU, NET, GOALS, and RISKS.

## Deliverables

Standard cycle deliverables, plus the CAD layout and the frame measurement list.

## Spend

$0 to $50. The frame is part of the kart MVP parts budget.

## Risks

RSK-005, RSK-006.

## Decisions

| Decision | Shared with | DEC |
| --- | --- | --- |
| Frame | none | |
| E-stop placement within the driver's reach | PACK | |

## Checkpoint additions

- Do PACK and DRV fit with room for wiring and service?
- Do the brakes stay independent of the electrics?

## Out of scope

- Buying a frame before integration.
- Buying a 3D printer, unless a later cycle justifies it.

## Open items

| # | Open item | Owner |
| --- | --- | --- |
| 1 | A printed mock-up needs a 3D printer, which the builder does not own. Cardboard is the default. | Builder decision |
