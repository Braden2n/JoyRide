---
id: PLANT-MODEL
status: draft
updated: 2026-10-16
---

# Plant model

A vehicle powertrain plant model for JoyRide, built in Scilab Xcos ([DEC-014](../../docs/decisions/DEC-014-plant-model-in-xcos.md), proposed). It starts as the sizing model v0 of [STG-1](../../docs/stages/STG-1-ARCHITECTURE.md#1b-system-level-research-about-1-week) task 1b. Later it becomes the plant for co-simulation with compiled embedded code.

| Field | Value |
| --- | --- |
| Serves | REQ-SYS-001, REQ-SYS-002, REQ-SYS-003, REQ-SYS-004, REQ-SAF-002 in [GOALS.md](../../docs/project/GOALS.md#system-requirements) |
| Owners | DRV and PACK |
| Users | DRV, PACK, VCU, and TMS cycles; STG-3 integration |
| Tool | Scilab Xcos, per [DEC-014](../../docs/decisions/DEC-014-plant-model-in-xcos.md) (proposed) |
| Form | Plain folder until real code exists, then its own submodule ([DEC-002](../../docs/decisions/DEC-002-open-source-with-submodules.md), [DEC-010](../../docs/decisions/DEC-010-non-subsystem-work-structure.md)) |
| Design | [FRAMEWORK.md](FRAMEWORK.md) |

## Use modes

| Mode | Question it answers | Controller | Stage |
| --- | --- | --- | --- |
| Sizing | What power, voltage, gearing, and energy meet the goals? | Ideal, inside the diagram | STG-1 |
| Co-simulation | Does the embedded code behave correctly against the plant? | Compiled VCU, BMS, or motor control code | STG-2 and STG-3 |

## Layout

Planned top-level structure. Create each folder only when its first file exists.

```text
tools/plant-model/
  README.md        this file
  FRAMEWORK.md     plant structure, interfaces, and the Xcos mapping
  models/          Xcos diagrams (.zcos), one per block and one top-level plant
  params/          parameter scripts, one per vehicle configuration
  cycles/          drive cycles and scenarios (DEC-011)
  sim/             sweep scripts and co-simulation setup
  studies/         sizing studies and their results
  pyproject.toml   builder's uv Python project (FMPy); kept, role in open item 4
  src/             Python package for that project
```

Exported FMUs are generated and are not committed.

## Open items

| # | Open item | Owner |
| --- | --- | --- |
| 1 | Accept [DEC-014](../../docs/decisions/DEC-014-plant-model-in-xcos.md) (Scilab Xcos for the plant model) in #37. | Builder decision |
| 2 | Verify on macOS: the Scilab Xcos version, FMI export and import, and that the exported FMU loads in FMPy. | STG-1 task 1b |
| 3 | Choose how compiled embedded code joins the plant: a direct shared-library link, or a wrapper FMU. | Builder decision |
| 4 | Choose the role of the Python project: post-processing, FMU runner, or removed. | Builder decision |
| 5 | Parameter values for every block. Each is TBD until research or a test supplies it. | STG-1 task 1b, then each cycle |
