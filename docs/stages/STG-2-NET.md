---
id: STG-2-NET
title: "Stage 2: NET subsystem cycle"
status: draft
owner: Braden Toone (builder)
last_updated: 2026-10-06
subsystem: SUB-NET
spark: not yet decided
source_sections: [7, 8, 9, 10, 12, 13]
---

# STG-2-NET: Network and harness cycle

## Purpose

This cycle turns the message needs collected from other subsystems into a working CAN network on the bench. NET starts light and grows with the other cycles, so it rarely needs much dedicated time.

## Inputs

- [Subsystem cycle template](../project/PROJECT.md#subsystem-cycle)
- [NET subsystem definition](../subsystems/SUBSYSTEMS.md#net-network-and-harness)
- [System goals](STG-1-ARCHITECTURE.md#requirements) and the optional Stage 1 DBC skeleton
- Message needs from every other cycle

**Neighbors to review.** NET touches every subsystem on the bus. This cycle reviews all of them and feeds changes back.

| Neighbor | What to review |
| --- | --- |
| [DRV](../subsystems/SUBSYSTEMS.md#drv-motor-and-drive) | Torque request and status messages |
| [PACK](../subsystems/SUBSYSTEMS.md#pack-battery-pack-bms-and-power-distribution) | Pack state messages; connectors and harness near the pack |
| [VCU](../subsystems/SUBSYSTEMS.md#vcu-vehicle-control-unit) | All VCU messages; MCU family and RTOS decision |
| [TEL](../subsystems/SUBSYSTEMS.md#tel-telemetry-and-apps) | Logger and DBC consumer |
| [CHS](../subsystems/SUBSYSTEMS.md#chs-chassis-and-mechanical) | Harness routing |

## Goals

- Build working vocabulary in CAN framing, bit timing, termination, and DBC files.
- Keep a DBC that records every message as a contract.
- Show two or three nodes exchanging DBC messages with a logger.

## Requirements

Values are TBD unless the builder fixed them.

| ID | Requirement | Target | How to check | Source |
| --- | --- | --- | --- | --- |
| REQ-NET-001 | Subsystems communicate over a shared network (system goal) | Per [STG-1](STG-1-ARCHITECTURE.md#requirements); protocol and rates defined during subsystem work | Test | Section 7 |
| REQ-NET-002 | Every message is recorded as a contract in a DBC. | TBD | Inspection | Section 8 responsibilities |
| REQ-NET-003 | Bus load stays acceptable at the chosen bit rate. | TBD | Analysis and test | Section 10 |
| REQ-NET-004 | Connectors, wiring diagrams, and labels exist for the harness. | TBD | Inspection | Section 8 responsibilities |

## Tasks

### Step 1: Learning burst (3 to 7 days, free)

- [ ] Study CAN 2.0 framing and bit timing.
- [ ] Study termination.
- [ ] Study DBC files.
- [ ] Try example tools, such as SavvyCAN and python-can.
- [ ] Keep a "what I still don't understand" list.

### Step 2: Needs and MVP sketch (1 to 2 days, free)

- [ ] Write a one-page needs sketch: what NET must do, key numbers, interfaces to neighbors, and safety concerns.
- [ ] Note the network's failure behavior, such as CAN loss.
- [ ] Confirm or change the draft subsystem MVP below.

Draft subsystem MVP (proposed, builder to confirm):

| Item | Draft |
| --- | --- |
| Prototype | PRT-NET-01: two or three dev boards and a USB-CAN adapter |
| Setup | Nodes exchange messages defined in the DBC, and a logger records them |
| Test | TST-NET-001 |
| Pass or fail criterion | Pass if every node sends and decodes its DBC messages, and the logger records them correctly. Bit rate and bus load limits TBD. |

### Step 3: Concepts (1 to 3 days, free)

- [ ] Sketch two or three options (buy, adapt open source, build) and compare them informally. Weigh learning value, cost, and fit.
- [ ] Treat safety as a pass or fail screen.
- [ ] Log the choice and the rejected options in the decision log.

Concept scoring is left blank on purpose. The rows are node options from the launch document.

| ID | Concept | Learning value | Cost | Fit | Safety screen |
| --- | --- | --- | --- | --- | --- |
| CON-NET-A | STM32 nodes with FreeRTOS or Zephyr | | | | |
| CON-NET-B | ESP32 for wireless nodes | | | | |
| CON-NET-C | Bare metal for simple nodes | | | | |

### Step 4: Paper proof of concept (1 to 2 weeks, free)

- [ ] Collect message needs from the other cycles as they define them.
- [ ] Draft them in a DBC.
- [ ] Estimate bus load for a candidate bit rate.
- [ ] Draft wiring diagrams and a labeling scheme.

### Step 5: Spend checkpoint (an hour, free)

- [ ] Answer the [spend checkpoint](../project/PROJECT.md#checkpoints) questions.
- [ ] Write down the one question the purchase answers.
- [ ] Decide go, adjust, or park.

### Step 6: Subsystem MVP (2 to 6 weeks)

- [ ] Buy dev boards and a USB-CAN adapter, and log each purchase with the NET code.
- [ ] Build PRT-NET-01 and run TST-NET-001.
- [ ] Judge the result against the pass or fail criterion.

### Step 7: Fold-back (1 to 2 days, free)

- [ ] Answer the [fold-back checkpoint](../project/PROJECT.md#checkpoints) questions.
- [ ] Update the system goals, interfaces, and hazard list.
- [ ] Feed message and harness changes back to every subsystem.
- [ ] Do the enjoyment check, and choose the next subsystem.
- [ ] Write a short process retrospective.

## Deliverables

- Journal entries and a one-page needs sketch.
- A DBC, a bus load estimate, and wiring diagrams.
- Concept comparison and logged decision.
- Bench results for TST-NET-001.
- Updated goals, interfaces, hazard list, and budget tracker.

## Spend

Steps 1 to 5 are free. The rough first spend is $60 to $120. See [PROJECT.md](../project/PROJECT.md#budget-and-purchasing).

## Risks and hazards

RSK-003 (short circuit or arc, from wiring faults) applies. See the [register](../subsystems/SUBSYSTEMS.md#seed-hazard-and-risk-register).

## Decisions to make

| Decision | Shared with |
| --- | --- |
| MCU family and RTOS | VCU |
| Bit rate | All subsystems |
| Connector family | All subsystems |

## Checkpoint questions

Use the spend and fold-back questions in [PROJECT.md](../project/PROJECT.md#checkpoints). NET adds:

- Does every message in the DBC have an owner and a consumer?
- What happens to each node on CAN loss?

## Out of scope

- Application logic in any node. That belongs to the owning subsystem.
- The wireless gateway's remote functions. They belong to the optional RMT.

## Open items

| # | Open item | Owner |
| --- | --- | --- |
| 1 | Targets for REQ-NET-002 to REQ-NET-004 | Builder decision |
| 2 | Candidate bit rate | NET cycle |
| 3 | Whether NET is part of Spark | Builder decision |
