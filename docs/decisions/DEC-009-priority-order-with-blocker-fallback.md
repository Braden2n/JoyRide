---
id: DEC-009
status: Accepted
decided: 2026-10-09
updated: 2026-10-09
---

# DEC-009: Work cycles in priority order, falling back when blocked

## Context

[PROJECT](../project/PROJECT.md#development-approach) said to run one cycle at a time. [STG-1](../stages/STG-1-ARCHITECTURE.md) open item 2 asked whether to start the DRV and PACK paper proofs in the first weeks instead. Raised in #10. The builder expects cycles to block each other on decisions, so neither option fits.

## Options

| Option | Pros | Cons |
| --- | --- | --- |
| One cycle at a time | Simple, one focus | Stalls when a cycle needs a decision from another |
| Start DRV and PACK paper proofs in the first weeks | Surfaces shared decisions early | Fixed pair, splits attention before a blocker exists |
| Priority order with blocker fallback | Always moves, work follows real dependencies | Needs each blocker named and tracked |

## Decision

Work the cycle highest in the [DEC-005](DEC-005-subsystem-order.md) order until it is blocked. On a blocker, run the cycle that clears it, using the standard process, until the blocker is resolved or another blocker arises. Then repeat the rule for that blocker, and return to the highest-priority unblocked cycle.

## Consequences

- Several cycles may be open at once. Each blocker is a Blocked issue naming the cycle that owns it.
- The rule replaces "run one subsystem cycle at a time" in PROJECT.md.
- Resolves STG-1 open item 2 (#10).
