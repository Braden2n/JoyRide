---
id: STG-2-CHS
title: "Stage 2: CHS subsystem cycle"
status: draft
owner: Braden Toone (builder)
last_updated: 2026-10-06
subsystem: SUB-CHS
spark: not part of Spark
source_sections: [7, 8, 9, 10, 12, 13]
---

# STG-2-CHS: Chassis and mechanical cycle

## Purpose

This cycle lays out where PACK and DRV mount and how mass is distributed, before any frame is bought. CHS is third in the recommended order. It is not part of Spark, but it must be addressed for later levels.

## Inputs

- [Subsystem cycle template](../project/PROJECT.md#subsystem-cycle)
- [CHS subsystem definition](../subsystems/SUBSYSTEMS.md#chs-chassis-and-mechanical)
- [System goals](STG-1-ARCHITECTURE.md#requirements), especially the Stage 1 design mass
- PACK and DRV sizes from [STG-2-PACK](STG-2-PACK.md) and [STG-2-DRV](STG-2-DRV.md)

**Neighbors to review.** No subsystem is defined in isolation. This cycle reviews these interfaces and feeds changes back.

| Neighbor | What to review |
| --- | --- |
| [PACK](../subsystems/SUBSYSTEMS.md#pack-battery-pack-bms-and-power-distribution) | Pack mount points, enclosure, and E-stop placement |
| [DRV](../subsystems/SUBSYSTEMS.md#drv-motor-and-drive) | Motor and gearing mounts, drive wheel connection |
| [VCU](../subsystems/SUBSYSTEMS.md#vcu-vehicle-control-unit) | Node mount and driver controls |
| [NET](../subsystems/SUBSYSTEMS.md#net-network-and-harness) | Harness routing |

## Goals

- Build working vocabulary in kart geometry, steering, braking, and CAD.
- Lay out PACK and DRV on a generic frame envelope.
- Know what to measure before buying a used frame.

## Requirements

Values are TBD unless the builder fixed them.

| ID | Requirement | Target | How to check | Source |
| --- | --- | --- | --- | --- |
| REQ-SYS-003 | Carries the design load, driver plus kart (system goal) | Per [STG-1](STG-1-ARCHITECTURE.md#requirements) | Test and analysis | Section 7 |
| REQ-CHS-001 | Brakes work independently of the electrics. | Mechanical only | Inspection and test | Section 8 boundaries |
| REQ-CHS-002 | The chassis provides mount points for PACK and DRV. | TBD | CAD layout and fit check | Section 8 boundaries |
| REQ-CHS-003 | The chassis provides steering. | TBD | Test | Section 8 responsibilities |
| REQ-CHS-004 | Mass distribution is acceptable at the design mass. | TBD | Analysis | Section 10 |

## Tasks

### Step 1: Learning burst (3 to 7 days, free)

- [ ] Study basic kart geometry.
- [ ] Study steering and braking.
- [ ] Study fasteners and welds.
- [ ] Learn FreeCAD basics, or another free CAD tool.
- [ ] Keep a "what I still don't understand" list.

### Step 2: Needs and MVP sketch (1 to 2 days, free)

- [ ] Write a one-page needs sketch: what CHS must do, key numbers, interfaces to neighbors, and safety concerns.
- [ ] Note the chassis safe state and failure behavior.
- [ ] Confirm or change the draft subsystem MVP below.

Draft subsystem MVP (proposed, builder to confirm):

| Item | Draft |
| --- | --- |
| Prototype | PRT-CHS-01: a CAD layout plus a cardboard mock-up. A printed mock-up needs a 3D printer, which the builder does not own. |
| Setup | PACK and DRV envelopes placed on a generic frame envelope |
| Test | TST-CHS-001 |
| Pass or fail criterion | Pass if PACK and DRV fit the layout with their mount points defined, and mass distribution is estimated. Also pass only if a list of used-frame measurements exists. |

### Step 3: Concepts (1 to 3 days, free)

- [ ] Sketch two or three frame options and compare them informally. Weigh learning value, cost, and fit.
- [ ] Treat safety as a pass or fail screen.
- [ ] Log the choice and the rejected options in the decision log.

Concept scoring is left blank on purpose.

| ID | Concept | Learning value | Cost | Fit | Safety screen |
| --- | --- | --- | --- | --- | --- |
| CON-CHS-A | Used kart frame | | | | |
| CON-CHS-B | Kit frame | | | | |
| CON-CHS-C | Custom welded | | | | |

### Step 4: Paper proof of concept (1 to 2 weeks, free)

- [ ] Lay out PACK and DRV mount locations and enclosures in CAD on a generic frame envelope.
- [ ] Estimate mass distribution at the Stage 1 design mass.
- [ ] Design brackets in CAD.
- [ ] List the measurements to take on a used frame before buying.

### Step 5: Spend checkpoint (an hour, free)

- [ ] Answer the [spend checkpoint](../project/PROJECT.md#checkpoints) questions.
- [ ] Write down the one question the purchase answers.
- [ ] Decide go, adjust, or park.

### Step 6: Subsystem MVP (2 to 6 weeks)

- [ ] Build PRT-CHS-01 and run TST-CHS-001.
- [ ] Measure a used frame before buying one. Buy the frame late, at integration.
- [ ] Judge the result against the pass or fail criterion.

### Step 7: Fold-back (1 to 2 days, free)

- [ ] Answer the [fold-back checkpoint](../project/PROJECT.md#checkpoints) questions.
- [ ] Update the system goals, interfaces, and hazard list.
- [ ] Feed mounting changes back to PACK, DRV, VCU, and NET.
- [ ] Do the enjoyment check, and choose the next subsystem.
- [ ] Write a short process retrospective.

## Deliverables

- Journal entries and a one-page needs sketch.
- CAD layout, bracket designs, and mass distribution estimate.
- Concept comparison and logged decision.
- Mock-up and a used-frame measurement list.
- Updated goals, interfaces, hazard list, and budget tracker.

## Spend

Steps 1 to 5 are free. The rough first spend is $0 to $50. The frame itself is part of MVP kart parts in [PROJECT.md](../project/PROJECT.md#budget-and-purchasing).

## Risks and hazards

RSK-005 (loss of braking) and RSK-006 (structural failure) apply. See the [register](../subsystems/SUBSYSTEMS.md#seed-hazard-and-risk-register).

## Decisions to make

| Decision | Shared with |
| --- | --- |
| Frame | None |
| Mock-up method (cardboard or printed) | None |

## Checkpoint questions

Use the spend and fold-back questions in [PROJECT.md](../project/PROJECT.md#checkpoints). CHS adds:

- Do PACK and DRV fit with room for wiring and service?
- Do the brakes stay independent of the electrics?

## Out of scope

- Buying a frame before integration.
- Spark. CHS is not part of Spark.
- A 3D printer purchase, unless a later cycle justifies it.

## Open items

| # | Open item | Owner |
| --- | --- | --- |
| 1 | Targets for REQ-CHS-002 to REQ-CHS-004 | Builder decision |
| 2 | Pass or fail criterion for TST-CHS-001 | Builder decision |
| 3 | E-stop placement within reach of the driver | CHS with PACK |
