---
id: DEC-014
status: Proposed
decided: TBD
updated: 2026-10-16
---

# DEC-014: The plant model uses FMI, built in Scilab Xcos and/or OpenModelica

## Context

Raised in #37. The plant model needs a simulation tool that runs standalone for sizing and extends to co-simulation with compiled embedded code. The builder compared candidates and chose Scilab Xcos and OpenModelica. Both have FMI support, are open source, run on macOS, need less effort than a hand-coded tool, and teach well. See [tools/plant-model/](../../tools/plant-model/README.md) and [REQ-SYS-004](../project/GOALS.md#system-requirements).

## Options

| Option | Pros | Cons |
| --- | --- | --- |
| Python: NumPy, SciPy, FMPy | Free, fast to iterate, matches the uv project already started | Hand-coded tool; no block-diagram or acausal modeling; fine-step motor models run slowly |
| C or C++ core with Python bindings | Fast enough for dq and switching models | Hand-coded tool; more build work up front |
| MATLAB, Simulink, and Simscape | Industry standard; strong embedded workflow | Licensed, which conflicts with [DEC-002](DEC-002-open-source-with-submodules.md) |
| Scilab Xcos | Open source; FMI support; macOS support; less setup; block diagrams | Smaller user base than Simulink or Modelica; FMI and macOS details to verify |
| OpenModelica | Open source; FMI support; macOS support; acausal physics libraries | Steep learning curve; FMI and macOS details to verify |
| Scilab Xcos and OpenModelica | Each covers the other's gaps; the shared FMI boundary keeps blocks portable | Two toolchains to maintain |

## Decision

Build the plant model in Scilab Xcos, OpenModelica, or both. The blocks follow one tool-neutral contract in [FRAMEWORK.md](../../tools/plant-model/FRAMEWORK.md). Each tool exports the top-level plant as an FMI co-simulation unit for embedded code. Parameter values come from tool-neutral files. Which tool builds which block is open item 2 in the plant model README.

## Consequences

- [FRAMEWORK.md](../../tools/plant-model/FRAMEWORK.md) is tool-neutral and maps the block contract to each tool.
- The plant model README lists the tool choices, verification, and integration as open items.
- The uv Python project stays in `tools/plant-model/`. Its role is open.
