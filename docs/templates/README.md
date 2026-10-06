---
id: TEMPLATES
status: active
updated: 2026-10-06
---

# Templates and record schemas

Every repeated document has a template, and every ID type has a schema. Placement and writing rules are in [CLAUDE.md](../../CLAUDE.md).

## Document templates

| Template | Use for | Lives in |
| --- | --- | --- |
| [stage.md](stage.md) | STG documents | `docs/stages/` |
| [decision.md](decision.md) | DEC files | `docs/decisions/` |
| [interface.md](interface.md) | ICD files | `docs/architecture/interfaces/` |
| [journal-entry.md](journal-entry.md) | Journal entries and the four checkpoints | `docs/journal/` |
| [test-report.md](test-report.md) | TST files | Subsystem `docs/tests/`; root for TST-SYS |
| [subsystem/README.md](subsystem/README.md) | Subsystem home index | `subsystems/<CODE>/docs/` |
| [subsystem/REQUIREMENTS.md](subsystem/REQUIREMENTS.md) | Subsystem requirements | `subsystems/<CODE>/docs/` |
| [subsystem/CYCLE.md](subsystem/CYCLE.md) | Subsystem cycle record | `subsystems/<CODE>/docs/` |
| [task.yml](../../.github/ISSUE_TEMPLATE/task.yml) | Backlog tasks | GitHub issues |

## ID formats

Codes: subsystem codes are DRV, PACK, CHS, VCU, TEL, NET, TMS, and RMT. System codes are SYS, SAF, and COST. IDs are never reused, and a dropped item keeps its ID with status Dropped.

| ID | Format | Form | Home |
| --- | --- | --- | --- |
| STG | `STG-1`, `STG-2-<code>`, `STG-3` | File | `docs/stages/` |
| SUB | `SUB-<code>` | Section | `docs/architecture/SUBSYSTEMS.md` |
| NEED | `NEED-NNN` | Row | `docs/project/GOALS.md` |
| REQ (system) | `REQ-<SYS, SAF, or COST>-NNN` | Row | `docs/project/GOALS.md` |
| REQ (subsystem) | `REQ-<subsystem code>-NNN` | Row | Subsystem `REQUIREMENTS.md` |
| ICD | `ICD-<type>-NNN`, type is CAN, PWR, MECH, or HMI | File | `docs/architecture/interfaces/` |
| CON | `CON-<code>-<letter>` | Row | Subsystem `CYCLE.md` |
| DEC | `DEC-NNN` | File | `docs/decisions/` |
| RSK | `RSK-NNN` | Row | `docs/project/RISKS.md` |
| TST | `TST-<code or SYS>-NNN` | File | Subsystem `docs/tests/`; root for SYS |
| PRT | `PRT-<code>-NN` | Row | Subsystem `CYCLE.md` |
| LRN | `LRN-NNN` | Row | `docs/project/GOALS.md` |
| Task | `#N`, GitHub's issue number (no project prefix) | Issue | GitHub issues |

## Status values

| Records | Values |
| --- | --- |
| STG, LRN | Not started, In progress, Blocked, Done |
| Task | Open or closed, in GitHub |
| REQ, NEED | Draft, Agreed, Verified, Dropped |
| DEC | Proposed, Accepted, Superseded |
| RSK | Open, Mitigated, Closed |
| ICD | Draft, Agreed, Superseded |
| CON | Candidate, Chosen, Rejected |
| PRT | Planned, Built, Retired |
| TST | Planned, Passed, Failed |

## Row schemas

Column order is fixed. A future CSV tracker uses the same columns.

| Record | Columns |
| --- | --- |
| NEED | ID, I want..., Priority (must or nice), Status |
| REQ (system) | ID, Requirement, Target, Minimum, How to check, Owner, Status |
| REQ (subsystem) | ID, Requirement, Target, How to check, Parent (REQ or ICD), Status |
| RSK | ID, Risk, Cause, Mitigation, Applies, Subsystems, Status |
| LRN | ID, Learning goal, Evidence, Status |
| CON | ID, Concept, Learning value, Cost, Fit, Safety screen (pass or fail), Status |
| PRT | ID, Description, Answers (question), Tests, Status |
| ICD list row | ID, Between, Type, Status |

Example subsystem requirement row:

| ID | Requirement | Target | How to check | Parent | Status |
| --- | --- | --- | --- | --- | --- |
| REQ-PACK-001 | The BMS opens the contactors on any fault in the fault list. | Within TBD ms | Fault-injection test | REQ-SAF-003 | Draft |

## SUB section block

Each subsystem in SUBSYSTEMS.md uses these parts, in order:

1. `## <CODE>: <name>`
2. A one-line purpose.
3. **Responsibilities**
4. **Boundaries and authority**
5. A Neighbor and Interface table, citing ICD IDs once they exist.
6. **Starting point**
7. **Stage**, a link to the STG-2 document.

Optional subsystems keep only parts 1, 2, 4, and 7 until they are activated.
