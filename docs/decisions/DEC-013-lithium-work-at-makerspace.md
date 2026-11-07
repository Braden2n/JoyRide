---
id: DEC-013
status: Proposed
decided: TBD
updated: 2026-11-07
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

Proposed: do no lithium work at home. Use fume-extracted home space for electronics work only, and do lithium work at the makerspace. The builder toured the makerspace and confirmed it as the lithium workspace (#9). It is not yet Accepted, because the fire response and membership cost are not confirmed.

## Consequences

- Confirmed by the builder's tour (#9):
  - The makerspace is the lithium workspace.
  - It permits lithium cell handling and charging.
  - Storage is adequate with safety measures. The measures are TBD.
  - Access is 24/7 after a probationary period. The length of the probation is TBD.
- Open items for the builder, before this DEC is Accepted:
  - Confirm the makerspace fire response: TBD.
  - Confirm membership cost: TBD.
- Resolves [STG-1](../stages/STG-1-ARCHITECTURE.md) open item 1 once Accepted (#9).
- RSK-004 and the PROJECT.md workspace constraint record the builder's finding on the home workspace.
- Once Accepted, the workspace safety plan and the workspace and safety budget line change to fit the makerspace.
