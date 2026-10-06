---
id: STG-<1 | 2-CODE | 3>
status: Not started
updated: <YYYY-MM-DD>
stage_type: <system | cycle | integration>
subsystem: <CODE, or none>
spark: <yes | no | not yet decided>
---

# STG-<id>: <name>

<!--
Every stage document keeps every heading below, in this order.
Optional stubs keep each heading with one line.
Cycle documents (stage_type: cycle) use exactly the seven Step headings under Tasks.
The cycle itself is defined in PROJECT.md#subsystem-cycle; do not restate it.
Delete these comments.
-->

## Purpose

<One or two sentences: why this stage exists.>

## Entry and exit

- Entry: <what must be true to start>
- Exit: <the checkpoint or condition that ends it>

## Inputs and neighbors

- <Links to the inputs this stage uses>
- Neighbors: <CODEs>, interfaces in [SUBSYSTEMS.md](../architecture/SUBSYSTEMS.md#<anchor>)

## Goals

- <Concrete outcomes of this stage>

## System goals served

<REQ IDs from GOALS.md, or "None yet". IDs only, no targets.>

## Tasks

### Step 1: Learning burst

- [ ] <short imperative>

### Step 2: Needs and MVP sketch

- [ ] Create `subsystems/<CODE>/docs/` from `docs/templates/subsystem/`.
- [ ] Write REQUIREMENTS.md, tracing each REQ to a system REQ or ICD.
- [ ] Confirm the draft MVP below.

| MVP | Draft (proposed, builder to confirm) |
| --- | --- |
| Prototype | PRT-<CODE>-01: <description> |
| Test | TST-<CODE>-001 |
| Pass or fail | <criterion; thresholds TBD> |

### Step 3: Concepts

- [ ] <options to compare in CYCLE.md>

### Step 4: Paper proof of concept

- [ ] <riskiest assumption to test on paper>

### Step 5: Spend checkpoint

- [ ] <the question the first purchase answers>

### Step 6: Subsystem MVP

- [ ] Build PRT-<CODE>-01 and run TST-<CODE>-001.

### Step 7: Fold-back

- [ ] Feed changes back to <neighbors>, GOALS, and RISKS.

## Deliverables

<Cycle documents: "Standard cycle deliverables, plus:" and only the extras. Others: the full list.>

## Spend

<Rough range and when it is spent.>

## Risks

<RSK IDs from RISKS.md, or "None in the register".>

## Decisions

| Decision | Shared with | DEC |
| --- | --- | --- |
| <decision> | <CODE or none> | <DEC ID once logged> |

## Checkpoint additions

<Stage-specific questions added to the standard checkpoint questions.>

## Out of scope

- <item>

## Open items

| # | Open item | Owner |
| --- | --- | --- |
| 1 | <item> | <Builder decision, or a stage> |
