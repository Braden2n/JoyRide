---
id: DEC-014
status: Proposed
decided: TBD
updated: 2026-10-16
---

# DEC-014: The plant model is built in Scilab Xcos

## Context

Raised in #37. The plant model needs one simulation tool that runs standalone for sizing and extends to co-simulation with compiled embedded code. The builder compared candidates and chose Scilab Xcos for FMI support, open-source licensing, macOS support, low setup effort, and value as a learning environment. See [tools/plant-model/](../../tools/plant-model/README.md) and [REQ-SYS-004](../project/GOALS.md#system-requirements).

## Options

| Option | Pros | Cons |
| --- | --- | --- |
| Python: NumPy, SciPy, FMPy | Free, fast to iterate, matches the uv project already started | No block-diagram view; fine-step motor models run slowly; no block authoring |
| C or C++ core with Python bindings | Fast enough for dq and switching models | More build work up front |
| OpenModelica | Acausal physics libraries; FMI support | Steep learning curve |
| MATLAB, Simulink, and Simscape | Industry standard; strong embedded workflow | Licensed, which conflicts with [DEC-002](DEC-002-open-source-with-submodules.md) |
| Scilab Xcos | Open source; FMI support; macOS support; less setup; good learning environment | Smaller user base than Simulink or Modelica; FMI and macOS details to verify |

## Decision

Build the plant model as Xcos diagrams. Each block is a superblock. Export the top-level plant as an FMI co-simulation unit for embedded code. Python stays for scripting and post-processing, pending open item 4 in the plant model README.

## Consequences

- [FRAMEWORK.md](../../tools/plant-model/FRAMEWORK.md) describes the plant in Xcos terms.
- The plant model README lists the verification and integration choices as open items 2, 3, and 4.
- The uv Python project stays in `tools/plant-model/`. Its role is open.
- When accepted, this DEC is cited from [STG-1](../stages/STG-1-ARCHITECTURE.md) and #37 is closed.
