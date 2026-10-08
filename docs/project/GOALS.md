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
| REQ-SYS-001 | The kart reaches a useful top speed on level pavement. | 45mph | 30mph | GPS test, calculated wheel speed, other measurement | DRV | Agreed |
| REQ-SYS-002 | The kart runs long enough for a useful session. | 30min | 15min | Field test | PACK | Agreed |
| REQ-SYS-003 | The kart carries its design load, driver plus kart. | 400lb driver | 300lb driver | Test and analysis | CHS | Agreed |
| REQ-SYS-004 | Power and energy are sized for the speed, load, and run time above. | TBD (kW & kWh) - based on sizing simulation | TBD - based on sizing simulation | Analysis and test | DRV, PACK | Draft |
| REQ-SYS-005 | Subsystems communicate over a shared network. | TBD (protocol and rates) | TBD | Test | NET | Draft |
| REQ-SAF-001 | An emergency stop removes traction power independent of software. | Hardware path only | Hardware path only | Test and inspection | PACK | Draft |
| REQ-SAF-002 | The battery stays below the shock-hazard voltage ceiling at full charge. | Below 60 V DC (fixed) | Below 60 V DC | Measurement | PACK | Agreed |
| REQ-SAF-003 | The battery system protects its cells and disconnects safely on faults. | TBD (fault list from STG-2-PACK) | TBD | Fault-injection test | PACK | Draft |
| REQ-SAF-004 | A single sensor or software fault cannot command unintended acceleration. | TBD (fault behavior from STG-2-VCU) | TBD | Fault-injection test | VCU | Draft |
| REQ-COST-001 | Spend stays within the budget plan. | $150 per month, rollover allowed (fixed)  | Same | Budget tracker | Project | Agreed |

Owners are proposed. Stage 1 confirms them.

## Learning goals

Learning is the desired outcome. These goals are aspirational, and might not all be attainable at all targets on the project ladder. These serve as possible directions and skills that might be learned throughout the project, in various levels of depth and execution.

Beginner < Novice < Intermediate < Competent < Proficient < Experienced < Expert

| ID | Skill area | Starting level | Target by project end | Practiced in |
| --- | --- | --- | --- | --- | --- |
| LRN-001 | Product requirements and systems engineering | Novice | Clearly define, refine, and specify requirements at product, system, subsystem, and implementation levels | STG-1 |
| LRN-002 | Subsystem architecture and design | Intermediate | Convert system requirements into easily transferable subsystem designs and specifications for implementation | STG-2 |
| LRN-003 | Design implementation | Intermediate | Develop and deliver implementations that meet subsystem design specifications | STG-3 |
| LRN-004 | Embedded C/C++, drivers, RTOS | Novice | Create custom drivers and RTOS applications on several nodes with shared libraries and packages | STG-2, STG-3 |
| LRN-005 | Schematic design and PCB layout | Novice | Develop and bring up custom power and mixed-signal boards that support subsystem requirements | STG-2 |
| LRN-006 | Vehicle networking | Intermediate | Create application-specific network with diagnostics and other higher-layer protocols | STG-2-NET |
| LRN-007 | Battery management and state estimation | Intermediate | Design BMS with power distribution and safety control authority and estimation algorithms | STG-2-PACK |
| LRN-008 | Vehicle control and state management | Novice | Implement full vehicle control strategy on a VCU | STG-2-VCU |
| LRN-009 | Motor control (Trapezoidal / FOC) | Beginner | Understand and implement motor control on a controller | STG-2-DRV |
| LRN-010 | 3D CAD and mechanical design | Novice | Design mounting system, enclosures, and structures for the vehicle | STG-2-CHS |
| LRN-011 | Data interface and software | Competent | Design live telemetry dashboard and data analysis app | STG-2-TEL |
