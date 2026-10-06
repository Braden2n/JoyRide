---
id: PROJECT
title: JoyRide project guide
status: draft
owner: Braden Toone (builder)
last_updated: 2026-10-06
source_sections: [1, 2, 3, 4, 9, 12, 13, 14, 15, 16, 17]
---

# JoyRide project guide

This document defines how JoyRide work is done. Subsystem facts live in [SUBSYSTEMS.md](../subsystems/SUBSYSTEMS.md). Stage tasks live in the [stage documents](#stages).

## Purpose and how to use these documents

JoyRide is a stepwise, nested build of an electric go-kart. Its real products are the builder's skills and a documented engineering record.

The documentation set serves two readers:

- The builder uses it as a map of what to do, in what order, and why.
- An orchestration LLM uses it as a specification for generating tracking tools later (see [Tracking artifacts to create later](#tracking-artifacts-to-create-later)).

Rules for the orchestration LLM, from the launch document:

- Treat these documents as a recommended framework, not a rulebook. The builder's latest instruction overrides them.
- Where a value is marked TBD or "placeholder", create an open item in the decision log. Do not invent a value.
- Use the ID schemes below in every artifact so items trace to each other.
- Generate tools just in time. Keep each one small enough to maintain in about 30 minutes a week.
- Do not add scope. New ideas go in the backlog tagged "parking lot".
- Ask the builder before resolving anything marked "builder decision".

Specific implementations named in these documents are illustrative examples, not decisions. That covers parts, tools, protocols, methods, and values. Only the high-level requirements and the builder's fixed constraints are binding. The system requirements are defined in [Stage 1](../stages/STG-1-ARCHITECTURE.md).

## ID schemes

Use only the prefixes that earn their keep. None are mandatory.

| Prefix | Meaning | Example |
| --- | --- | --- |
| NEED | A stakeholder need | NEED-004 |
| REQ | A requirement, tagged with a subsystem code | REQ-PACK-012 |
| SUB | A subsystem (codes in [SUBSYSTEMS.md](../subsystems/SUBSYSTEMS.md)) | SUB-PACK |
| ICD | An interface definition | ICD-CAN-001 |
| CON | A concept option for a subsystem | CON-VCU-B |
| DEC | A decision | DEC-007 |
| RSK | A risk | RSK-003 |
| TST | A test | TST-PACK-005 |
| PRT | A prototype | PRT-PACK-02 |
| LRN | A learning goal | LRN-003 |
| TSK | A backlog task | TSK-0123 |
| STG | A stage document | STG-2-DRV |

STG is not in the launch document's ID table. It was added by the builder's documentation instructions to label stage documents.

## Charter

JoyRide designs and builds a drivable electric go-kart over roughly 18 months. Every electronic subsystem is understood, documented, and, where practical, built by the builder using open tools.

The journey is the goal. Success is measured by what the builder learns and records, with a working vehicle as the proof.

### Goals

1. Practice a lightweight version of the full development loop. That loop is research, requirements, architecture, concept selection, prototype, test, and refine. Run it once at system level and again inside each subsystem.
2. Build breadth beyond the day job. Target areas are PCB design, embedded firmware with an RTOS, motor control, CAN networking, battery management, 3D CAD, and web or mobile software.
3. Keep a documented engineering record that works as a portfolio. It includes requirements, interface definitions, test reports, and a decision log.
4. End with a kart that drives safely at modest speed.

### Non-goals

- Production, certification, road legality, sale, or any manufacturing concern.
- High speed or high power. The kart is deliberately modest so mistakes stay cheap and survivable.
- Competing with commercial karts on performance or cost.
- Proprietary tools or paid software, unless a task cannot be done otherwise.

### Success ladder

| Level | Outcome | Evidence |
| --- | --- | --- |
| Spark | The first subsystems in the suggested order (DRV, then PACK) each have a paper proof of concept and a subsystem MVP on the bench. The builder then decides whether to continue. CHS is not part of Spark. | Journal notes, bench demos |
| Bronze | The kart moves under its own power with the safety architecture in place. Commercial parts may fill any subsystem the builder has not yet designed. | Kart MVP checkpoint passed, documented drive test |
| Silver | At least three subsystems (suggested: PACK, VCU, TEL) run builder-designed hardware and firmware on a CAN bus with live telemetry. | Test notes for each, telemetry demo |
| Gold | A builder-designed motor controller drives the kart, with data logging and a web or mobile interface. | Drive test data, system goals traced to tests |

Each level, including Spark, is a valid stopping point. Stopping early after learning something is a success, not a consolation prize.

### Current aim

The builder's current aim is Spark, on a timeline of about 18 months, for fun and learning.

## Working principles

These are the builder's own words, kept verbatim.

> - Safety first. Stay at low voltage (<60V), put protection in hardware, and energize in stages. The design should not present any large safety hazard to the builder or user that would require specialized PPE.
> - Prioritize cost. Design goals should start with hobbyist and commercially available parts, with low to modest capital requirements. Prefer a cheap/free prototype to a long analysis.
> - Once the core MVP (drivable kart) has been achieved, builder-defined subsystem/part/design upgrades should be as close to drop in (form, fit, function) replacements if not otherwise mentioned.
> - Document decisions when they are made, alongside rejected options and discussed paths. Part of the learning will be through mistakes and documentation.
> - Require open-source tools and standards where possible. Deviations to this will need to be addressed case-by-case, but publicly available information should be the go-to.

## Builder profile

The builder is a systems-minded engineer. Professional depth in vehicle electrical architecture is strong. The base in hobby-scale embedded, PCB, and mechanical work is thinner. The plan leans on strengths early and stretches into gaps deliberately.

- About 5 years in control systems and electrical engineering, at an EV startup and in heavy equipment (mining truck).
- That work covered systems and subsystem design, pinouts and schematics, high-voltage battery and power distribution, and some low-level C++.
- Educational background in web development and data science (JavaScript, Python).
- Semi-novice at hobby embedded work (not a beginner, not experienced), and a fast learner.
- Owns no multimeter, soldering equipment, oscilloscope, other electrical tools, or 3D printer. Capital expenditure will be required but should be minimized.

| Strong, leverage early | Stretch areas, practice deliberately |
| --- | --- |
| System and subsystem design | PCB layout for power and mixed-signal |
| Power distribution and HV safety practice | Motor control (field-oriented control) |
| Schematics, pinouts, wiring diagrams | RTOS-based firmware and driver work |
| CAN and automotive architecture | 3D CAD and mechanical design |
| Python analysis and web software | Battery state estimation algorithms |

## Constraints

These are the builder's constraints, kept as written.

| Constraint | Value | Status |
| --- | --- | --- |
| Monthly budget | About $150, covering tools, parts, PCB runs, and software | Fixed, carry-forward and rollover allowed |
| Software licensing | Open source or free for personal use | Fixed |
| Voltage ceiling | Below 60 V DC at full charge | Fixed |
| Weekly time | 6 to 10 hours | Estimated |
| Workspace | A garage for the kart and a spare bedroom for subsystem work; ventilation for lithium charging and soldering still needs to be addressed | TBD |
| Timeline | About 18 months | Fixed (builder answer) |

### Repository strategy

The builder decided on a fully open-source GitHub setup.

- A main project repository holds documentation and planning, written in Markdown.
- Each atomic piece gets its own Git submodule. Examples are embedded firmware, a shared communications library, PCB schematics, and CAD.
- Submodules are created when the work that needs them starts. None exist yet.

## Development approach

JoyRide borrows the shape of a formal product development process and applies it loosely. There is one short architecture pass, then a small learn, prove, and build cycle inside each subsystem.

Everything in this section is a recommendation. Skip, shorten, or reorder any step that is not helping, and note why in the journal.

### Three nested stages

1. Stage 1, Architecture (once, free, about 3 weeks). Set up free tools and do just enough system-level research. Write a short list of goals and split the kart into subsystems with rough interfaces. Nothing is bought.
2. Stage 2, Subsystem cycles (repeated per subsystem, in the builder's order). Each subsystem gets a mini version of the framework. It runs from a learning burst through a paper proof of concept to the smallest useful physical iteration.
3. Stage 3, Integration (grows over time). Connect subsystems as they mature, first on the bench and later on a kart. The kart MVP is a result of integration, not a prerequisite for subsystem work.

The launch document's framework diagram did not export. This text and the [stage table](#stages) replace it.

### Why nested and theory-first

The builder is new to several of these areas. Each subsystem therefore starts with a small burst of targeted learning, not up-front research on everything. That gets subsystem work started within about three weeks. Paper proofs of concept show whether a subsystem is worth building, and enjoyable, before any hardware is paid for.

### Nested, not siloed

Subsystems depend on each other, so no subsystem can be defined in complete isolation. Some conceptual work can be done alone, such as a battery state estimation algorithm. The system is still worked as a whole. Each cycle reviews its neighbors' interfaces and feeds changes back into the architecture and the other subsystems.

### What is binding

Only the high-level requirements and the builder's fixed constraints are binding. The system requirements (weight, speeds, power, energy, and so on) are defined in Stage 1. Every specific implementation named in these documents is an example to consider, not a decision.

### How the standard process is applied

| Standard step | JoyRide treatment | Weight |
| --- | --- | --- |
| Opportunity and planning | Replaced by the [charter](#charter). | Done |
| Market research and benchmarking | A light system-level pass in Stage 1, then targeted learning bursts inside each subsystem cycle. | Light |
| Customer needs | The builder is the customer. A handful of plain "I want" statements, no interviews. | Very light |
| Requirements and target specs | 10 to 15 system goals in Stage 1, then a one-page sketch per subsystem. | Light |
| Architecture and decomposition | Stage 1, revisited after every subsystem cycle. | Medium |
| Concept generation and selection | Two or three concepts per subsystem, compared informally. Formal matrices are optional. | Light |
| Prototyping | Paper proof of concept first, then the smallest physical iteration. | Core |
| Testing and refinement | Bench tests per subsystem, integration tests later, lessons folded back. | Medium |
| Design for manufacture, volume cost, launch, business case | Dropped. | None |

### Recorded decisions

| ID | Decision | Source |
| --- | --- | --- |
| DEC-001 | The project does not begin with a commercial baseline kart. Commercial parts appear later, as placeholders for subsystems that have not had their turn. | Launch section 4 (seed decision) |
| TBD | Development is fully open source, with a Git submodule per atomic piece. | Launch sections 9 and 17 (builder answer) |

The open-source decision has no DEC ID yet. Assign one when the decision log is created.

## Stages

Each stage has a stable ID and its own document. Stage documents hold the tasks and requirements. This section only defines entry and exit.

| ID | Stage | Document |
| --- | --- | --- |
| STG-1 | Architecture | [STG-1-ARCHITECTURE.md](../stages/STG-1-ARCHITECTURE.md) |
| STG-2-DRV | Subsystem cycle: motor and drive | [STG-2-DRV.md](../stages/STG-2-DRV.md) |
| STG-2-PACK | Subsystem cycle: battery pack, BMS, and power distribution | [STG-2-PACK.md](../stages/STG-2-PACK.md) |
| STG-2-CHS | Subsystem cycle: chassis and mechanical | [STG-2-CHS.md](../stages/STG-2-CHS.md) |
| STG-2-VCU | Subsystem cycle: vehicle control unit | [STG-2-VCU.md](../stages/STG-2-VCU.md) |
| STG-2-TEL | Subsystem cycle: telemetry and apps | [STG-2-TEL.md](../stages/STG-2-TEL.md) |
| STG-2-NET | Subsystem cycle: network and harness | [STG-2-NET.md](../stages/STG-2-NET.md) |
| STG-2-TMS | Subsystem cycle: thermal management (optional) | [STG-2-TMS.md](../stages/STG-2-TMS.md) |
| STG-2-RMT | Subsystem cycle: remote and wireless (optional) | [STG-2-RMT.md](../stages/STG-2-RMT.md) |
| STG-3 | Integration and the kart MVP | [STG-3-INTEGRATION.md](../stages/STG-3-INTEGRATION.md) |

### STG-1: Architecture

Stage 1 is a short, free, high-level pass that runs once. It sets up tools, gathers rough numbers, and defines the system requirements. It also splits the kart into subsystems with rough interfaces and picks a starting subsystem.

- Entry: project start. Nothing is required.
- Exit: the [architecture checkpoint](#checkpoints) is answered in the journal.

### STG-2-code: Subsystem cycles

Each subsystem runs the [subsystem cycle](#subsystem-cycle) once, in the builder's order. The cycle aims for a first working physical iteration with the least money and the most learning.

- Entry: the architecture checkpoint is done, or a previous fold-back chose this subsystem. The first four steps are free and may overlap the end of Stage 1.
- Exit: the fold-back checkpoint is answered. A cycle may also end at the spend checkpoint with a "park" decision.

### STG-3: Integration

Stage 3 connects subsystems as they mature and grows over time. Its first milestone is a drivable kart, the kart MVP. Integration is not required for Spark.

- Entry: at least two subsystems work on the bench.
- Exit for the first milestone: the [kart MVP checkpoint](#checkpoints) is answered. Upgrades continue after that.

## Subsystem cycle

Every STG-2 document follows this recommended seven-step cycle. Size each step to the builder's interest.

Times are rough calendar estimates at 6 to 10 hours a week. Every step except the subsystem MVP is free.

There are two kinds of MVP:

- A subsystem MVP (step 6) is the smallest isolated demonstration of one subsystem's core function.
- The kart MVP is the first drivable kart. It is defined in [STG-3](../stages/STG-3-INTEGRATION.md).

| # | Step | What happens | Typical time | Cost |
| --- | --- | --- | --- | --- |
| 1 | Learning burst | Study the subsystem's fundamentals: key references, a tutorial or two, and one or two open-source projects. Aim for working vocabulary, not mastery. | 3 to 7 days | Free |
| 2 | Needs and MVP sketch | One page: what the subsystem must do, key numbers, interfaces to its neighbors, and safety concerns. It also defines the subsystem MVP with a pass or fail criterion. | 1 to 2 days | Free |
| 3 | Concepts | Sketch two or three options (buy, adapt open source, build) and compare them informally. Log the choice and the rejected options. | 1 to 3 days | Free |
| 4 | Paper proof of concept | Prove the riskiest idea in theory only. Use calculations, a model, a schematic, a CAD sketch, or a firmware design. | 1 to 2 weeks | Free |
| 5 | Spend checkpoint | Decide whether to go, adjust, or park, and list the cheapest physical test. | An hour | Free |
| 6 | Subsystem MVP (first physical iteration) | Build the MVP defined in step 2. Use a dev board, a breadboard, or one small PCB. | 2 to 6 weeks | Small (see [Budget](#budget-and-purchasing)) |
| 7 | Fold-back | Write down what was learned. Update goals, interfaces, and hazards, and choose the next subsystem. | 1 to 2 days | Free |

### Tips for each step

- Learning burst: keep a running list of "what I still don't understand". It becomes the target of the paper proof of concept.
- Concepts: weigh learning value alongside cost and fit. Treat safety as a pass or fail screen. Pugh charts and decision matrices are optional tools.
- Paper proof of concept: pick the assumption most likely to be wrong and test it first.
- Spend checkpoint: a good first purchase fits inside about one month's budget and answers one written question.
- Subsystem MVP: judge it against the pass or fail criterion written in step 2. If a custom PCB is justified, order a small batch and expect a second revision.
- Fold-back: this is also the enjoyment check. If the subsystem was fun, continue. If not, note why and consider changing the order.

### Cycle rules of thumb

- Run one subsystem cycle at a time and park the others in the backlog.
- Review neighbors in every cycle. Feed interface and requirement changes back into the architecture and the other subsystems.
- A subsystem can legitimately end at the paper proof of concept.
- If a step stops being fun or useful, shorten it or skip it.
- Log each decision when it is made, with the options that were rejected.

### Deliverables per cycle

- A journal entry, a one-page needs sketch, paper proof of concept notes, and bench results.
- Updated goals, interfaces, hazard list, and budget tracker.

## Safety approach

The plan keeps the project survivable by staying at low voltage, putting protection in hardware, and energizing in stages. A hobby build has no safety team beyond the builder.

### Safety principles

- Design ceiling below 60 V DC at full charge. This keeps the kart out of the high-voltage class used in EV safety standards.
- The safe state is traction power off. A hardware path reaches it without help from software.
- Fail toward de-energized. A lost signal, a lost heartbeat, or a watchdog trip removes torque.
- Energize in stages: bench with current limit, then rig with wheels off the ground, then low-speed field test.
- Review every new wiring change a second time before applying power.
- Never work on live circuits, and never work alone on the battery.
- Test the E-stop and the BMS cutoffs at every checkpoint, not only once.
- Never charge or store lithium cells unattended outside the designated container and area.

The hardware path to the safe state, and who owns it, is described in [SUBSYSTEMS.md](../subsystems/SUBSYSTEMS.md#architecture-overview).

### Per-subsystem functional safety approach

There is no formal functional safety process. Safety practice is applied per subsystem rather than as a full-system process.

- Each subsystem records its safe state, its failure behavior, and which protections live in hardware.
- Stage 1 runs a hazard analysis and produces a seed hazard list.
- The safety-relevant subsystems (PACK, VCU, and DRV) run a short failure modes and effects analysis (FMEA) inside their cycles.
- Risks are linked to goals and tests where practical, so each mitigation gets verified.
- If useful, score each risk on a simple 5 by 5 probability and impact scale. Review the list at each checkpoint.
- A subsystem with unmet safety basics does not go on the kart.

The seed hazard and risk register lives in [SUBSYSTEMS.md](../subsystems/SUBSYSTEMS.md#seed-hazard-and-risk-register).

### Compliance

JoyRide targets no certification and no formal functional safety compliance. Standards for EV electrical safety and battery packs are read as design guidance only. The builder is responsible for checking local rules on where the kart may run, and for insurance. These documents are a plan, not a safety certification.

## Budget and purchasing

Spend follows learning. Nothing is bought until a subsystem's paper proof of concept passes its spend checkpoint. Each first physical iteration is sized to fit inside about one month's budget.

At $150 per month with rollover, the project has up to about $2,700 over the 18-month target. All figures are approximate planning ranges. Check current prices before buying.

| Category | Approximate range | When |
| --- | --- | --- |
| Stage 1 and every paper proof of concept | $0 | Setup, research, architecture, and steps 1 to 4 of every cycle |
| First tools (multimeter, soldering gear, bench power supply) | $150 to $250 | At the first spend checkpoint that needs them |
| First physical iterations (dev boards, small parts, test cells) | $30 to $150 each | At each subsystem's spend checkpoint |
| Later tools (oscilloscope, logic analyzer, hot air station, 3D printer) | $350 to $550 | Only when a cycle needs one |
| Workspace and personal safety (including ventilation) | $100 to $250 | Before the first lithium or high-current work |
| MVP kart parts (used frame, placeholder motor and controller, pack, contactor, fuses, wiring) | $700 to $1,350 | After several subsystems work, at the MVP stage |

The builder can stop after any row without having committed to the next. Each subsystem's rough first spend is listed in [SUBSYSTEMS.md](../subsystems/SUBSYSTEMS.md#subsystem-summary).

### Indicative pacing

- Weeks 1 to 3: no spend. Stage 1 runs while the first learning bursts and paper proofs of concept start.
- From the first passed spend checkpoint: roughly one first physical iteration every one to two months, plus tools as needed.
- MVP kart parts are bought when enough subsystems work, funded by rollover from earlier months.

### Purchasing rules (suggested)

1. The monthly cap is $150. Unspent money rolls forward, and the budget tracker shows the running balance.
2. Buy only after a spend checkpoint, and write down the question the purchase answers.
3. Buy used where it is safe (frame, bench tools). Buy new for cells, fuses, contactors, and safety gear.
4. Use dev boards and breakouts before custom PCBs. Order custom boards in small batches when the learning value is high.
5. Log every purchase with a category and a subsystem code.

### Software cost policy

Everything runs on free or open-source tools. Examples named in the launch document are KiCad, FreeCAD or Onshape free tier, PlatformIO or STM32CubeIDE, FreeRTOS or Zephyr, SavvyCAN, PulseView, and Python. Any paid tool needs a DEC entry that shows no free alternative works.

## Learning goals and skills

Learning is the product. Each skill area has a target level and a place where it gets practiced, with a repository artifact as evidence.

Starting levels for areas the builder did not describe are assumptions. The builder should confirm or correct them.

| Skill area | Starting level (confirm) | Target by project end | Practiced in |
| --- | --- | --- | --- |
| Requirements and systems engineering | Strong in practice | A light but traceable process run at system and subsystem level | STG-1 |
| Power distribution and HV safety | Strong | Own pack power path with precharge, contactors, and fault handling | STG-2-PACK |
| Schematic capture and PCB layout (KiCad) | Assumed moderate | Multi-layer power and mixed-signal boards that work on rev B | STG-2-NET, STG-2-PACK, STG-2-DRV |
| Embedded C/C++, drivers, RTOS | Some | Drivers and RTOS applications on several nodes | STG-2-VCU, STG-2-PACK, STG-2-NET |
| CAN and vehicle networking | Likely strong | DBC-driven network with diagnostics and a gateway | STG-2-NET |
| Battery management and state estimation | Assumed moderate | Own BMS with a state of charge estimator tested against data | STG-2-PACK |
| Motor control (FOC) | Assumed new | Working field-oriented control on a self-built inverter | STG-2-DRV |
| 3D CAD and mechanical design | Assumed new | Enclosures and brackets that fit first or second try | STG-2-CHS |
| Web and mobile software | Educational background | Live telemetry dashboard and a configuration app | STG-2-TEL |
| Test and verification practice | Moderate | Written test procedures, fault injection, and automated analysis | All |

Some targets reach beyond the current Spark aim. Examples are FOC on a self-built inverter and multi-layer boards. They describe the full ladder, not the Spark scope.

### Seed learning goals

Each LRN item gets an evidence field when the learning tracker is created.

| ID | Learning goal | Evidence |
| --- | --- | --- |
| LRN-001 | Take a board from schematic to ordered, assembled, and debugged. | Bring-up report |
| LRN-002 | Write a DBC and use it across at least three nodes and a logger. | TBD |
| LRN-003 | Build firmware with an RTOS and a layered driver structure on two different boards. | TBD |
| LRN-004 | Characterize a cell and fit a battery model in Python. | TBD |
| LRN-005 | Implement and compare two state of charge estimators on logged data. | TBD |
| LRN-006 | Design and test a precharge and contactor circuit with fault handling. | TBD |
| LRN-007 | Run a Pugh chart and a weighted decision matrix and record the decision. | TBD |
| LRN-008 | Run a fault-injection test campaign and close every finding. | TBD |
| LRN-009 | Run field-oriented control on a motor, first with open-source firmware, then with own hardware. | TBD |
| LRN-010 | Complete one subsystem cycle, from learning burst to fold-back, and change the process as a result. | TBD |

## Tracking artifacts to create later

None of these exist yet. Create the starter set (rows 1 to 10) in the first week. Create the rest only when a stage or cycle needs them.

Each tool should ship with a one-paragraph usage note, column definitions, and one example row. Prefer plain formats that live in the repository. Use the ID schemes and dropdowns for status (Not started, In progress, Blocked, Done). Where a value is a placeholder, mark the cell "TBD, builder decision".

| # | Artifact | Format | Purpose | Create | Update |
| --- | --- | --- | --- | --- | --- |
| 1 | Master roadmap | Spreadsheet or board | Stages, subsystem order, and checkpoints, with no fixed dates | Week 1 | Weekly |
| 2 | Backlog and task board | Project board or sheet | Tasks with subsystem and cycle-step fields | Week 1 | Weekly |
| 3 | Subsystem tracker | Spreadsheet | One row per subsystem with cycle step, next action, and rough cost | Week 1 | Weekly |
| 4 | Budget and purchase tracker | Spreadsheet | Monthly cap, rollover, and spend by subsystem | Week 1 | On purchase |
| 5 | Journal and decision log | Markdown | Dated entries and rejected options | Week 1 | Weekly |
| 6 | Risk and hazard list | Spreadsheet | The living version of the seed register | Week 1 | Monthly |
| 7 | Learning tracker | Spreadsheet | LRN items with evidence links | Week 1 | Monthly |
| 8 | Tool and equipment shopping list | Spreadsheet | Empty until a cycle needs something | Week 1 | On purchase |
| 9 | Repository structure and README conventions | Markdown | How the repository and submodules are laid out | Week 1 | As needed |
| 10 | Checkpoint templates | Markdown | One page each for architecture, spend, fold-back, and kart MVP | Week 1 | At each checkpoint |
| 11 | System goals list | Spreadsheet | Goals with a subsystem tag on each | Stage 1 | As needed |
| 12 | Interface notes and DBC skeleton | Markdown, CSV, DBC | Interfaces between subsystems | Stage 1 | Per change |
| 13 | Subsystem one-pager | Markdown template | Needs sketch, concepts, paper proof of concept notes, results | Start of each cycle | During the cycle |
| 14 | Test log and report template | Spreadsheet plus Markdown | Test records | First physical iteration | Per test |

Orchestrator behavior when creating these:

- Before generating any tool, list open assumptions and questions and ask the builder to confirm the ones that change structure.
- After generating the starter set, write a short note on which IDs flow into which tool.
- When the builder completes a checkpoint, update the affected tools instead of creating duplicates.

## Rhythm and checkpoints

The project runs on a light weekly rhythm and four short checkpoints. It can be paused at any checkpoint without losing work.

### Cadence

| Rhythm | Activity | Time |
| --- | --- | --- |
| Weekly | Look at the backlog, pick next week's tasks, check the budget, and write a short journal entry | About 30 minutes |
| Monthly | Skim the hazard list, reconcile the budget, and update the learning tracker | About 1 hour |
| Each checkpoint | A few lines in the journal answering the checkpoint questions | About 30 minutes |
| End of each subsystem cycle | A short retrospective on the subsystem and on the process | About 1 hour |

### Checkpoints

Each checkpoint is a few lines in the journal. Each is a decision for the builder, not an approval.

| Checkpoint | When | Questions to answer in a few lines |
| --- | --- | --- |
| Architecture | End of STG-1 | Can I name every subsystem and what it does? Which subsystem do I start with, and why? Do I have a rough cost for each? Is anything still unclear enough to stop me from starting? |
| Spend | After each paper proof of concept | Does the paper proof hold up? What is the cheapest physical test, and does it fit one month's budget? Do I still want to build this? Go, adjust, or park. |
| Fold-back | After each subsystem MVP | Did the MVP meet its pass or fail criterion? What did I learn? What changes in the architecture or interfaces? Was it fun, and what comes next? |
| Kart MVP | When the first kart drives | Does it drive safely at low speed? Have the E-stop and the BMS cutoffs been tested? Do my notes match the kart as built? Which placeholder do I replace first? |

The architecture and kart MVP rows merge the question lists from launch sections 8, 11, and 16.

### Project rules of thumb

- Time-box, then decide. If a step runs well past its estimate, shorten it or park it.
- Spend only after a spend checkpoint.
- Run one subsystem cycle at a time.
- If a step stops being fun or useful, skip it and note why.
- Keep a working baseline. Do not remove a working part until its replacement works.
- A subsystem with unmet safety basics does not go on the kart.
- After each subsystem cycle, write a short process retrospective. Note what research was wasted, what was worth it, and what to change.

### Definition of done

The project is done when three things are true:

1. The builder declares a success level (Spark, Bronze, Silver, or Gold).
2. The engineering record matches the as-built kart.
3. A final retrospective is written.

Stopping at any level is a legitimate end.

## Assumptions and builder answers

The plan rests on a handful of assumptions. The builder should confirm or correct them before tracking tools are built.

### Assumptions

- The $150 monthly cap is firm and includes everything, with unspent money rolling over.
- The voltage ceiling is below 60 V DC at full charge.
- The builder has 6 to 10 hours a week.
- The builder has a workspace where lithium cells can be handled and charged safely. See the flagged contradiction below.
- The kart runs only on private property or a closed course.
- No MCU family, RTOS, or wireless platform is chosen yet. Examples are options for the relevant subsystem cycle to decide.
- The framework follows the general sequence of Mattson and Sorensen's text, applied loosely. Chapter-level mapping should be checked against the book.

### Builder answers

| Question | Answer |
| --- | --- |
| Workspace | A garage for the kart and a spare bedroom for subsystem work. Ventilation for lithium and soldering is not good and must be addressed later. |
| Timeline and aim | About 18 months, with Spark as the current aim, mainly for fun and learning. |
| Starting subsystem | The recommended order in [SUBSYSTEMS.md](../subsystems/SUBSYSTEMS.md#subsystem-summary): DRV first. |
| Battery source | A pack assembled from cells is the preference, still to be decided in STG-2-PACK. |
| Openness | Fully open source, with a Git submodule for each atomic piece. |
| Driver mass, kart mass, top speed | Starting inputs only: about a 300 lb driver, a 200 lb kart, and about 30 mph. Stage 1 confirms or changes them. |

### Gaps and contradictions in the launch document

These are flagged, not resolved. Each needs a builder decision.

| # | Issue | Where | Suggested handling |
| --- | --- | --- | --- |
| 1 | The assumptions say a safe lithium workspace exists. The builder's answer says ventilation is poor. | Sections 3, 17 | Treat the workspace as TBD until the STG-1 safety plan is done. |
| 2 | "Never work alone on the battery" conflicts with a single-person project. | Section 12 | Builder decision: how to meet this rule for PACK work. |
| 3 | "Run one subsystem cycle at a time" conflicts with starting DRV and PACK paper proofs in the first week. | Sections 9, 10, 16 | Builder decision. The stage documents keep DRV first and PACK second. |
| 4 | First physical iterations are budgeted at $30 to $150 each. DRV and PACK first spends can reach $400 and $250. | Sections 10, 13 | Decide at each spend checkpoint, using rollover. |
| 5 | REQ-SAF-001 and REQ-COST-001 use codes that are not subsystem codes. | Sections 1, 7, 8 | Keep the IDs. Owners are proposed in STG-1. |
| 6 | The section 7 goals list has no subsystem tags yet. | Section 7 | Tags in SUBSYSTEMS.md are proposals for Stage 1 to confirm. |
| 7 | "Stage review" and "P0" are used but never defined. | Sections 12, 14 | Read "stage review" as checkpoint. "P0" was not carried over. |
| 8 | The CHS MVP mentions a printed mock-up, but the builder owns no 3D printer. | Sections 3, 10 | Cardboard is the default until a printer is justified. |
| 9 | Both embedded diagrams did not export. | Sections 4, 8 | Text descriptions replace them. |
