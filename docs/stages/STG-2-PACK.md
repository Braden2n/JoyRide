---
id: STG-2-PACK
status: Not started
updated: 2026-10-06
stage_type: cycle
subsystem: PACK
spark: yes
---

# STG-2-PACK: Battery pack, BMS, and power distribution

## Purpose

Prove that a pack, its BMS, and its power path start up safely and trip on faults. Prove it on paper first, then on an isolated bench pack. Power distribution is part of this cycle.

## Entry and exit

- Entry: the DRV fold-back chose PACK.
- Exit: the fold-back checkpoint is answered, or the cycle is parked at the spend checkpoint. Finishing this cycle after DRV reaches Spark.

## Inputs and neighbors

- DRV current and energy needs from [STG-2-DRV](STG-2-DRV.md), and system goals from [GOALS.md](../project/GOALS.md).
- Neighbors: DRV, VCU, CHS, NET. Interfaces are in [SUBSYSTEMS.md](../architecture/SUBSYSTEMS.md#pack-battery-pack-bms-and-power-distribution).

## Goals

- A paper design of pack sizing, precharge, fusing, and the E-stop loop that holds together.
- A bench pack that starts up safely and trips on every injected fault.

## System goals served

REQ-SYS-002, REQ-SYS-004, REQ-SAF-001, REQ-SAF-002, REQ-SAF-003.

## Tasks

### Step 1: Learning burst

- [ ] Study Li-ion and LiFePO4 basics, cell limits, and balancing.
- [ ] Study equivalent-circuit models and state of charge estimation.
- [ ] Read BMS front-end datasheets.
- [ ] Study fusing, wire sizing, contactors, precharge, and E-stop loops.
- [ ] Find out whether HVIL or IMD is needed below 60 V DC.

### Step 2: Needs and MVP sketch

- [ ] Create `subsystems/PACK/docs/` from the subsystem templates.
- [ ] Write REQUIREMENTS.md, including the fault list for REQ-SAF-003.
- [ ] Confirm the draft MVP below.

| MVP | Draft (proposed, builder to confirm) |
| --- | --- |
| Prototype | PRT-PACK-01: a few series cells at low voltage. BMS logic switches a contactor or relay into a resistive or lamp load. No motor. |
| Test | TST-PACK-001 |
| Pass or fail | Precharge and safety checks run before the load connects. Every injected fault on the list trips the pack. The mechanical E-stop opens the power path without software. Thresholds TBD. |

### Step 3: Concepts

- [ ] Compare Li-ion cells assembled by the builder, LiFePO4, and a commercial pack with its own BMS. Settle [DEC-004](../decisions/DEC-004-pack-from-cells.md).
- [ ] Compare BMS options: buy, adapt open source, or build.

### Step 4: Paper proof of concept

- [ ] Size the pack for DRV's current and energy needs.
- [ ] Fit a cell model to public data in Python.
- [ ] Calculate precharge time and resistor ratings, and size fuses and wires.
- [ ] Draw the BMS start-up sequence and E-stop loop in KiCad.
- [ ] Send PACK message needs to NET.
- [ ] Draft the FMEA.

### Step 5: Spend checkpoint

- [ ] Confirm the workspace and personal safety spend, including ventilation, is done before any lithium work.
- [ ] Write the question the purchase answers.

### Step 6: Subsystem MVP

- [ ] Confirm the charging area, storage, and fire response are ready.
- [ ] Buy cells, fuses, and contactors new.
- [ ] Build PRT-PACK-01 and run TST-PACK-001.

### Step 7: Fold-back

- [ ] Feed changes back to DRV, VCU, CHS, NET, GOALS, and RISKS.
- [ ] Decide whether to continue past Spark.

## Deliverables

Standard cycle deliverables, plus the start-up and E-stop schematic.

## Spend

$100 to $250. Workspace and safety spend is separate. The upper end can exceed one month's budget, so check the rollover balance.

## Risks

RSK-001, RSK-003, RSK-004.

## Decisions

| Decision | Shared with | DEC |
| --- | --- | --- |
| Nominal pack voltage | DRV | |
| Cell chemistry and pack source | none | DEC-004 (proposed) |
| Charging approach: commercial or builder-designed charger | none | |
| Whether HVIL or IMD is needed | none | |

## Checkpoint additions

- Does the fully charged pack stay below 60 V DC?
- Did every injected fault on the list trip the pack?
- Is the workspace safe for lithium charging and storage?

## Out of scope

- A builder-designed charger, unless the charging decision chooses one.
- Mounting on a frame (CHS and STG-3).

## Open items

| # | Open item | Owner |
| --- | --- | --- |
| 1 | How to meet "never work alone on the battery" as a solo builder | Builder decision |
| 2 | Number of series cells for the bench pack | Builder decision |
| 3 | Fault list for REQ-SAF-003 | This cycle, step 2 |
