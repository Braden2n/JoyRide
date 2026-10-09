---
id: DEC-009
status: Accepted
decided: 2026-10-09
updated: 2026-10-09
---

# DEC-009: A useful session is a multi-scenario drive cycle

## Context

[REQ-SYS-002](../project/GOALS.md#system-requirements) says the kart runs long enough for a useful session, but never defined one. This was open item 3 of [STG-1](../stages/STG-1-ARCHITECTURE.md). The builder decided it in #11. PACK sizes energy from this requirement.

## Options

| Option | Pros | Cons |
| --- | --- | --- |
| Continuous run at one steady speed | Simple to test | Does not represent real driving |
| A drive cycle that exposes the driver to multiple driving scenarios | Matches how the kart will be used and sizes energy for varied load | Needs a defined cycle before PACK can size energy |

## Decision

A useful session is a drive cycle that lets the driver experience multiple different driving scenarios. Examples:

- Multiple laps of an endurance course.
- A test drive that yields enough meaningful data for statistical analysis.
- A show run that demonstrates kart performance to others.

## Consequences

- [GOALS.md](../project/GOALS.md#system-requirements) REQ-SYS-002 now cites this DEC. Its 30min target and 15min minimum are unchanged.
- The reference drive cycle for PACK energy sizing (REQ-SYS-004) is still TBD. It must cover the examples above.
- [STG-1](../stages/STG-1-ARCHITECTURE.md) open item 3 is resolved in #11.
