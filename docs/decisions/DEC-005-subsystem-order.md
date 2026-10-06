---
id: DEC-005
status: Accepted
decided: 2026-10-05
updated: 2026-10-06
---

# DEC-005: Subsystem order DRV, PACK, CHS, VCU, TEL, NET

## Context

Stage 2 runs one subsystem cycle at a time, so the cycles need an order. Any subsystem could go first.

## Options

| Option | Pros | Cons |
| --- | --- | --- |
| DRV first | Motor selection drives most other work, and its proof of concept checks the system goals | Needs Stage 1 sizing numbers |
| PACK first | Plays to the builder's power distribution strengths | Sized from DRV's needs, so it may need rework |
| VCU or TEL first | Cheapest start | Defers the riskiest questions |

## Decision

The order is DRV, PACK, CHS, VCU, TEL, NET. TMS and RMT are optional and come after the core subsystems.

## Consequences

Any fold-back may change the order with a new DEC. NET is mostly defined during the other cycles.
