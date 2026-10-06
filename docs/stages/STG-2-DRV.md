---
id: STG-2-DRV
status: Not started
updated: 2026-10-06
stage_type: cycle
subsystem: DRV
spark: yes
---

# STG-2-DRV: Motor and drive

## Purpose

Choose a motor and controller and spin it on the bench. The paper proof of concept doubles as a go or no-go check on the system goals. If DRV cannot meet them, the rest of the system probably cannot either.

## Entry and exit

- Entry: the architecture checkpoint is answered.
- Exit: the fold-back checkpoint is answered, or the cycle is parked at the spend checkpoint.

## Inputs and neighbors

- Sizing model v0 and system goals from [STG-1](STG-1-ARCHITECTURE.md).
- Neighbors: PACK, VCU, CHS, NET. Interfaces are in [SUBSYSTEMS.md](../architecture/SUBSYSTEMS.md#drv-motor-and-drive).

## Goals

- A go or no-go call on the system goals.
- A motor spun safely at low voltage, with speed and current logged.

## System goals served

REQ-SYS-001, REQ-SYS-004.

## Tasks

### Step 1: Learning burst

- [ ] Study BLDC and PMSM basics, commutation, FOC, and current sensing.
- [ ] Learn to read motor and controller specifications.
- [ ] Skim open-source examples, such as SimpleFOC and VESC.

### Step 2: Needs and MVP sketch

- [ ] Create `subsystems/DRV/docs/` from the subsystem templates.
- [ ] Write REQUIREMENTS.md from the DRV boundaries in SUBSYSTEMS.md.
- [ ] Confirm the draft MVP below.

| MVP | Draft (proposed, builder to confirm) |
| --- | --- |
| Prototype | PRT-DRV-01: the chosen motor and controller, or a small learning motor, on a current-limited bench supply at low voltage |
| Test | TST-DRV-001 |
| Pass or fail | Spins on command, speed and current are logged, and a commanded stop brings it safely to rest. Thresholds TBD. |

### Step 3: Concepts

- [ ] Compare a commercial BLDC kit, a hub motor, and brushed DC.
- [ ] Decide between a small learning motor and the real motor for the MVP.

### Step 4: Paper proof of concept

- [ ] Size the motor and gearing against REQ-SYS-001 and REQ-SYS-004.
- [ ] Shortlist motor and controller pairs, and check voltage and current compatibility with PACK.
- [ ] Make the go or no-go call. On no-go, revisit GOALS.md.
- [ ] Send DRV message needs to NET.
- [ ] Draft the FMEA.

### Step 5: Spend checkpoint

- [ ] Decide which first tools are needed, such as a multimeter and a bench supply.
- [ ] Write the question the purchase answers.

### Step 6: Subsystem MVP

- [ ] Confirm the workspace safety plan covers this work.
- [ ] Build PRT-DRV-01 and run TST-DRV-001.

### Step 7: Fold-back

- [ ] Feed changes back to PACK, VCU, CHS, NET, GOALS, and RISKS.

## Deliverables

Standard cycle deliverables, plus a go or no-go note.

## Spend

$40 to $90 for a small learning motor, or $150 to $400 for the real motor and controller. First tools are separate. The real option can exceed one month's budget, so check the rollover balance.

## Risks

RSK-002.

## Decisions

| Decision | Shared with | DEC |
| --- | --- | --- |
| Go or no-go on the system goals | All | |
| Motor and controller for the kart MVP | none | |
| Nominal pack voltage (for example 24, 36, or 48 V) | PACK | |
| Learning motor or real motor for the MVP | none | |

## Checkpoint additions

- Can the shortlisted pair meet the system goals below 60 V DC?
- Does the safe stop work every time it is tested?

## Out of scope

- A builder-designed controller or inverter (Gold).
- Mounting on a frame (CHS and STG-3).

## Open items

| # | Open item | Owner |
| --- | --- | --- |
| 1 | Bench supply voltage and current limit for the MVP | Builder decision |
| 2 | Pass or fail thresholds for TST-DRV-001 | Builder decision |
