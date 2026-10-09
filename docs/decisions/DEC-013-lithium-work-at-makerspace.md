---
id: DEC-013
status: Proposed
decided: TBD
updated: 2026-10-09
---

# DEC-013: Do lithium work at a local makerspace

## Context

[STG-1](../stages/STG-1-ARCHITECTURE.md) open item 1 asked whether the home workspace is safe for lithium work. Raised in #9. The builder assessed it and found it is not. [RSK-004](../project/RISKS.md) and [DEC-008](DEC-008-solo-battery-work-plan.md) depend on the answer.

- With desktop fume extraction, the home workspace is safe for electronics work.
- It has too little space to remove a battery in an emergency (thermal runaway or electrolyte leakage).
- Lithium fumes in the home workspace would not be acceptable.

The builder found a local makerspace that could serve as the alternative. It may also give access to 3D printers, a metal shop, and electronics equipment, which could cut capital spend.

## Options

| Option | Pros | Cons |
| --- | --- | --- |
| Home workspace for all work | No travel, no fees | Fails the emergency and fume checks for lithium |
| Home for electronics, makerspace for lithium | Meets the lithium safety need, keeps routine work at home | Lithium sessions need travel and makerspace rules |
| Makerspace for all kart work | Shared tools may reduce spend | Travel for every session, makerspace rules apply to all work |

## Decision

Proposed: do no lithium work at home. Use fume-extracted home space for electronics work only, and do lithium work at the makerspace, once the makerspace is confirmed. The builder has not yet stated the makerspace as final.

## Consequences

- Open items for the builder, before this DEC is Accepted:
  - Confirm the makerspace is the lithium workspace.
  - Confirm the makerspace permits lithium cell handling, charging, and storage, and has a fire response: TBD.
  - Confirm membership cost and access hours: TBD.
- Resolves [STG-1](../stages/STG-1-ARCHITECTURE.md) open item 1 once Accepted (#9).
- Follow-ups for the builder to approve, not made here:
  - Update RSK-004 cause and mitigation.
  - Revisit the workspace and safety budget line and the workspace assumption in PROJECT.md, given shared tool access.
  - Rewrite the workspace safety plan for the makerspace.
