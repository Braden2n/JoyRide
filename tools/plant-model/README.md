---
id: PLANT-MODEL
status: draft
updated: 2026-10-16
---

# Plant model

A vehicle powertrain plant model for JoyRide. It starts as the sizing model v0 of [STG-1](../../docs/stages/STG-1-ARCHITECTURE.md#1b-system-level-research-about-1-week) task 1b. Later it becomes the plant for co-simulation with compiled embedded code. The model is tool-neutral: Scilab Xcos or OpenModelica builds it, and FMI connects it to the embedded code ([DEC-014](../../docs/decisions/DEC-014-plant-model-in-xcos.md), proposed).

| Field | Value |
| --- | --- |
| Serves | REQ-SYS-001, REQ-SYS-002, REQ-SYS-003, REQ-SYS-004, REQ-SAF-002 in [GOALS.md](../../docs/project/GOALS.md#system-requirements) |
| Owners | DRV and PACK |
| Users | DRV, PACK, VCU, and TMS cycles; STG-3 integration |
| Tools | Scilab Xcos or OpenModelica, per [DEC-014](../../docs/decisions/DEC-014-plant-model-in-xcos.md) (proposed) |
| Form | Plain folder until real code exists, then its own submodule ([DEC-002](../../docs/decisions/DEC-002-open-source-with-submodules.md), [DEC-010](../../docs/decisions/DEC-010-non-subsystem-work-structure.md)) |
| Design | [FRAMEWORK.md](FRAMEWORK.md) |

## Use modes

| Mode | Question it answers | Controller | Stage |
| --- | --- | --- | --- |
| Sizing | What power, voltage, gearing, and energy meet the goals? | Ideal, inside the model | STG-1 |
| Co-simulation | Does the embedded code behave correctly against the plant? | Compiled VCU, BMS, or motor control code | STG-2 and STG-3 |

## Layout

Planned top-level structure. Create each folder only when its first file exists.

```text
tools/plant-model/
  README.md        this file
  FRAMEWORK.md     tool-neutral plant spec: physics, block contract, FMI boundary
  params/          tool-neutral parameter sets, one per configuration, read by both tools
  cycles/          drive cycles and scenarios (DEC-011)
  xcos/            Scilab Xcos diagrams and scripts
  modelica/        OpenModelica package and scripts
  sim/             runners and co-simulation setup, for either tool
  studies/         sizing studies and their results
  pyproject.toml   builder's uv Python project (FMPy); kept, role in open item 6
  src/             Python package for that project
```

Exported FMUs are generated and are not committed.

## Open items

| # | Open item | Owner |
| --- | --- | --- |
| 1 | Accept [DEC-014](../../docs/decisions/DEC-014-plant-model-in-xcos.md) (Scilab Xcos and/or OpenModelica, joined by FMI) in #37. | Builder decision |
| 2 | Choose which tool builds which block, or whether both build every block. | Builder decision |
| 3 | Verify on macOS, for each tool: version, FMI export and import, and that the exported FMU loads in FMPy. | STG-1 task 1b |
| 4 | Choose how compiled embedded code joins the plant: a direct shared-library link, or a wrapper FMU. | Builder decision |
| 5 | Choose the format of the tool-neutral parameter files in `params/`. | Builder decision |
| 6 | Choose the role of the Python project: post-processing, FMU runner, or removed. | Builder decision |
| 7 | Parameter values for every block. Each is TBD until research or a test supplies it. | STG-1 task 1b, then each cycle |
