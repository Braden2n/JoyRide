---
id: PLANT-MODEL
status: draft
updated: 2026-10-16
---

# Plant model

A vehicle powertrain plant model for JoyRide. It starts as the sizing model v0 of [STG-1](../../docs/stages/STG-1-ARCHITECTURE.md#1b-system-level-research-about-1-week) task 1b. Later it becomes the plant for co-simulation with compiled embedded code.

| Field | Value |
| --- | --- |
| Serves | REQ-SYS-001, REQ-SYS-002, REQ-SYS-003, REQ-SYS-004, REQ-SAF-002 in [GOALS.md](../../docs/project/GOALS.md#system-requirements) |
| Owners | DRV and PACK |
| Users | DRV, PACK, VCU, and TMS cycles; STG-3 integration |
| Form | Plain folder until real code exists, then its own submodule ([DEC-002](../../docs/decisions/DEC-002-open-source-with-submodules.md), [DEC-010](../../docs/decisions/DEC-010-non-subsystem-work-structure.md)) |
| Design | [FRAMEWORK.md](FRAMEWORK.md) |

## Use modes

| Mode | Question it answers | Controller | Stage |
| --- | --- | --- | --- |
| Sizing | What power, voltage, gearing, and energy meet the goals? | Ideal, inside the model | STG-1 |
| Co-simulation | Does the embedded code behave correctly against the plant? | Compiled VCU, BMS, or motor control code | STG-2 and STG-3 |

## Layout

Planned top-level structure. Create each folder only when its first file exists.

```
tools/plant-model/
  README.md        this file
  FRAMEWORK.md     reference framework: physics, interfaces, tool stacks
  params/          vehicle parameter sets, one per configuration
  cycles/          drive cycles and scenarios (DEC-011)
  models/          component models, one per block in FRAMEWORK.md
  sim/             standalone runner and co-simulation harness
  studies/         sizing studies and their results
```

## Open items

| # | Open item | Owner |
| --- | --- | --- |
| 1 | Choose the tool stack from the options in [FRAMEWORK.md](FRAMEWORK.md#tool-stack-options). | Builder decision |
| 2 | Parameter values for every block. Each is TBD until research or a test supplies it. | STG-1 task 1b, then each cycle |
