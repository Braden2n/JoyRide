# Project JoyRide — Launch Document

Oct 5, 2026 · @Braden Toone

## 1. Purpose and how to use this document

This document is the single source of truth for Project JoyRide, a stepwise, nested build of an electric go-kart whose real products are the builder's skills and a documented engineering record.

It serves two readers. The builder uses it as a map of what to do, in what order, and why. An orchestration LLM uses it as a specification for generating the project's tracking tools (section 15).

**Rules for the orchestration LLM**

- Treat this document as a recommended framework, not a rulebook, and let the builder's latest instruction override it. Where a value is marked TBD or "placeholder", create an open item in the decision log; do not invent a value.
- Use the ID schemes below in every artifact so items trace to each other.
- Generate tools just in time (section 15 gives the order), and keep each one small enough to maintain in about 30 minutes a week.
- Do not add scope. New ideas go in the backlog tagged "parking lot".
- Ask the builder before resolving anything marked "builder decision".

Specific implementations named in this document (parts, tools, protocols, methods, and values) are illustrative examples, not decisions. Only the high-level requirements and the builder's fixed constraints are binding, and the system requirements (weight, speeds, power, energy, and so on) are defined in Stage 1.

**ID scheme****s**

| Prefix | Meaning | Example |
| --- | --- | --- |
| NEED | A stakeholder need | NEED-004 |
| REQ | A requirement, tagged with a subsystem code | REQ-PACK-012 |
| SUB | A subsystem (codes in section 8) | SUB-PACK |
| ICD | An interface definition | ICD-CAN-001 |
| CON | A concept option for a subsystem | CON-VCU-B |
| DEC | A decision | DEC-007 |
| RSK | A risk | RSK-003 |
| TST | A test | TST-PACK-005 |
| PRT | A prototype | PRT-PACK-02 |
| LRN | A learning goal | LRN-003 |
| TSK | A backlog task | TSK-0123 |

Use only the prefixes that earn their keep; none are mandatory. The work is organized as three nested stages (section 4), with a short cycle inside each subsystem (section 9).

## 2. Project charter

Over roughly 18 months, JoyRide designs and builds a drivable electric go-kart in which every electronic subsystem is understood, documented, and, where practical, built by the builder using open tools.

The journey is the goal. Success is measured by what the builder learns and records, with a working vehicle as the proof.

**Goals**

1. Practice a lightweight version of the full development loop (research, requirements, architecture, concept selection, prototype, test, refine), once at system level and again inside each subsystem.
2. Build breadth beyond the day job: PCB design, embedded firmware with an RTOS, motor control, CAN networking, battery management, 3D CAD, and web or mobile software.
3. Keep a documented engineering record (requirements, interface definitions, test reports, decision log) that works as a portfolio.
4. End with a kart that drives safely at modest speed.

**Non-goals**

- Production, certification, road legality, sale, or any manufacturing concern.
- High speed or high power. The kart is deliberately modest so mistakes stay cheap and survivable.
- Competing with commercial karts on performance or cost.
- Proprietary tools or paid software, unless a task cannot be done otherwise.

**Success ladder**

| Level | Outcome | Evidence |
| --- | --- | --- |
| Spark | The first subsystems in the suggested order (DRV, then PACK) each have a paper proof of concept and a subsystem MVP on the bench, and the builder decides whether to continue. CHS is not part of Spark. | Journal notes, bench demos |
| Bronze | The kart moves under its own power with the safety architecture in place; commercial parts may fill any subsystem the builder has not yet designed | Kart MVP checkpoint passed, documented drive test |
| Silver | At least three subsystems (suggested: PACK, VCU, TEL) run builder-designed hardware and firmware on a CAN bus with live telemetry | Test notes for each, telemetry demo |
| Gold | A builder-designed motor controller drives the kart, with data logging and a web or mobile interface | Drive test data, system goals traced to tests |

Each level, including Spark, is a valid stopping point. Stopping early after learning something is a success, not a consolation prize. The builder's current aim is Spark, on a timeline of about 18 months, for fun and learning.

**Working principles**

- Safety first. Stay at low voltage (<60V), put protection in hardware, and energize in stages. The design should not present any large safety hazard to the builder or user that would require specialized PPE.
- Prioritize cost. Design goals should start with hobbyist and commercially available parts, with low to modest capital requirements. Prefer a cheap/free prototype to a long analysis.
- Once the core MVP (drivable kart) has been achieved, builder-defined subsystem/part/design upgrades should be as close to drop in (form, fit, function) replacements if not otherwise mentioned.
- Document decisions when they are made, alongside rejected options and discussed paths. Part of the learning will be through mistakes and documentation.
- Require open-source tools and standards where possible. Deviations to this will need to be addressed case-by-case, but publicly available information should be the go-to.

## 3. Builder profile, constraints, and resources

The builder is a systems-minded engineer with strong professional depth in vehicle electrical architecture and a thinner base in hobby-scale embedded, PCB, and mechanical work, so the plan leans on strengths early and stretches into gaps deliberately.

**Builder profile**

- About 5 years in control systems and electrical engineering at an EV startup and in heavy equipment (mining truck): systems and subsystem design, pinouts and schematics, high-voltage battery and power distribution, some low-level C++.
- Educational background in web development and data science (JavaScript, Python).
- Semi-novice at hobby embedded work (not a beginner, not experienced), and a fast learner.
- Owns no multimeter, soldering equipment, oscilloscope, other electrical tools, or 3D printer. Capital expenditure will be required, but should be minimized where possible

**Constraints**

| Constraint | Value | Status |
| --- | --- | --- |
| Monthly budget | About $150, covering tools, parts, PCB runs, and software | Fixed, carry-forward and rollover allowed |
| Software licensing | Open source or free for personal use | Fixed |
| Voltage ceiling | Below 60 V DC at full charge | Fixed |
| Weekly time | 6 to 10 hours | Estimated |
| Workspace | A garage for the kart and a spare bedroom for subsystem work; ventilation for lithium charging and soldering still needs to be addressed | TBD |

