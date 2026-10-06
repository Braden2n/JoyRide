---
id: STG-2-DRV
title: "Stage 2: DRV subsystem cycle"
status: draft
owner: Braden Toone (builder)
last_updated: 2026-10-06
subsystem: SUB-DRV
spark: part of Spark
source_sections: [7, 8, 9, 10, 12, 13]
---

# STG-2-DRV: Motor and drive cycle

## Purpose

This cycle takes DRV from a learning burst to a spinning motor on the bench. DRV is first in the recommended order, because motor and controller selection drives most other subsystem work.

The DRV paper proof of concept doubles as a go or no-go check on the system goals. If DRV cannot meet them, the rest of the system probably cannot either.

## Inputs

- [Subsystem cycle template](../project/PROJECT.md#subsystem-cycle)
- [DRV subsystem definition](../subsystems/SUBSYSTEMS.md#drv-motor-and-drive)
- [System goals](STG-1-ARCHITECTURE.md#requirements) and the Stage 1 sizing model v0
- [Safety approach](../project/PROJECT.md#safety-approach)

**Neighbors to review.** No subsystem is defined in isolation. This cycle reviews these interfaces and feeds changes back.

| Neighbor | What to review |
| --- | --- |
| [PACK](../subsystems/SUBSYSTEMS.md#pack-battery-pack-bms-and-power-distribution) | Pack voltage and current compatibility; traction power through the contactors |
| [VCU](../subsystems/SUBSYSTEMS.md#vcu-vehicle-control-unit) | Torque requests and DRV status; derate inputs |
| [CHS](../subsystems/SUBSYSTEMS.md#chs-chassis-and-mechanical) | Motor and gearing mounts |
| [NET](../subsystems/SUBSYSTEMS.md#net-network-and-harness) | Message needs for the DBC |

## Goals

- Build working vocabulary in motor and drive fundamentals.
- Make a go or no-go call on the system goals.
- Spin a motor safely at low voltage with logged speed and current.

## Requirements

Values are TBD unless the builder fixed them.

| ID | Requirement | Target | How to check | Source |
| --- | --- | --- | --- | --- |
| REQ-SYS-001 | Useful top speed (system goal) | Per [STG-1](STG-1-ARCHITECTURE.md#requirements) | GPS test | Section 7 |
| REQ-SYS-004 | Power and energy sized for speed, load, and run time (system goal, shared with PACK) | Per [STG-1](STG-1-ARCHITECTURE.md#requirements) | Analysis and test | Section 7 |
| REQ-DRV-001 | DRV converts electrical power from PACK into torque at the drive wheels. | TBD | Analysis and test | Section 8 responsibilities |
| REQ-DRV-002 | DRV takes torque requests from VCU over the shared network. | TBD | Test | Section 8 boundaries |
| REQ-DRV-003 | DRV receives traction power only through the PACK contactors. | Hardware path | Inspection | Section 8 boundaries |
| REQ-DRV-004 | DRV removes torque on a lost signal, lost heartbeat, or watchdog trip. | TBD | Fault-injection test | Section 12 principles |
| REQ-DRV-005 | DRV is compatible with the nominal pack voltage and current. | TBD, below 60 V DC | Analysis | Section 10 |

## Tasks

### Step 1: Learning burst (3 to 7 days, free)

- [ ] Study BLDC and PMSM basics and commutation.
- [ ] Study field-oriented control and current sensing to working vocabulary.
- [ ] Learn to read motor and controller specifications.
- [ ] Skim open-source examples, such as the SimpleFOC and VESC documentation.
- [ ] Keep a "what I still don't understand" list.

### Step 2: Needs and MVP sketch (1 to 2 days, free)

- [ ] Write a one-page needs sketch: what DRV must do, key numbers from STG-1, interfaces to neighbors, and safety concerns.
- [ ] Note DRV's safe state and failure behavior for the per-subsystem safety approach.
- [ ] Confirm or change the draft subsystem MVP below.

Draft subsystem MVP (proposed, builder to confirm):

| Item | Draft |
| --- | --- |
| Prototype | PRT-DRV-01: the chosen motor and controller, or a small learning motor, on the bench |
| Setup | Spun from a current-limited bench supply at low voltage |
| Test | TST-DRV-001 |
| Pass or fail criterion | Pass if the motor spins on command, speed and current are logged, and a commanded stop brings it safely to rest. Thresholds TBD. |

### Step 3: Concepts (1 to 3 days, free)

- [ ] Sketch two or three options and compare them informally. Weigh learning value, cost, and fit.
- [ ] Treat safety as a pass or fail screen.
- [ ] Decide between a small learning motor and the real motor for the MVP.
- [ ] Log the choice and the rejected options in the decision log.

Concept scoring is left blank on purpose.

| ID | Concept | Learning value | Cost | Fit | Safety screen |
| --- | --- | --- | --- | --- | --- |
| CON-DRV-A | Commercial BLDC kit | | | | |
| CON-DRV-B | Hub motor | | | | |
| CON-DRV-C | Brushed DC | | | | |

### Step 4: Paper proof of concept (1 to 2 weeks, free)

- [ ] Size the motor and gearing against the Stage 1 system requirements.
- [ ] Shortlist motor and controller pairs.
- [ ] Check pack voltage and current compatibility with PACK.
- [ ] Make the go or no-go call on the system goals. If no-go, revisit the goals in STG-1.
- [ ] Draft DRV message needs and hand them to NET.
- [ ] Start a short FMEA, since DRV is safety-relevant.

### Step 5: Spend checkpoint (an hour, free)

- [ ] Answer the [spend checkpoint](../project/PROJECT.md#checkpoints) questions.
- [ ] Write down the one question the purchase answers.
- [ ] Decide which first tools are needed, such as a multimeter and a bench power supply.
- [ ] Decide go, adjust, or park.

### Step 6: Subsystem MVP (2 to 6 weeks)

- [ ] Confirm the workspace safety plan covers this work.
- [ ] Buy the parts and any first tools, and log each purchase with the DRV code.
- [ ] Build PRT-DRV-01 and run TST-DRV-001.
- [ ] Judge the result against the pass or fail criterion.

### Step 7: Fold-back (1 to 2 days, free)

- [ ] Answer the [fold-back checkpoint](../project/PROJECT.md#checkpoints) questions.
- [ ] Update the system goals, interfaces, and hazard list.
- [ ] Feed interface changes back to PACK, VCU, CHS, and NET.
- [ ] Do the enjoyment check, and choose the next subsystem. PACK is next in the recommended order.
- [ ] Write a short process retrospective.

## Deliverables

- Journal entries and a one-page needs sketch.
- Paper proof of concept notes, including the go or no-go call.
- Concept comparison and logged decision.
- Bench results for TST-DRV-001.
- Updated goals, interfaces, hazard list, and budget tracker.

## Spend

Steps 1 to 5 are free. The rough first spend is $40 to $90 for a small learning motor, or $150 to $400 for the real motor and controller. First tools are budgeted separately in [PROJECT.md](../project/PROJECT.md#budget-and-purchasing).

The real motor option can exceed one month's budget. Decide at the spend checkpoint whether rollover covers it.

## Risks and hazards

RSK-002 (unintended acceleration) applies. See the [register](../subsystems/SUBSYSTEMS.md#seed-hazard-and-risk-register).

## Decisions to make

| Decision | Shared with |
| --- | --- |
| Go or no-go on the system goals | System (STG-1) |
| Motor and controller for the kart MVP | None |
| Nominal pack voltage | PACK |
| Learning motor or real motor for the MVP | None |

## Checkpoint questions

Use the spend and fold-back questions in [PROJECT.md](../project/PROJECT.md#checkpoints). DRV adds:

- Can the shortlisted motor and controller meet the system goals at a pack voltage below 60 V DC?
- Does the safe stop work every time it is tested?

## Out of scope

- A builder-designed motor controller or inverter. That is a later, Gold-level goal.
- Final mounting on a frame. That belongs to CHS and STG-3.
- A separate thermal subsystem, unless monitoring shows it is needed.

## Open items

| # | Open item | Owner |
| --- | --- | --- |
| 1 | Targets for REQ-DRV-001 to REQ-DRV-005 | Builder decision |
| 2 | Pass or fail thresholds for TST-DRV-001 | Builder decision |
| 3 | Bench supply voltage and current limit for the MVP | Builder decision |
| 4 | DRV message content on the bus | DRV cycle, with NET |
