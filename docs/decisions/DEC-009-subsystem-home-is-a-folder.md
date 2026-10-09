---
id: DEC-009
status: Accepted
decided: 2026-10-09
updated: 2026-10-09
---

# DEC-009: A subsystem home is a folder of submodules

## Context

Resolves #12 and open item 4 of [STG-1](../stages/STG-1-ARCHITECTURE.md). [DEC-002](DEC-002-open-source-with-submodules.md) gives each atomic piece its own submodule. Submodules exist so a board, simulation tool, code target, or library can be shared, worked on, and shown to employers separately. A subsystem home also holds documentation, and some tools belong to no subsystem.

## Options

| Option | Pros | Cons |
| --- | --- | --- |
| Folder of submodules | Each piece is its own repository and portfolio item; no extra layer | Subsystem documentation lives in the root repository |
| Submodule of submodules | Whole subsystem can be shared as one unit | Nested submodules are awkward, and the extra layer adds no evidence per piece |

## Decision

A subsystem home is a folder in the root repository. Its documentation lives in the folder, and each atomic piece inside it is a submodule.

## Consequences

- [CLAUDE.md](../../CLAUDE.md#layout) Layout states that a home is a folder.
- [DEC-002](DEC-002-open-source-with-submodules.md) no longer lists the question as TBD.
- [STG-1](../stages/STG-1-ARCHITECTURE.md) open item 4 is resolved in #12.
- Work outside any subsystem is covered by [DEC-010](DEC-010-non-subsystem-work-structure.md).
