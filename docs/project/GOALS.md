---
id: GOALS
status: draft
updated: 2026-10-06
---

# JoyRide goals

The kart's goals and the builder's learning goals. Both are measured against the [success ladder](PROJECT.md#success-ladder).

## Needs

The builder is the customer. Write 8 to 12 plain "I want..." statements in [STG-1](../stages/STG-1-ARCHITECTURE.md) task 1c, and mark each as must-have or nice-to-have.

| ID | I want... | Priority | Status |
| --- | --- | --- | --- |

## System requirements

System requirements use only the SYS, SAF, and COST codes. Subsystem requirements live in each subsystem's home and trace back to these. Stage 1 sets every TBD value and grows the list to 10 to 15 goals.

| ID | Requirement | Target | Minimum | How to check | Owner | Status |
| --- | --- | --- | --- | --- | --- | --- |
| REQ-SYS-001 | The kart reaches a useful top speed on level pavement. | TBD (starting input: about 30 mph) | TBD | GPS test | DRV | Draft |
| REQ-SYS-002 | The kart runs long enough for a useful session. | TBD | TBD | Test | PACK | Draft |
| REQ-SYS-003 | The kart carries its design load, driver plus kart. | TBD (starting inputs: about 300 lb driver, about 200 lb kart) | TBD | Test and analysis | CHS | Draft |
| REQ-SYS-004 | Power and energy are sized for the speed, load, and run time above. | TBD, from the sizing model | TBD | Analysis and test | DRV, PACK | Draft |
| REQ-SYS-005 | Subsystems communicate over a shared network. | TBD (protocol and rates) | TBD | Test | NET | Draft |
| REQ-SAF-001 | An emergency stop removes traction power independent of software. | Hardware path only | Hardware path only | Test and inspection | PACK | Draft |
| REQ-SAF-002 | The battery stays below the shock-hazard voltage ceiling at full charge. | Below 60 V DC (fixed) | Below 60 V DC | Measurement | PACK | Agreed |
| REQ-SAF-003 | The battery system protects its cells and disconnects safely on faults. | TBD (fault list from STG-2-PACK) | TBD | Fault-injection test | PACK | Draft |
| REQ-SAF-004 | A single sensor or software fault cannot command unintended acceleration. | TBD (fault behavior from STG-2-VCU) | TBD | Fault-injection test | VCU | Draft |
| REQ-COST-001 | Spend stays within the budget plan. | $150 per month, rollover allowed (fixed) | Same | Budget tracker | Project | Agreed |

Owners are proposed. Stage 1 confirms them.

## Learning goals

Learning is the product. Starting levels marked "assumed" need the builder to confirm them. Some targets reach beyond Spark and describe the full ladder.

| Skill area | Starting level | Target by project end | Practiced in |
| --- | --- | --- | --- |
| Requirements and systems engineering | Strong in practice | A light but traceable process at system and subsystem level | STG-1 |
| Power distribution and HV safety | Strong | Own pack power path with precharge, contactors, and fault handling | STG-2-PACK |
| Schematic capture and PCB layout | Assumed moderate | Multi-layer power and mixed-signal boards that work on rev B | STG-2-NET, STG-2-PACK, STG-2-DRV |
| Embedded C/C++, drivers, RTOS | Some | Drivers and RTOS applications on several nodes | STG-2-VCU, STG-2-PACK, STG-2-NET |
| CAN and vehicle networking | Likely strong | DBC-driven network with diagnostics and a gateway | STG-2-NET |
| Battery management and state estimation | Assumed moderate | Own BMS with a state of charge estimator tested against data | STG-2-PACK |
| Motor control (FOC) | Assumed new | Field-oriented control on a self-built inverter | STG-2-DRV |
| 3D CAD and mechanical design | Assumed new | Enclosures and brackets that fit on the first or second try | STG-2-CHS |
| Web and mobile software | Educational background | Live telemetry dashboard and a configuration app | STG-2-TEL |
| Test and verification | Moderate | Written procedures, fault injection, and automated analysis | All |

| ID | Learning goal | Evidence | Status |
| --- | --- | --- | --- |
| LRN-001 | Take a board from schematic to ordered, assembled, and debugged. | Bring-up report | Not started |
| LRN-002 | Write a DBC and use it across at least three nodes and a logger. | TBD | Not started |
| LRN-003 | Build RTOS firmware with a layered driver structure on two different boards. | TBD | Not started |
| LRN-004 | Characterize a cell and fit a battery model in Python. | TBD | Not started |
| LRN-005 | Implement and compare two state of charge estimators on logged data. | TBD | Not started |
| LRN-006 | Design and test a precharge and contactor circuit with fault handling. | TBD | Not started |
| LRN-007 | Run a Pugh chart and a weighted decision matrix, and record the decision. | TBD | Not started |
| LRN-008 | Run a fault-injection test campaign and close every finding. | TBD | Not started |
| LRN-009 | Run FOC on a motor, first with open-source firmware, then with own hardware. | TBD | Not started |
| LRN-010 | Complete one subsystem cycle and change the process as a result. | TBD | Not started |
