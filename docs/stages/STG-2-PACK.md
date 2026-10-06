---
id: STG-2-PACK
title: "Stage 2: PACK subsystem cycle"
status: draft
owner: Braden Toone (builder)
last_updated: 2026-10-06
subsystem: SUB-PACK
spark: part of Spark
source_sections: [7, 8, 9, 10, 12, 13, 17]
---

# STG-2-PACK: Battery pack, BMS, and power distribution cycle

## Purpose

This cycle takes PACK from a learning burst to an isolated bench pack. The bench pack switches a load safely and trips on injected faults. PACK is second in the recommended order, because it has the most important interaction with DRV.

Power distribution (main fuse, contactors, precharge) is part of this cycle, because it is physically part of the pack.

## Inputs

- [Subsystem cycle template](../project/PROJECT.md#subsystem-cycle)
- [PACK subsystem definition](../subsystems/SUBSYSTEMS.md#pack-battery-pack-bms-and-power-distribution)
- [System goals](STG-1-ARCHITECTURE.md#requirements) and the Stage 1 sizing model v0
- DRV's current and energy needs from [STG-2-DRV](STG-2-DRV.md)
- [Safety approach](../project/PROJECT.md#safety-approach)

**Neighbors to review.** No subsystem is defined in isolation. This cycle reviews these interfaces and feeds changes back.

| Neighbor | What to review |
| --- | --- |
| [DRV](../subsystems/SUBSYSTEMS.md#drv-motor-and-drive) | Current and energy needs; nominal pack voltage |
| [VCU](../subsystems/SUBSYSTEMS.md#vcu-vehicle-control-unit) | Pack state messages; the control states the BMS and power path define |
| [CHS](../subsystems/SUBSYSTEMS.md#chs-chassis-and-mechanical) | Pack mount points and enclosure |
| [NET](../subsystems/SUBSYSTEMS.md#net-network-and-harness) | Message needs, connectors, and harness |

## Goals

- Build working vocabulary in cells, BMS design, and the pack power path.
- Prove on paper that the pack, precharge, fusing, and E-stop loop hold together.
- Show a bench pack that starts up safely and trips on injected faults.

## Requirements

Values are TBD unless the builder fixed them.

| ID | Requirement | Target | How to check | Source |
| --- | --- | --- | --- | --- |
| REQ-PACK-001 | Below the voltage ceiling at full charge (system goal) | Per [STG-1](STG-1-ARCHITECTURE.md#requirements) (below 60 V DC, fixed) | Measurement | Section 7 |
| REQ-PACK-002 | Protects cells and disconnects safely on faults (system goal) | Per [STG-1](STG-1-ARCHITECTURE.md#requirements); fault list defined in this cycle | Fault-injection test | Section 7 |
| REQ-SAF-001 | Hardware E-stop removes traction power (system goal, proposed owner PACK) | Per [STG-1](STG-1-ARCHITECTURE.md#requirements) | Test and inspection | Section 7 |
| REQ-SYS-002 | Useful run time (system goal) | Per [STG-1](STG-1-ARCHITECTURE.md#requirements) | Test | Section 7 |
| REQ-SYS-004 | Power and energy sized for speed, load, and run time (system goal, shared with DRV) | Per [STG-1](STG-1-ARCHITECTURE.md#requirements) | Analysis and test | Section 7 |
| REQ-PACK-003 | The BMS monitors and balances the cells. | TBD | Test | Section 8 responsibilities |
| REQ-PACK-004 | The BMS estimates state of charge. | TBD | Test against logged data | Section 8 responsibilities |
| REQ-PACK-005 | The BMS has authority over the contactors and precharge. | Ownership only; design TBD | Inspection and test | Section 8 boundaries |
| REQ-PACK-006 | Precharge completes before the main contactor closes. | TBD | Functional test | Sections 8, 10 |
| REQ-PACK-007 | A main fuse protects the pack. | TBD | Inspection | Section 8 responsibilities |
| REQ-PACK-008 | The mechanical E-stop loop works independently of software. | Hardware path only | Test | Section 8 boundaries |
| REQ-PACK-009 | HVIL and IMD are included only if determined necessary below 60 V DC. | TBD | Analysis | Section 8 responsibilities |
| REQ-PACK-010 | The pack reports its state to VCU over the shared network. | TBD | Test | Section 8 boundaries |

## Tasks

### Step 1: Learning burst (3 to 7 days, free)

- [ ] Study Li-ion and LiFePO4 basics, cell limits, and balancing.
- [ ] Study equivalent-circuit models and state of charge estimation.
- [ ] Read BMS front-end datasheets.
- [ ] Study fusing, wire sizing, contactors, and precharge.
- [ ] Study E-stop loops, and whether HVIL or IMD is needed below 60 V DC.
- [ ] Keep a "what I still don't understand" list.

### Step 2: Needs and MVP sketch (1 to 2 days, free)

- [ ] Write a one-page needs sketch: what PACK must do, key numbers, interfaces to neighbors, and safety concerns.
- [ ] Note PACK's safe state, failure behavior, and which protections live in hardware.
- [ ] Draft the fault list for REQ-PACK-002.
- [ ] Confirm or change the draft subsystem MVP below.

Draft subsystem MVP (proposed, builder to confirm):

| Item | Draft |
| --- | --- |
| Prototype | PRT-PACK-01: an isolated bench pack of a few series cells at low voltage |
| Setup | BMS logic controls a contactor or relay into a resistive or lamp load. No motor. |
| Test | TST-PACK-001 |
| Pass or fail criterion | Pass if precharge and safety checks run before the load is connected, and each injected fault trips the pack. The mechanical E-stop loop must also open the power path without software. Fault list and thresholds TBD. |

### Step 3: Concepts (1 to 3 days, free)

- [ ] Sketch two or three pack source options and compare them informally. Weigh learning value, cost, and fit.
- [ ] Sketch BMS options as buy, adapt open source, or build.
- [ ] Treat safety as a pass or fail screen.
- [ ] Log the choice and the rejected options in the decision log.

Concept scoring is left blank on purpose.

| ID | Concept | Learning value | Cost | Fit | Safety screen |
| --- | --- | --- | --- | --- | --- |
| CON-PACK-A | Li-ion cells assembled by the builder (current preference) | | | | |
| CON-PACK-B | LiFePO4 | | | | |
| CON-PACK-C | Commercial pack with its own BMS | | | | |

### Step 4: Paper proof of concept (1 to 2 weeks, free)

- [ ] Size the pack for DRV's current and energy needs.
- [ ] Fit a cell model to public data in Python.
- [ ] Calculate precharge time and resistor ratings.
- [ ] Size fuses and wires.
- [ ] Draw the BMS-controlled start-up sequence and E-stop loop in KiCad.
- [ ] Decide on paper whether HVIL or IMD is needed.
- [ ] Draft PACK message needs and hand them to NET.
- [ ] Start a short FMEA, since PACK is safety-relevant.

### Step 5: Spend checkpoint (an hour, free)

- [ ] Answer the [spend checkpoint](../project/PROJECT.md#checkpoints) questions.
- [ ] Write down the one question the purchase answers.
- [ ] Confirm workspace and personal safety spend, including ventilation, is done before any lithium work.
- [ ] Decide go, adjust, or park.

### Step 6: Subsystem MVP (2 to 6 weeks)

- [ ] Confirm the charging and storage area and the fire response plan are ready.
- [ ] Decide how to meet the "never work alone on the battery" rule.
- [ ] Buy cells, fuses, and contactors new, and log each purchase with the PACK code.
- [ ] Build PRT-PACK-01 and run TST-PACK-001.
- [ ] Judge the result against the pass or fail criterion.

### Step 7: Fold-back (1 to 2 days, free)

- [ ] Answer the [fold-back checkpoint](../project/PROJECT.md#checkpoints) questions.
- [ ] Update the system goals, interfaces, and hazard list.
- [ ] Feed interface changes back to DRV, VCU, CHS, and NET.
- [ ] Do the enjoyment check. Completing this cycle after DRV reaches Spark, so decide whether to continue.
- [ ] Write a short process retrospective.

## Deliverables

- Journal entries and a one-page needs sketch, including the fault list.
- Paper proof of concept notes: pack sizing, cell model, precharge, fuse and wire sizing, and the start-up and E-stop schematic.
- Concept comparison and logged decision.
- Bench results for TST-PACK-001.
- Updated goals, interfaces, hazard list, and budget tracker.

## Spend

Steps 1 to 5 are free. The rough first spend is $100 to $250. Workspace and personal safety spend is budgeted separately in [PROJECT.md](../project/PROJECT.md#budget-and-purchasing).

The upper end can exceed one month's budget. Decide at the spend checkpoint whether rollover covers it.

## Risks and hazards

RSK-001 (lithium fire), RSK-003 (short circuit or arc), and RSK-004 (ventilation) apply. See the [register](../subsystems/SUBSYSTEMS.md#seed-hazard-and-risk-register).

## Decisions to make

| Decision | Shared with |
| --- | --- |
| Nominal pack voltage | DRV |
| Cell chemistry and pack source | None |
| Charging approach | None |
| Whether HVIL or IMD is needed | None |
| How to meet the "never work alone on the battery" rule | Project-wide |

## Checkpoint questions

Use the spend and fold-back questions in [PROJECT.md](../project/PROJECT.md#checkpoints). PACK adds:

- Does the fully charged pack stay below 60 V DC?
- Did every injected fault on the list trip the pack?
- Is the workspace safe for lithium charging and storage?

## Out of scope

- A builder-designed charger, unless chosen in the charging decision.
- Final pack mounting on a frame. That belongs to CHS and STG-3.
- A separate power distribution or thermal subsystem.

## Open items

| # | Open item | Owner |
| --- | --- | --- |
| 1 | Targets for REQ-PACK-003 to REQ-PACK-010 | Builder decision |
| 2 | Fault list for REQ-PACK-002 and TST-PACK-001 | PACK cycle |
| 3 | Number of series cells for the bench pack | Builder decision |
| 4 | Workspace ventilation and charging area | Builder decision |
| 5 | PACK message content on the bus | PACK cycle, with NET |
