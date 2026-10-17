---
id: DEC-010
status: Accepted
decided: 2026-10-16
updated: 2026-10-16
---

# DEC-010: Non-subsystem work lives in folders by kind

## Context

Raised in #12 while resolving [DEC-009](DEC-009-subsystem-home-is-a-folder.md). Some valuable content belongs to no single subsystem: simulation tools, libraries shared across subsystems, tools that define system requirements, and other deliverables. Each should stay shareable as its own submodule ([DEC-002](DEC-002-open-source-with-submodules.md)). Where these submodules live is undecided. Resolved in #36.

## Options

| Option | Pros | Cons |
| --- | --- | --- |
| One shared folder, such as `shared/`, of submodules | Simple; one place to look | Mixes tools, libraries, and deliverables |
| Folders by kind, such as `tools/`, `libs/`, and `deliverables/` | Clear purpose per folder | More folders, and some pieces fit two kinds |
| Treat system-level work as a pseudo-subsystem home (`subsystems/SYS/`) | Reuses the subsystem layout and the SYS code | Blurs the line between subsystems and shared work |

## Decision

Work outside a single subsystem lives in root folders named by kind. `tools/` holds simulation and analysis tools. Other kind folders are named when their first piece exists.

## Consequences

- The Layout section of [CLAUDE.md](../../CLAUDE.md#layout) names `tools/`.
- Each piece's README names its owners.
- The first piece is `tools/plant-model/`. It stays a plain folder until real code exists, then becomes a submodule ([DEC-002](DEC-002-open-source-with-submodules.md)).
- [STG-1](../stages/STG-1-ARCHITECTURE.md) open item 3 is resolved in #36.