**Where the builder starts**

| Strong, leverage early | Stretch areas, practice deliberately |
| --- | --- |
| System and subsystem design | PCB layout for power and mixed-signal |
| Power distribution and HV safety practice | Motor control (field-oriented control) |
| Schematics, pinouts, wiring diagrams | RTOS-based firmware and driver work |
| CAN and automotive architecture | 3D CAD and mechanical design |
| Python analysis and web software | Battery state estimation algorithms |

## 4. Development approach

JoyRide borrows the shape of a formal product development process (research, requirements, concepts, prototypes, refinement) and applies it as a loose, nested framework: one short architecture pass, then a small learn, prove, and build cycle inside each subsystem.

Everything in sections 4 to 11 is a recommendation. Skip, shorten, or reorder any step that is not helping, and note why in the journal.

**Three nested stages**

1. Stage 1, Architecture (once, free, about 3 weeks): set up free tools, do just enough system-level research, write a short list of goals, and split the kart into subsystems with rough interfaces. Nothing is bought.
2. Stage 2, Subsystem cycles (repeated per subsystem, in the builder's order): each subsystem gets a mini version of the framework, from a learning burst through a paper proof of concept to the smallest physical iteration that answers an open question.
3. Stage 3, Integration (grows over time): connect subsystems as they mature, first on the bench and later on a kart. The first drivable kart (the kart MVP) is a result of integration, not a prerequisite for subsystem work.

&#91;embedded content: JoyRide framework · 3 nested stages, 7-step subsystem cycle\]

The Stage 2 cycle repeats for each subsystem, and the highlighted spend checkpoint is the only point where money enters.

**Why nested and theory-first**

The builder is new to several of these areas, so each subsystem starts with a small burst of targeted learning instead of up-front research on everything. That also gets subsystem work started within about three weeks. Paper proofs of concept show whether a subsystem is worth building, and enjoyable, before any hardware is paid for.

Seed decision DEC-001: the project does not begin with a commercial baseline kart. Commercial parts appear later, as placeholders for subsystems that have not had their turn.

**Nested, not siloed**

Subsystems depend on each other, so a lot of cross-subsystem work is needed and no subsystem can be defined in complete isolation. Some conceptual work can be done alone, such as a battery state estimation algorithm, but the system is worked as a whole: each cycle reviews its neighbors' interfaces and feeds changes back into the architecture and the other subsystems.

**What is binding**

Only the high-level requirements and the builder's fixed constraints are binding. The system requirements (weight, speeds, power, energy, and so on) are defined in Stage 1, and every specific implementation named in this document is an example to consider, not a decision.

**How the standard process is used**

| Standard step | JoyRide treatment | Weight |
| --- | --- | --- |
| Opportunity and planning | Replaced by the charter (section 2). | Done |
| Market research and benchmarking | A light system-level pass in Stage 1, then targeted learning bursts inside each subsystem cycle. | Light |
| Customer needs | The builder is the customer. A handful of plain "I want" statements, no interviews. | Very light |
| Requirements and target specs | 10 to 15 system goals in Stage 1, then a one-page sketch per subsystem. | Light |
| Architecture and decomposition | Stage 1, revisited after every subsystem cycle. | Medium |
| Concept generation and selection | Two or three concepts per subsystem, compared informally. Formal matrices are optional. | Light |
| Prototyping | Paper proof of concept first, then the smallest physical iteration. | Core |
| Testing and refinement | Bench tests per subsystem, integration tests later, lessons folded back. | Medium |
| Design for manufacture, volume cost, launch, business case | Dropped. | None |

**Checkpoints instead of gates**

Four short checkpoints (architecture, spend, fold-back, and kart MVP) replace formal gates. Each is a few lines in the journal answering a handful of questions, and each is a decision for the builder rather than an approval (section 16).

## 5. Stage 1a: Setup (a few days, free)

Setup costs nothing but time: install free tools, create the repository, and start the journal before any hardware is bought.

**Objective:** be able to learn, simulate, and take notes on a computer from day one.

**Recommended activities**

1. Create a fully open-source GitHub setup: a main project repository for documentation and planning, plus a Git submodule for each atomic piece (embedded firmware, a shared communications library, PCB schematics, CAD, and so on), with documentation in Markdown.
2. Install free or open-source tools as they become useful, for example KiCad (with ngspice), FreeCAD or an Onshape free tier, and Python with Jupyter. Embedded toolchains (PlatformIO or STM32CubeIDE) can wait until the first physical iteration.
3. Start the journal and the decision log, even as plain text files.
4. Sketch a workspace safety plan on paper: where lithium cells would be charged and stored, ventilation, and fire response. The garage (kart) and spare bedroom (subsystem work) lack good ventilation for lithium and soldering, so plan a fix before the first physical iteration. Buy nothing yet.
5. Start an empty tool shopping list. Items go on it only when a subsystem cycle needs them.

**Deliverables**

- Repository, journal, decision log, and an empty shopping list.
- A one-paragraph workspace safety note.

**Done when** the builder can open KiCad, run a Python notebook, and commit a journal entry.

## 6. Stage 1b: System-level research (about 1 week)

System-level research only needs to answer the questions that shape the architecture; subsystem details wait for each subsystem's own learning burst.

**Objective:** get rough numbers and a feel for what exists, without going deep on any one subsystem.

**Suggested research streams**

Spend roughly 3 to 4 hours on each and finish with a short note on what it means for JoyRide.

| Stream | Question to answer | Output |
| --- | --- | --- |
| Reference builds | What do successful DIY electric karts and small EVs use for frame, motor, voltage, and battery, and what went wrong for others? | Benchmark table of 3 to 5 builds |
| Drivetrain sizing | What power, voltage, gearing, and energy give a useful top speed and run time for the builder's starting inputs (about 300 lb driver, 200 lb kart, about 30 mph), which Stage 1 turns into system requirements? | Python sizing model v0 |
| Safety basics | What are the main hazards below 60 V DC, and which protections matter most? | Seed hazard list |
| Open-source landscape | Which open projects exist for motor control, battery management, CAN tools, and dashboards? | Link list per subsystem (names only, study later) |

Defer detailed research on silicon choices, cell chemistry, frames, and local rules to the subsystem cycle that needs them.

**Deliverables**

- Benchmark table, sizing model v0, seed hazard list, and the open-source link list.

**Done when** the builder has rough numbers for power, pack voltage, and energy, plus a short hazard list. Rough is fine; the models get refined inside the subsystem cycles.

## 7. Stage 1c: System goals (3 to 4 days)

A short list of system-level goals, not a formal specification, keeps later subsystem work pointed in the same direction. Stage 1 is where the system requirements (weight, speeds, power, energy, run time, and so on) are defined, using the sizing model from the research step.

**Objective:** write down what the kart should do in numbers loose enough to change, so every subsystem has something to aim at.

**Suggested approach**

1. List 8 to 12 plain "I want..." statements covering driving, learning, safety, and cost, and mark each as a must-have or a nice-to-have.
2. Turn them into 10 to 15 system goals, each with a target, a minimum, and (if useful) how it would be checked.
3. Tag each goal with the subsystem most responsible for it. Subsystems add their own sketches later (section 9).

Treat the list as a living draft. Change a goal whenever a subsystem cycle teaches something, and jot down why.

**Illustrative starting goals**

These are goal themes, not specifications. The builder's starting inputs are shown for reference, and Stage 1 sets every value.

| ID | Goal | Target | How to check |
| --- | --- | --- | --- |
| REQ-SYS-001 | The kart reaches a useful top speed on level pavement | Defined in Stage 1 (builder's starting input: about 30 mph) | GPS test |
| REQ-SYS-002 | The kart runs long enough for a useful session | Defined in Stage 1 | Test |
| REQ-SYS-003 | The kart carries its design load, driver plus kart | Defined in Stage 1 (starting inputs: about 300 lb driver, about 200 lb kart) | Test and analysis |
| REQ-SYS-004 | Power and energy are sized for the speed, load, and run time above | Defined in Stage 1 from the sizing model | Analysis and test |
| REQ-PACK-001 | The battery stays below the shock-hazard voltage ceiling at full charge | Below 60 V DC (fixed constraint) | Measurement |
| REQ-PACK-002 | The battery system protects its cells and disconnects safely on faults | Fault list defined in the PACK cycle | Fault-injection test |
| REQ-SAF-001 | An emergency stop removes traction power independent of software | Hardware path only | Test and inspection |
| REQ-VCU-001 | A single sensor or software fault cannot command unintended acceleration | Fault behavior defined in the VCU cycle | Fault-injection test |
| REQ-NET-001 | Subsystems communicate over a shared network | Protocol and rates defined during subsystem work | Test |
| REQ-COST-001 | Spend stays within the budget plan (section 13) | $150 per month, rollover allowed | Budget tracker |

**Deliverables**

- A plain-language wants list and a goals list with a subsystem tag on each goal.

**Done when** the builder is happy that the goals describe the kart they want. They do not need to be perfect.

## 8. Stage 1d: Architecture and subsystem definition (about 1 week)

Stage 1d splits the kart into six subsystems with rough interfaces, so each can be learned, designed, bought, or replaced independently.

**Objective:** split the kart into subsystems, sketch how they connect, and choose where to start.

**Activities**

1. Functional decomposition: list what the kart must do (store energy, distribute and protect power, convert electrical to mechanical power, read driver intent, stop safely, communicate, inform the driver, carry loads) and map each function to a subsystem.
2. Architecture style: one central vehicle control unit plus CAN nodes, with a gateway to wireless. Three to five nodes is plenty to start.
3. Safety approach v0: no formal functional safety process. Each subsystem documents its safe state, its failure behavior, and where its protections live. At system level, define the overall safe state (traction power off) and the hardware path that reaches it: BMS-controlled contactors plus a mechanical E-stop loop.
4. Interface sketches: for each pair of subsystems that touch, jot down the power, data (rough CAN message ideas), mechanical, and human interfaces. Formalize them as interface definitions only when it helps.
5. Define the kart MVP and the starting point: describe what the first drivable kart needs, which subsystems may be commercial placeholders, and which subsystem to start with (section 10 records the builder's order).

&#91;embedded content: JoyRide architecture · 6 subsystems, 1 CAN bus\]

Solid arrows carry power, the thick band is the CAN bus, the dashed accent line is the hardware E-stop path, dashed grey lines are wireless links, and dashed boxes are optional additions.

**Subsystems**

| Code | Subsystem | Responsibilities | Boundaries and suggested starting point |
| --- | --- | --- | --- |
| CHS | Chassis and mechanical | Frame, steering, brakes, mounts, enclosures, mass distribution | Mount points for PACK and DRV set the integration details. Brakes work independently of the electrics. Design brackets in CAD and buy a used frame late, at integration. Not part of Spark. |
| PACK | Battery pack, BMS, and power distribution | Cells, cell monitoring and balancing, protection, state of charge estimation; main fuse, contactors, and precharge; HVIL and IMD only if determined necessary; mechanical E-stop loop | The power distribution unit is physically part of the pack. The BMS has authority over the contactors and precharge, and the mechanical E-stop loop works independently of software. Assembling the pack from cells is the current preference. |
| DRV | Motor and drive | Motor, controller or inverter, gearing, torque output | Takes torque requests from the VCU over CAN and power through the PACK contactors. Its paper proof of concept doubles as a go or no-go check on the system goals. Commercial motor and controller first, own controller later. |
| VCU | Vehicle control unit | Throttle processing, torque request, driving modes, state machine, fault handling, derate strategy, simple driver-facing LEDs | Owns the application-layer logic and state, including the driver-facing HMI role. Reads PACK state, commands DRV, reports to TEL. Own design on a dev board. |
| NET | Network and harness | CAN bus, DBC, message and interface contracts, connectors, wiring diagrams, labeling | Interfaces are mostly defined during other subsystems' cycles, and NET records them as contracts. |
| TEL | Telemetry and apps | Data logging, detailed and debug information, web or mobile dashboards, analysis in Python | Listens on CAN and is the hub for monitoring and validation. Detailed driver and debug information lives here, not on the kart. |
| TMS (optional) | Thermal management | Passive cooling with monitoring and a derate strategy | Not a subsystem unless monitoring shows it is needed. Monitoring sits in PACK and DRV, and derating in the VCU. |
| RMT (optional) | Remote and wireless | Remote kill, speed limiting, wireless configuration | Parking-lot idea, considered only after the core subsystems. |

The detailed design of the BMS's authority over contactors, precharge, and any HVIL or IMD belongs in the PACK stage documents. At this level, it is enough to record who owns each responsibility. Starting points in the table are suggestions, not decisions.

**Deliverables**

- Architecture diagram and a subsystem list with a one-line responsibility each.
- Rough interface sketches and a DBC skeleton (optional).
- Safety concept v0 and an updated hazard list.
- Rough cost per subsystem, so spending stays a choice.
- The MVP definition and the chosen starting subsystem.

**Architecture checkpoint** (a few lines in the journal)

- Can I name each subsystem and what it is responsible for?
- Have I chosen the subsystem to start with, and do I know why?
- Do I have a rough cost for each subsystem?
- Is anything still unclear enough to stop me from starting?

## 9. Stage 2: The subsystem cycle (repeat for each subsystem)

Each subsystem runs the same short cycle, sized to the builder's interest: learn a little, sketch what it must do, try ideas on paper, decide whether to spend, build the smallest physical version, and fold the lessons back.

**Objective:** reach a first working physical iteration of each subsystem with the least money and the most learning.

**The cycle (recommended)**

Times are rough calendar estimates at 6 to 10 hours a week. Every step except the subsystem MVP is free. There are two kinds of MVP: a subsystem MVP (step 6), the smallest isolated demonstration of one subsystem's core function, and the kart MVP (section 11), the first drivable kart.

| # | Step | What happens | Typical time | Cost |
| --- | --- | --- | --- | --- |
| 1 | Learning burst | Study the subsystem's fundamentals: key references, a tutorial or two, and one or two open-source projects. Aim for working vocabulary, not mastery. | 3 to 7 days | Free |
| 2 | Needs and MVP sketch | One page: what the subsystem must do, key numbers, interfaces to its neighbors, safety concerns, and the subsystem MVP: the smallest isolated demonstration of its core function, with a pass or fail criterion. | 1 to 2 days | Free |
| 3 | Concepts | Sketch two or three options (buy, adapt open source, build) and compare them informally. Log the choice and the rejected options. | 1 to 3 days | Free |
| 4 | Paper proof of concept | Prove the riskiest idea in theory only: calculations, a Python or ngspice model, a KiCad schematic, a CAD sketch, or a firmware design. | 1 to 2 weeks | Free |
| 5 | Spend checkpoint | Decide whether to go, adjust, or park, and list the cheapest physical test. | An hour | Free |
| 6 | Subsystem MVP (first physical iteration) | Build the MVP defined in step 2: the smallest physical version that answers the biggest open question, on a dev board, a breadboard, or one small PCB. | 2 to 6 weeks | Small (section 13) |
| 7 | Fold-back | Write down what was learned, update goals, interfaces, and hazards, and choose the next subsystem. | 1 to 2 days | Free |

**Tips for each step**

- Learning burst: keep a running list of "what I still don't understand". It becomes the target of the paper proof of concept.
- Concepts: weigh learning value alongside cost and fit, and treat safety as a pass or fail screen. Pugh charts and decision matrices are optional tools, not requirements.
- Paper proof of concept: pick the assumption most likely to be wrong and test it first. For example: will this motor reach the target torque at this pack voltage, or does this BMS front end cover the protections needed?
- Spend checkpoint: a good first purchase fits inside about one month's budget and answers one written question.
- Subsystem MVP: judge it against the pass or fail criterion written in step 2. If a custom PCB is justified, order a small batch and expect a second revision.
- Fold-back: this is also the enjoyment check. If the subsystem was fun, continue; if not, note why and consider changing the order.

**Rules of thumb**

- Run one subsystem cycle at a time and park the others in the backlog.
- Review neighbors in every cycle. No subsystem is defined in complete isolation, so interface and requirement changes found in one cycle are fed back into the architecture and the other subsystems.
- A subsystem can legitimately end at the paper proof of concept.
- If a step stops being fun or useful, shorten it or skip it.
- Log each decision when it is made, with the options that were rejected.

**Decisions that will come up**

| Decision | Options to consider | Comes up in |
| --- | --- | --- |
| Nominal pack voltage | 24 V, 36 V, 48 V | PACK and DRV |
| Cell chemistry and pack source | Li-ion cells assembled by the builder (current preference), LiFePO4, or a commercial pack with its own BMS | PACK |
| Motor and controller for the kart MVP | Commercial BLDC kit, hub motor, brushed DC | DRV |
| MCU family and RTOS | STM32 with FreeRTOS or Zephyr, ESP32 for wireless, bare metal for simple nodes | NET and VCU |
| Dashboard approach | LEDs only, a small embedded display, a phone or laptop web app | VCU and TEL |
| Frame | Used kart frame, kit frame, custom welded | CHS |
| Charging approach | Commercial charger, builder-designed charger | PACK |
| Open or closed development | Decided: fully open source, with Git submodules per atomic piece | Any time |

**Deliverables per cycle**

- A journal entry, a one-page needs sketch, paper proof of concept notes, and bench results.
- Updated goals, interfaces, hazard list, and budget tracker.

## 10. Stage 2: Starter guide for each subsystem

Every subsystem has a suggested learning burst, a paper proof of concept idea, and a subsystem MVP that can be built in isolation, listed here in the builder's recommended order.

Spend figures are approximate, check current prices, and exclude shared tools such as a multimeter (section 13). The Spark level covers the first two rows. All tools, parts, protocols, and methods named here are examples to consider, not decisions.

| Subsystem | Learning burst topics | Paper proof of concept idea | Subsystem MVP (isolated) | Rough first spend |
| --- | --- | --- | --- | --- |
| DRV | BLDC and PMSM basics, commutation, field-oriented control, current sensing, motor and controller specifications, SimpleFOC and VESC documentation | Size motor and gearing against the Stage 1 system requirements, shortlist motor and controller pairs, check pack voltage and current compatibility, and make a go or no-go call on the system goals | The chosen motor and controller, or a small learning motor, spun from a bench supply at low voltage with logged speed and current and a safe stop | $40 to $90 (small learning motor) or $150 to $400 (the real motor and controller) |
| PACK | Li-ion and LiFePO4 basics, cell limits and balancing, equivalent-circuit models, state of charge estimation, BMS front-end datasheets, fusing and wire sizing, contactors and precharge, E-stop loops, and whether HVIL or IMD is needed below 60 V DC | Size the pack for DRV's current and energy needs, fit a cell model to public data in Python, calculate precharge time and resistor ratings, size fuses and wires, and draw the BMS-controlled start-up sequence and E-stop loop in KiCad | An isolated bench pack: a few series cells at low voltage, with the BMS logic controlling a contactor or relay, running the precharge and safety checks into a resistive or lamp load, tripping on injected faults, with the mechanical E-stop loop working. No motor. | $100 to $250 |
| CHS | Basic kart geometry, steering and braking, fasteners and welds, FreeCAD basics | Lay out PACK and DRV mount locations and enclosures in CAD on a generic frame envelope, and estimate mass distribution at the Stage 1 design mass | Not part of Spark. A CAD layout plus a cardboard or printed mock-up; measure a used frame before buying one | $0 to $50 |
| VCU | Embedded C or C++, RTOS tasks, state machines, sensor plausibility checks, derate and safe-state patterns, LED status indication | Draw the vehicle state machine, including derate and safe states, define throttle processing and the LED indications, and test the logic on a computer | A dev board reading two potentiometers as redundant throttle, running the state machine against simulated PACK and DRV messages, and driving status LEDs | $30 to $60 |
| TEL | CAN logging, data formats, WebSocket or MQTT, simple web dashboards, Python analysis | Mock up the dashboard and debug views and define a data schema, tested on simulated data | A logger and web dashboard showing simulated, then live, CAN data, including a debug view | $10 to $30 (a software-only start is free) |
| NET | CAN 2.0 framing and bit timing, termination, DBC files, SavvyCAN, python-can | Starts light and grows with the other subsystems: collect message needs as their cycles define them, draft them in a DBC, and estimate bus load for a candidate bit rate | Two or three dev boards and a USB-CAN adapter exchanging DBC messages with a logger | $60 to $120 |
| TMS (optional) | Cell and motor thermal limits, derating curves, simple temperature sensing | Estimate heating from the sizing and cell models and decide whether passive cooling plus a derate strategy is enough | Temperature monitoring and derate logic prototyped inside the PACK and VCU MVPs; a separate subsystem only if monitoring says it is needed | $0 to $30 |
| RMT (optional) | Wireless link basics (ELRS or BLE), failsafe behavior, wireless safety | Design the remote kill concept and its failsafe behavior | A wireless link between two dev boards with a failsafe test | $30 to $60 |

Every cycle's first four steps are free, so the DRV and PACK paper proofs of concept can start in the first week with no hardware. The optional additions wait until the core subsystems are done.

**Recommended order (the builder's call)**

1. DRV: motor and controller selection drives most of the other subsystem work. If DRV cannot meet the system goals, the rest of the system probably cannot either, so its paper proof of concept doubles as a go or no-go check.
2. PACK (with distribution): the pack and distribution have the most important interaction with DRV and the most chassis integration. The BMS and power path also define most of the VCU's control states.
3. CHS: chassis constraints drive most of the PACK and DRV integration details. CHS is not part of Spark but must be addressed for later levels.
4. VCU: owns most of the application-layer logic and state, including the driver LED processing.
5. TEL: the hub for monitoring and debugging, critical for design and validation, and the feed for any downstream capability.
6. NET: the glue that holds everything together, but typically defined and created as the other subsystems' work proceeds, so it is lower priority than TEL and rarely needs much dedicated time.

## 11. Stage 3: Integration and the MVP kart (grows over time)

Integration starts as soon as two subsystems work and reaches its first milestone with a drivable kart (the MVP) built from the builder's own subsystems plus commercial placeholders for any subsystem that has not had its turn.

**Objective:** end up with a kart that drives safely at low speed, and a clear list of which placeholders to replace next.

**The MVP kart (builder to confirm)**

The MVP is a kart that drives at low speed under its own power, with a working E-stop, a protected battery, and controlled throttle. Which parts are the builder's own and which are commercial placeholders is decided at the architecture checkpoint and revisited after each subsystem cycle.

**Integration ladder**

1. Bench: two subsystems at a time, powered from a current-limited supply, with CAN traffic logged.
2. Rig: the full electrical system on the kart with the drive wheels off the ground and the E-stop within reach.
3. Low-speed field test: a clear, private area, a helmet, and a speed limit enforced in the VCU or controller.
4. Performance test: speed, acceleration, range, and thermal behavior, with data logged for analysis.
5. Endurance and review: repeated runs, inspection after each, and a data review in Python.

Move up a rung when the previous one feels solid. A written checklist is optional.

**Test types**

| Type | Examples |
| --- | --- |
| Electrical | Continuity, insulation, voltage drop, load and temperature rise |
| Functional | Start-up sequence, state machine transitions, driving modes |
| Fault injection | Cell limit trips, E-stop, sensor disconnect, CAN loss, stuck throttle |
| Performance | Top speed, acceleration, run time, efficiency |
| Reliability | Thermal soak, vibration, connector and fastener inspection |
| Usability | Can the builder operate and diagnose it from the dashboard and logs? |

**Refinement and upgrades**

- Turn every failed test into a short note with a cause and a fix, or a decision to accept it.
- Update the architecture, interfaces, and goals after each test campaign, and log why.
- After the MVP, replace placeholders with the builder's own subsystems as drop-in replacements in form, fit, and function, one at a time, keeping the kart drivable.
- After each subsystem cycle, write a short retrospective on the process: what research was wasted, what was worth it, and what to change next time.

**Deliverables**

- Test notes and results for each integration rung.
- A short demo recording or log for the portfolio.
- An updated architecture, interface notes, and a list of placeholders still to replace.

Kart **MVP checkpoint** (a few lines in the journal)

- Does the kart drive safely at low speed?
- Have the E-stop and the BMS cutoffs been tested?
- Do my notes match the kart as built?
- Which placeholder do I replace first?

## 12. Safety, risk, and compliance

The plan keeps the project survivable by staying at low voltage, putting protection in hardware, and energizing in stages, because a hobby build has no safety team beyond the builder.

**Safety principles**

- Design ceiling below 60 V DC at full charge. This keeps the kart out of the high-voltage class used in EV safety standards.
- The safe state is traction power off. A hardware path (E-stop loop and main contactor) reaches it without help from software.
- Fail toward de-energized: a lost signal, a lost heartbeat, or a watchdog trip removes torque.
- Energize in stages: bench with current limit, then rig with wheels off the ground, then low-speed field test.
- Review every new wiring change a second time before applying power. Never work on live circuits, and never work alone on the battery.
- Test the E-stop and the BMS cutoffs at every stage review, not only once.
- Never charge or store lithium cells unattended outside the designated container and area.

**Seed hazard and risk register**

If useful, score each risk for probability and impact on a simple 5 by 5 scale, and review the list at each checkpoint.

| Risk | Cause | Candidate mitigation | When it applies |
| --- | --- | --- | --- |
| Lithium pack fire or thermal runaway | Cell damage, overcharge, short circuit, poor charging practice | Quality cells or a reputable pack, independent protection, main fuse near the pack, fire-safe charging area | Any lithium cell work |
| Unintended acceleration | Sensor fault, firmware fault, controller fault | Redundant throttle sensing with a plausibility check, hardware E-stop, wheels-off testing, speed-limit modes | Any powered motion |
| Short circuit or arc at the pack | Tool slip, wiring fault | Insulated tools, covers, fusing, precharge, a second look at wiring before power-up | Any high-current wiring |
| Poor ventilation for soldering fumes and lithium handling | The garage and spare bedroom lack good ventilation | Fume extraction or an open-air setup for soldering, ventilation and a fire-safe spot for charging, sorted out before the first physical iteration | Before any soldering or lithium work |
| Loss of braking | Mechanical failure | Proven mechanical brakes that work independently of the electrics | Integration |
| Structural failure | Frame crack, loose mount | Commercial frame, inspection checklist, torque marks | Integration |
| Injury while driving | Speed, falls, collisions | Helmet, speed limit, a clear and closed test area | Integration |
| Budget overrun | Parts mistakes, scrapped boards, scope growth | Monthly cap, spend checkpoints, small PCB runs (section 13) | Throughout |
| Lost interest or scope creep | Too many subsystems at once, slow progress | One subsystem at a time, an enjoyment check at fold-back, a backlog parking lot, Spark and Bronze as valid stops | Throughout |

**Methods**

- Hazard analysis in Stage 1, then a short failure modes and effects analysis (FMEA) inside the cycles of the safety-relevant subsystems: PACK, VCU, and DRV.
- Risks are linked to goals and tests where practical, so each mitigation gets verified.

**Compliance**

JoyRide targets no certification and no formal functional safety compliance. Beyond the major safety concerns above, the builder follows good documentation and safe-state practice, applied per subsystem rather than as a full-system process: each subsystem records its safe state, its failure behavior, and which protections live in hardware. Standards for EV electrical safety and battery packs are read as design guidance only. The builder is responsible for checking local rules on where the kart may run and for insurance. This document is a plan, not a safety certification.

## 13. Budget and procurement plan

Spend follows learning: nothing is bought until a subsystem's paper proof of concept passes its spend checkpoint, and each first physical iteration is sized to fit inside about one month's budget.

At $150 per month, with carry-forward and rollover allowed, the project has up to about $2,700 over the 18-month target. All figures are approximate planning ranges, so check current prices before buying.

| Category | Approximate range | When |
| --- | --- | --- |
| Stage 1 and every paper proof of concept | $0 | Setup, research, architecture, and steps 1 to 4 of every cycle |
| First tools (multimeter, soldering gear, bench power supply) | $150 to $250 | At the first spend checkpoint that needs them |
| First physical iterations (dev boards, small parts, test cells) | $30 to $150 each | At each subsystem's spend checkpoint |
| Later tools (oscilloscope, logic analyzer, hot air station, 3D printer) | $350 to $550 | Only when a cycle needs one |
| Workspace and personal safety (including ventilation) | $100 to $250 | Before the first lithium or high-current work |
| MVP kart parts (used frame, placeholder motor and controller, pack, contactor, fuses, wiring) | $700 to $1,350 | After several subsystems work, at the MVP stage |

The builder can stop after any row without having committed to the next.

**Indicative pacing**

- Weeks 1 to 3: no spend. Stage 1 runs while the first learning bursts and paper proofs of concept get started.
- From the first passed spend checkpoint: roughly one first physical iteration every one to two months, plus tools as they are needed.
- MVP kart parts are bought when enough subsystems work, funded by rollover from earlier months.

**Purchasing rules (suggested)**

1. The monthly cap is $150. Unspent money rolls forward, and the budget tracker shows the running balance.
2. Buy only after a spend checkpoint, and write down the question the purchase answers.
3. Buy used where it is safe (frame, bench tools). Buy new for cells, fuses, contactors, and safety gear.
4. Use dev boards and breakouts before custom PCBs. Order custom boards in small batches when the learning value is high.
5. Log every purchase with a category and a subsystem code.

**Software cost policy**

Everything runs on free or open-source tools: KiCad, FreeCAD or Onshape free tier, PlatformIO or STM32CubeIDE, FreeRTOS or Zephyr, SavvyCAN, PulseView, and Python. Any paid tool needs a DEC entry that shows no free alternative works.

## 14. Learning goals and skills roadmap

Because learning is the product, each skill area has a target level and a place in the plan where it gets practiced, with a repository artifact as the evidence.

Starting levels for areas the builder did not describe are assumptions. The builder should correct them in P0.

| Skill area | Starting level (confirm) | Target by project end | Practiced in |
| --- | --- | --- | --- |
| Requirements and systems engineering | Strong in practice | A light but traceable process run at system and subsystem level | Stage 1 |
| Power distribution and HV safety | Strong | Own pack power path with precharge, contactors, and fault handling | PACK |
| Schematic capture and PCB layout (KiCad) | Assumed moderate | Multi-layer power and mixed-signal boards that work on rev B | NET, PACK, DRV |
| Embedded C/C++, drivers, RTOS | Some | Drivers and RTOS applications on several nodes | VCU, PACK, NET |
| CAN and vehicle networking | Likely strong | DBC-driven network with diagnostics and a gateway | NET |
| Battery management and state estimation | Assumed moderate | Own BMS with a state of charge estimator tested against data | PACK |
| Motor control (FOC) | Assumed new | Working field-oriented control on a self-built inverter | DRV |
| 3D CAD and mechanical design | Assumed new | Enclosures and brackets that fit first or second try | CHS |
| Web and mobile software | Educational background | Live telemetry dashboard and a configuration app | TEL |
| Test and verification practice | Moderate | Written test procedures, fault injection, and automated analysis | All |

**Seed learning goals**

The orchestration LLM should turn these into LRN items, each with an evidence field.

- LRN-001: Take a board from schematic to ordered, assembled, and debugged (evidence: bring-up report).
- LRN-002: Write a DBC and use it across at least three nodes and a logger.
- LRN-003: Build firmware with an RTOS and a layered driver structure on two different boards.
- LRN-004: Characterize a cell and fit a battery model in Python.
- LRN-005: Implement and compare two state of charge estimators on logged data.
- LRN-006: Design and test a precharge and contactor circuit with fault handling.
- LRN-007: Run a Pugh chart and a weighted decision matrix and record the decision.
- LRN-008: Run a fault-injection test campaign and close every finding.
- LRN-009: Run field-oriented control on a motor, first with open-source firmware, then with own hardware.
- LRN-010: Complete one subsystem cycle, from learning burst to fold-back, and change the process as a result.

## 15. Tracking tools for the orchestration LLM to generate

Generate a small starter set in the first week (rows 1 to 10), then create the rest only when a stage or subsystem cycle needs them, so the process never outruns the work.

**Rules**

- Prefer plain formats that live in the repository (CSV, Markdown) or simple spreadsheets. Every tool uses the ID schemes in section 1 and links to others by ID.
- Each tool ships with a one-paragraph usage note, column definitions, and one example row.
- Use dropdowns for status fields. Suggested statuses: Not started, In progress, Blocked, Done.
- Seed tools from the sections listed. Where this document gives placeholders, mark the cell "TBD, builder decision".

| # | Tool | Suggested format | Seed from | Create | Update |
| --- | --- | --- | --- | --- | --- |
| 1 | Master roadmap: stages, subsystem order, and checkpoints, with no fixed dates | Spreadsheet or board | Sections 4, 16 | Week 1 | Weekly |
| 2 | Backlog and task board with subsystem and cycle-step fields | Project board or sheet | All sections | Week 1 | Weekly |
| 3 | Subsystem tracker: one row per subsystem with its cycle step (dropdown), next action, and rough cost | Spreadsheet | Sections 8 to 10 | Week 1 | Weekly |
| 4 | Budget and purchase tracker with monthly cap, rollover, and spend by subsystem | Spreadsheet | Section 13 | Week 1 | On purchase |
| 5 | Journal and decision log: dated entries and rejected options | Markdown | Sections 9, 16 | Week 1 | Weekly |
| 6 | Risk and hazard list | Spreadsheet | Section 12 | Week 1 | Monthly |
| 7 | Learning tracker with evidence links | Spreadsheet | Section 14 | Week 1 | Monthly |
| 8 | Tool and equipment shopping list, empty until a cycle needs something | Spreadsheet | Section 13 | Week 1 | On purchase |
| 9 | Repository structure and README conventions | Markdown | Section 5 | Week 1 | As needed |
| 10 | Checkpoint templates (architecture, spend, fold-back, MVP) | Markdown | Section 16 | Week 1 | At each checkpoint |
| 11 | System goals list with a subsystem tag on each goal | Spreadsheet | Section 7 | Stage 1 | As needed |
| 12 | Interface notes and a DBC skeleton | Markdown, CSV, DBC | Section 8 | Stage 1 | Per change |
| 13 | Subsystem one-pager: needs sketch, concepts, paper proof of concept notes, results | Markdown template | Section 9 | Start of each cycle | During the cycle |
| 14 | Test log and report template | Spreadsheet plus Markdown | Section 11 | First physical iteration | Per test |

**Orchestrator behavior**

- Before generating any tool, list assumptions and open questions from section 17 and ask the builder to confirm the ones that change structure.
- After generating the starter set, produce a short "how the tools connect" note: which ID flows into which tool.
- When the builder completes a checkpoint, update the affected tools instead of creating duplicates.

## 16. Rhythm, checkpoints, and definition of done

The project runs on a light weekly rhythm and four short checkpoints, and it can be paused at any checkpoint without losing work.

**Cadence**

| Rhythm | Activity | Time |
| --- | --- | --- |
| Weekly | Look at the backlog, pick next week's tasks, check the budget, and write a short journal entry | About 30 minutes |
| Monthly | Skim the hazard list, reconcile the budget, and update the learning tracker | About 1 hour |
| Each checkpoint | A few lines in the journal answering the checkpoint questions | About 30 minutes |
| End of each subsystem cycle | A short retrospective on the subsystem and on the process | About 1 hour |

**Checkpoints**

| Checkpoint | When | Questions to answer in a few lines |
| --- | --- | --- |
| Architecture | End of Stage 1 | Can I name every subsystem and what it does? Which subsystem do I start with? Do I have a rough cost for each? |
| Spend | After each paper proof of concept | Does the paper proof hold up? What is the cheapest physical test, and does it fit one month's budget? Do I still want to build this? Go, adjust, or park. |
| Fold-back | After each subsystem MVP | Did the MVP meet its pass or fail criterion? What did I learn? What changes in the architecture or interfaces? Was it fun, and what comes next? |
| Kart MVP | When the first kart drives | Does it drive safely? Do the E-stop and BMS cutoffs work? Which placeholder do I replace first? |

The orchestration LLM can turn each checkpoint into a one-page template (section 15, row 10).

**Rules of thumb**

- Time-box, then decide. If a step runs well past its estimate, shorten it or park it.
- Spend only after a spend checkpoint.
- Run one subsystem cycle at a time.
- If a step stops being fun or useful, skip it and note why.
- Keep a working baseline: do not remove a working part until its replacement works.
- A subsystem with unmet safety basics does not go on the kart.

**Definition of done for JoyRide**

The project is done when the builder declares a success level from section 2 (Spark, Bronze, Silver, or Gold), the engineering record matches the as-built kart, and a final retrospective is written. Stopping at any level is a legitimate end.

## 17. Assumptions, open questions, and first 30 days

The plan rests on a handful of assumptions that the builder should confirm or correct before the orchestration LLM builds the first tools.

**Assumptions**

- The $150 monthly cap is firm and includes everything, with unspent money rolling over.
- The voltage ceiling is below 60 V DC at full charge.
- The builder has 6 to 10 hours a week and a workspace where lithium cells can be handled and charged safely.
- The kart runs only on private property or a closed course.
- No MCU family, RTOS, or wireless platform is chosen yet. The examples named in this document are options for the relevant subsystem cycle to decide.
- The framework follows the general sequence of Mattson and Sorensen's text, applied loosely as the builder asked. Chapter-level mapping (tool names and templates) should be checked against the book and the orchestrator adjusted to match.

**Open questions (builder decisions)**

1. Where will the kart be built, stored, and driven, and what power and ventilation does the workspace have?
2. Is the target timeline closer to 12 months or 24 months, and which success level (Spark, Bronze, Silver, Gold) is the real aim?
3. Which subsystem do you want to start with? Section 10 suggests an order, but any subsystem can go first.
4. Should the first drivable kart use a bought battery pack or one assembled from cells?
5. Will the repository and documentation be public (open source) or private?
6. How heavy is the intended driver, and what is the intended top speed?

**Builder answers (from comment threads)**

- Workspace: a garage for the kart and a spare bedroom for subsystem work. Ventilation for lithium and soldering is not good and must be addressed later.
- Timeline and aim: about 18 months, with Spark as the current aim, mainly for fun and learning.
- Starting order: recorded in section 10.
- Battery: a pack assembled from cells is the preference, still to be determined in the PACK cycle.
- Openness: fully open source, with a Git or GitHub submodule for each atomic piece (embedded firmware, shared communications library, PCB schematics, and so on).
- Starting inputs for the Stage 1 system requirements: about a 300 lb driver, a 200 lb kart, and about 30 mph top speed, all to be confirmed in Stage 1.

**First 30 days**

- [ ] Confirm or correct the assumptions and answer the open questions above.
- [ ] Ask the orchestration LLM to generate the starter set of tools (section 15).
- [ ] Create the repository, the journal, and the decision log, and install KiCad, FreeCAD, and a Python environment.
- [ ] Do the system-level research (section 6): benchmark table, drivetrain sizing model, and seed hazard list.
- [ ] Write the system goals and the architecture (sections 7 and 8), and pick the first subsystem.
- [ ] Hold the architecture checkpoint (section 16).
- [ ] Start the first subsystem's learning burst and paper proof of concept (sections 9 and 10), which can overlap with the end of Stage 1.
- [ ] At the first spend checkpoint, decide whether any first purchase is worth making.
