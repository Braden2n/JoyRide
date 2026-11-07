---
id: DEC-013
status: Accepted
decided: 2026-11-07
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

Do no lithium work at home. Use fume-extracted home space for electronics work only, and do lithium work at the makerspace. The builder confirmed the makerspace as the lithium workspace, with its fire response and membership cost (#9).

## Consequences

- Makerspace facts, from the builder's tour (#9):
  - It permits lithium cell handling and charging.
  - Storage is adequate with safety measures: safe deactivation or neutralization of any HV source, and packaging in an enclosed environment until the battery system is self-contained with its own enclosure.
  - Access is 24/7 after a 30-day probationary period.
  - It has a fire response.
  - Membership costs $45 per month, against the $150 monthly cap in [PROJECT.md](../project/PROJECT.md#builder-and-constraints).
- Resolves [STG-1](../stages/STG-1-ARCHITECTURE.md) open item 1 (#9).
- RSK-004 and the PROJECT.md workspace constraint record the builder's finding on the home workspace.
- Once Accepted, the workspace safety plan and the workspace and safety budget line change to fit the makerspace.
