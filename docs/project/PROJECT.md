---
id: PROJECT
status: draft
updated: 2026-10-06
---

# JoyRide project guide

How JoyRide is run. Goals are in [GOALS.md](GOALS.md), risks in [RISKS.md](RISKS.md), subsystems in [SUBSYSTEMS.md](../architecture/SUBSYSTEMS.md), and decisions in [decisions](../decisions/README.md).

## Contents

- [Charter](#charter)
- [Working principles](#working-principles)
- [Builder and constraints](#builder-and-constraints)
- [Development approach](#development-approach)
- [Subsystem cycle](#subsystem-cycle)
- [Safety](#safety)
- [Budget](#budget)
- [Rhythm and checkpoints](#rhythm-and-checkpoints)
- [Tracking artifacts to create](#tracking-artifacts-to-create)
- [Assumptions](#assumptions)

## Charter

JoyRide builds a drivable electric go-kart. Every electronic subsystem is understood, documented, and, where practical, built by the builder with open tools. The journey is the goal: success is measured by what the builder learns and records, with a working kart as the proof.

Goals:

1. Practice a lightweight development loop (research, requirements, architecture, concepts, prototype, test, refine), at system level and inside each subsystem.
2. Build breadth beyond the day job. Target areas are PCB design, RTOS firmware, motor control, CAN, battery management, 3D CAD, and web or mobile software.
3. Keep an engineering record that works as a portfolio.
4. End with a kart that drives safely at modest speed.

Non-goals: production, certification, road legality, or sale; high speed or high power; competing with commercial karts; paid tools unless nothing free works.

### Success ladder

Every level, including Spark, is a valid stopping point. The current aim is Spark ([DEC-003](../decisions/DEC-003-timeline-and-aim.md)).

| Level | Outcome | Evidence |
| --- | --- | --- |
| Spark | DRV and PACK each have a paper proof of concept and a subsystem MVP on the bench. The builder then decides whether to continue. | Journal notes, bench demos |
| Bronze | The kart moves under its own power with the safety architecture in place. Commercial parts may fill any subsystem not yet designed. | Kart MVP checkpoint, documented drive test |
| Silver | At least three subsystems (suggested: PACK, VCU, TEL) run builder-designed hardware and firmware on CAN with live telemetry. | Test reports, telemetry demo |
| Gold | A builder-designed motor controller drives the kart, with data logging and a web or mobile interface. | Drive test data, system goals traced to tests |

## Working principles

The builder's own words:

> - Safety first. Stay at low voltage (<60V), put protection in hardware, and energize in stages. The design should not present any large safety hazard to the builder or user that would require specialized PPE.
> - Prioritize cost. Design goals should start with hobbyist and commercially available parts, with low to modest capital requirements. Prefer a cheap/free prototype to a long analysis.
> - Once the core MVP (drivable kart) has been achieved, builder-defined subsystem/part/design upgrades should be as close to drop in (form, fit, function) replacements if not otherwise mentioned.
> - Document decisions when they are made, alongside rejected options and discussed paths. Part of the learning will be through mistakes and documentation.
> - Require open-source tools and standards where possible. Deviations to this will need to be addressed case-by-case, but publicly available information should be the go-to.

## Builder and constraints

- About 5 years in control systems and electrical engineering (EV startup, mining trucks): system design, schematics, HV battery and power distribution, some C++.
- Educational background in web development and data science (JavaScript, Python). Semi-novice at hobby embedded work, and a fast learner.
- Owns no electrical tools or 3D printer yet. Capital spend should be minimized.

The builder's constraints:

| Constraint | Value | Status |
| --- | --- | --- |
| Monthly budget | About $150, covering tools, parts, PCB runs, and software | Fixed, carry-forward and rollover allowed |
| Software licensing | Open source or free for personal use | Fixed |
| Voltage ceiling | Below 60 V DC at full charge | Fixed |
| Weekly time | 6 to 10 hours | Estimated |
| Workspace | A garage for the kart and a spare bedroom for subsystem work; ventilation for lithium charging and soldering still needs to be addressed | TBD |
| Timeline | About 18 months | Fixed ([DEC-003](../decisions/DEC-003-timeline-and-aim.md)) |

The repository is fully open source, with one submodule per atomic piece ([DEC-002](../decisions/DEC-002-open-source-with-submodules.md)). The documentation layout is in [CLAUDE.md](../../CLAUDE.md#layout).

## Development approach

A loose, nested version of a formal product development process. Every step is a recommendation. Skip, shorten, or reorder any step that is not helping, and note why in the journal.

1. **Stage 1, Architecture** ([STG-1](../stages/STG-1-ARCHITECTURE.md)). Runs once, is free, and takes about 3 weeks. Covers setup, rough numbers, system goals, and subsystems with rough interfaces.
2. **Stage 2, Subsystem cycles** (`STG-2-<code>`). Runs once per subsystem, in the order set by [DEC-005](../decisions/DEC-005-subsystem-order.md). Each goes from a learning burst to the smallest useful physical iteration.
3. **Stage 3, Integration** ([STG-3](../stages/STG-3-INTEGRATION.md)). Grows over time, from the bench to a drivable kart MVP. The kart MVP results from integration; it is not a prerequisite ([DEC-001](../decisions/DEC-001-no-commercial-baseline-kart.md)).

Nested, not siloed: no subsystem is defined in isolation. Every cycle reviews its neighbors' interfaces and feeds changes back into the architecture and other subsystems.

Only the system goals and the builder's fixed constraints are binding. Named parts, tools, and methods are examples until a DEC accepts them.

## Subsystem cycle

Every STG-2 document follows these seven steps. Times assume 6 to 10 hours a week. Only step 6 costs money.

| # | Step | What happens | Typical time |
| --- | --- | --- | --- |
| 1 | Learning burst | Study fundamentals, a tutorial or two, and one or two open-source projects. Aim for working vocabulary. Keep a "what I still don't understand" list. | 3 to 7 days |
| 2 | Needs and MVP sketch | Write what the subsystem must do, its key numbers, interfaces, safety concerns, and safe state. Define the subsystem MVP with a pass or fail criterion. | 1 to 2 days |
| 3 | Concepts | Compare two or three options (buy, adapt open source, build) on learning value, cost, and fit. Safety is a pass or fail screen. Log a DEC. | 1 to 3 days |
| 4 | Paper proof of concept | Test the assumption most likely to be wrong, in theory only: calculations, a model, a schematic, CAD, or a firmware design. | 1 to 2 weeks |
| 5 | Spend checkpoint | Go, adjust, or park. A good first purchase fits about one month's budget and answers one written question. | An hour |
| 6 | Subsystem MVP | Build the smallest physical version that answers the biggest open question, and judge it against the step 2 criterion. | 2 to 6 weeks |
| 7 | Fold-back | Record what was learned. Update goals, interfaces, and risks. Check enjoyment, and choose the next subsystem. | 1 to 2 days |

There are two kinds of MVP. A subsystem MVP is the smallest isolated demonstration of one subsystem's core function. The kart MVP is the first drivable kart.

The standard deliverables of every cycle are:

- journal entries
- the subsystem home (README, REQUIREMENTS, CYCLE)
- test reports
- updates to GOALS, RISKS, and SUBSYSTEMS

## Safety

The project stays survivable by keeping voltage low, putting protection in hardware, and energizing in stages.

- The design ceiling is below 60 V DC at full charge (REQ-SAF-002).
- The safe state is traction power off, reached by a hardware path without software (REQ-SAF-001).
- Fail toward de-energized: a lost signal, lost heartbeat, or watchdog trip removes torque.
- Energize in stages: a current-limited bench, then a rig with wheels off the ground, then a low-speed field test.
- Review every wiring change a second time before applying power. Never work on live circuits, and never work alone on the battery unless the [solo work safety plan](../procedures/SOLO-SAFETY.md) applies.
- Test the E-stop and the BMS cutoffs at every checkpoint.
- Never charge or store lithium cells unattended outside the designated container and area.
- A subsystem with unmet safety basics does not go on the kart.

There is no formal functional safety process. Each subsystem records its safe state, failure behavior, and hardware protections. DRV, PACK, and VCU also run a short FMEA. Risks live in [RISKS.md](RISKS.md).

JoyRide targets no certification. EV safety and battery standards are design guidance only. The builder checks local rules on where the kart may run, and insurance.

## Budget

Spend follows learning: nothing is bought before a spend checkpoint. At $150 per month with rollover, the envelope is about $2,700 over 18 months. Ranges are approximate, so check prices before buying.

| Category | Approximate range | When |
| --- | --- | --- |
| Stage 1 and every cycle's steps 1 to 5 | $0 | Always |
| First tools (multimeter, soldering gear, bench supply) | $150 to $250 | First spend checkpoint that needs them |
| Each first physical iteration | $30 to $150 | Each spend checkpoint |
| Later tools (oscilloscope, logic analyzer, hot air, 3D printer) | $350 to $550 | Only when a cycle needs one |
| Workspace and personal safety, including ventilation | $100 to $250 | Before the first lithium or high-current work |
| Kart MVP parts | $700 to $1,350 | At integration, funded by rollover |

Purchasing rules:

1. Unspent money rolls forward. The budget tracker shows the running balance.
2. Buy only after a spend checkpoint, and write down the question the purchase answers.
3. Buy used where safe (frame, bench tools). Buy new for cells, fuses, contactors, and safety gear.
4. Use dev boards before custom PCBs. Order custom boards in small batches.
5. Log every purchase with a category and a subsystem code.
6. A paid tool needs a DEC showing that no free alternative works.

## Rhythm and checkpoints

| Rhythm | Activity | Time |
| --- | --- | --- |
| Weekly | Pick tasks, check the budget, write a journal entry | About 30 minutes |
| Monthly | Review RISKS, reconcile the budget, update learning goals | About 1 hour |
| Checkpoint | Answer the checkpoint questions in a journal entry | About 30 minutes |
| End of each cycle | Retrospective on the subsystem and on the process | About 1 hour |

Checkpoints are decisions for the builder, not approvals. Their questions are in the [journal entry template](../templates/journal-entry.md).

| Checkpoint | When |
| --- | --- |
| Architecture | End of STG-1 |
| Spend | After each paper proof of concept |
| Fold-back | After each subsystem MVP |
| Kart MVP | When the first kart drives |

Rules of thumb:

- Work cycles in priority order until blocked, then run the cycle that clears the blocker ([DEC-009](../decisions/DEC-009-priority-order-with-blocker-fallback.md)).
- Time-box, then decide. If a step runs well past its estimate, shorten it or park it.
- If a step stops being fun or useful, skip it and note why.
- Do not remove a working part until its replacement works.

The project is done when three things are true. The builder declares a success level, the record matches the as-built kart, and a final retrospective is written.

## Tracking artifacts to create

Create each one only when it is needed. Prefer CSV or Markdown in this repository, with columns from the [record schemas](../templates/README.md).

| Artifact | Purpose | Create |
| --- | --- | --- |
| Roadmap | Stages, subsystem order, and checkpoints, with no fixed dates | Week 1 |
| Subsystem tracker | One row per subsystem: cycle step, next action, rough cost | Week 1 |
| Budget tracker | Monthly cap, rollover, and spend by subsystem | Week 1 |
| Shopping list | Tools and parts, empty until a cycle needs something | Week 1 |

Goals, risks, decisions, the journal, interfaces, tests, and the backlog already have homes. See [CLAUDE.md](../../CLAUDE.md#layout).

## Assumptions

Confirm or correct these in [STG-1](../stages/STG-1-ARCHITECTURE.md).

- The $150 monthly cap is firm and includes everything.
- The kart runs only on private property or a closed course.
- No MCU family, RTOS, or wireless platform is chosen yet.
- The process loosely follows the general sequence of Mattson and Sorensen's product development text.
