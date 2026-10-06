---
id: STG-2-RMT
status: Not started
updated: 2026-10-06
stage_type: cycle
subsystem: RMT
spark: not yet decided
---

# STG-2-RMT: Remote and wireless (optional)

## Purpose

Explore a remote kill, speed limiting, and wireless configuration that fail safe. This is a parking-lot idea until the core subsystems are done.

## Entry and exit

- Entry: the core subsystems are done, and the builder chooses to start RMT.
- Exit: the fold-back checkpoint is answered, or the cycle is parked.

## Inputs and neighbors

- Neighbors: VCU, NET, PACK. Interfaces are in [SUBSYSTEMS.md](../architecture/SUBSYSTEMS.md#rmt-remote-and-wireless-optional).

## Goals

- A remote kill whose link loss removes torque.

## System goals served

None yet.

## Tasks

### Step 1: Learning burst

- [ ] Study wireless link basics (for example ELRS or BLE), failsafe behavior, and wireless safety.

### Step 2: Needs and MVP sketch

- [ ] Draft MVP: a wireless link between two dev boards with a failsafe test. Pass or fail TBD (proposed, builder to confirm).

### Step 3: Concepts

- [ ] Compare two or three link options.

### Step 4: Paper proof of concept

- [ ] Design the remote kill and its failsafe behavior.

### Step 5: Spend checkpoint

- [ ] Go, adjust, or park.

### Step 6: Subsystem MVP

- [ ] Build the link and run the failsafe test.

### Step 7: Fold-back

- [ ] Feed changes back to VCU, NET, GOALS, and RISKS.

## Deliverables

Standard cycle deliverables.

## Spend

$30 to $60.

## Risks

RSK-002, RSK-007.

## Decisions

| Decision | Shared with | DEC |
| --- | --- | --- |
| Whether to start RMT | none | |
| Wireless link type | NET | |

## Checkpoint additions

- Does link loss always remove torque?

## Out of scope

- Replacing the hardware E-stop.

## Open items

None.
