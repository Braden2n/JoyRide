---
id: STG-2-NET
status: Not started
updated: 2026-10-06
stage_type: cycle
subsystem: NET
spark: not yet decided
---

# STG-2-NET: Network and harness

## Purpose

Turn the message needs from the other cycles into a working CAN network on the bench. NET grows with the other cycles, so it rarely needs much dedicated time.

## Entry and exit

- Entry: the TEL fold-back chose NET. The DBC grows from STG-1 onward.
- Exit: the fold-back checkpoint is answered, or the cycle is parked at the spend checkpoint.

## Inputs and neighbors

- Message needs from every other cycle, and the optional DBC skeleton from STG-1.
- Neighbors: all subsystems. Interfaces are in [SUBSYSTEMS.md](../architecture/SUBSYSTEMS.md#interfaces).

## Goals

- A DBC that records every message as a contract.
- Two or three nodes exchanging DBC messages with a logger.

## System goals served

REQ-SYS-005.

## Tasks

### Step 1: Learning burst

- [ ] Study CAN 2.0 framing, bit timing, and termination.
- [ ] Study DBC files.
- [ ] Try example tools, such as SavvyCAN and python-can.

### Step 2: Needs and MVP sketch

- [ ] Create `subsystems/NET/docs/` from the subsystem templates.
- [ ] Write REQUIREMENTS.md, including each node's behavior on CAN loss.
- [ ] Confirm the draft MVP below.

| MVP | Draft (proposed, builder to confirm) |
| --- | --- |
| Prototype | PRT-NET-01: two or three dev boards and a USB-CAN adapter |
| Test | TST-NET-001 |
| Pass or fail | Every node sends and decodes its DBC messages, and the logger records them correctly. Bit rate and bus load limits TBD. |

### Step 3: Concepts

- [ ] Compare node options, for example STM32 with an RTOS, ESP32 for wireless nodes, and bare metal for simple nodes.

### Step 4: Paper proof of concept

- [ ] Collect message needs into a DBC.
- [ ] Estimate bus load for a candidate bit rate.
- [ ] Draft wiring diagrams and a labeling scheme.

### Step 5: Spend checkpoint

- [ ] Write the question the purchase answers.

### Step 6: Subsystem MVP

- [ ] Build PRT-NET-01 and run TST-NET-001.

### Step 7: Fold-back

- [ ] Feed message and harness changes back to every subsystem.

## Deliverables

Standard cycle deliverables, plus the DBC, the bus load estimate, and the wiring diagrams.

## Spend

$60 to $120.

## Risks

RSK-003.

## Decisions

| Decision | Shared with | DEC |
| --- | --- | --- |
| MCU family and RTOS | VCU | |
| Bit rate | All | |
| Connector family | All | |

## Checkpoint additions

- Does every DBC message have an owner and a consumer?
- What does each node do on CAN loss?

## Out of scope

- Application logic in any node (the owning subsystem).
- Remote functions of the wireless gateway (RMT).

## Open items

| # | Open item | Owner |
| --- | --- | --- |
| 1 | Whether NET is part of Spark | Builder decision |
