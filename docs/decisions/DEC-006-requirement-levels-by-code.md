---
id: DEC-006
status: Accepted
decided: 2026-10-06
updated: 2026-10-06
---

# DEC-006: Requirement level is set by its code

## Context

The first goals list mixed subsystem codes into system goals (REQ-PACK-001, REQ-VCU-001, REQ-NET-001), so a REQ's level and home were ambiguous.

## Options

| Option | Pros | Cons |
| --- | --- | --- |
| Add a level field | No renumbering | The ID alone does not say where the REQ lives |
| Reserve system codes | The ID alone gives the level and home | Four goals are renumbered |

## Decision

System requirements use only SYS, SAF, and COST, and live in [GOALS.md](../project/GOALS.md). Subsystem requirements use a subsystem code and live in that subsystem's home. Renumbered: REQ-PACK-001 to REQ-SAF-002, REQ-PACK-002 to REQ-SAF-003, REQ-VCU-001 to REQ-SAF-004, and REQ-NET-001 to REQ-SYS-005.

## Consequences

Every subsystem REQ must name a parent system REQ or ICD.
