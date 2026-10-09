---
id: DEC-010
status: Proposed
decided: TBD
updated: 2026-10-09
---

# DEC-010: Folder structure for non-subsystem work

## Context

Raised in #12 while resolving [DEC-009](DEC-009-subsystem-home-is-a-folder.md). Some valuable content belongs to no single subsystem: simulation tools, libraries shared across subsystems, tools that define system requirements, and other deliverables. Each should stay shareable as its own submodule ([DEC-002](DEC-002-open-source-with-submodules.md)). Where these submodules live is undecided.

## Options

| Option | Pros | Cons |
| --- | --- | --- |
| One shared folder, such as `shared/`, of submodules | Simple; one place to look | Mixes tools, libraries, and deliverables |
| Folders by kind, such as `tools/`, `libs/`, and `deliverables/` | Clear purpose per folder | More folders, and some pieces fit two kinds |
| Treat system-level work as a pseudo-subsystem home (`subsystems/SYS/`) | Reuses the subsystem layout and the SYS code | Blurs the line between subsystems and shared work |

## Decision

TBD. Builder decision.

## Consequences

- When accepted, the Layout section of [CLAUDE.md](../../CLAUDE.md#layout) names the folders.
- Folder names, the rule for a piece shared by two subsystems, and the owner of each piece are TBD.
