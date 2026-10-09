---
id: DEC-002
status: Accepted
decided: 2026-10-05
updated: 2026-10-06
---

# DEC-002: Fully open source, one submodule per atomic piece

## Context

The repository and its documentation could be public or private, and could be one repository or several.

## Options

| Option | Pros | Cons |
| --- | --- | --- |
| Private repository | No exposure of unfinished work | No portfolio value; conflicts with the open-source principle |
| Public monorepo | Simple | Mixes firmware, PCB, and CAD histories |
| Public root plus submodules | Open, portfolio-ready, each piece versioned on its own | More repositories to manage |

## Decision

Public GitHub. A root repository holds documentation and planning. Each atomic piece (firmware, shared communications library, PCB, CAD, and so on) gets its own Git submodule, created when its work starts.

## Consequences

Subsystem documentation lives in each subsystem's home. See the layout in [CLAUDE.md](../../CLAUDE.md#layout). A home is a folder of submodules ([DEC-009](DEC-009-subsystem-home-is-a-folder.md)).
