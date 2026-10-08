# JoyRide documentation rules

These rules govern every document in this repository. Update this file when practice changes.

## What this repository is

This root repository holds high-level decisions and project-level documentation for JoyRide, a hobby electric go-kart. Subsystem detail lives in each subsystem's home (see [Layout](#layout)).

Core documents drive all future work, and the builder reviews them closely:

- `docs/project/` (PROJECT, GOALS, RISKS)
- `docs/architecture/SUBSYSTEMS.md`
- `docs/stages/STG-*.md`

Core-document rules:

- Edit a core document only when the builder asks, or when a task explicitly requires it.
- Keep diffs minimal. Do not reword text that is not part of the change.
- List every core-document change in the reply.
- Keep the builder's verbatim text (working principles, constraints) unchanged.

## Working with the builder

- Treat stage tasks and the cycle as recommendations. The builder's latest instruction wins.
- Never invent a value. Write TBD and add an open item to the owning document.
- Ask before resolving anything marked "builder decision".
- Do not add scope. New ideas go to the backlog as an issue labeled `parking lot`.
- Named parts, tools, and protocols are examples, not decisions, until a DEC accepts them.

## Action items

- Track every action item and open assessment as a GitHub issue, using the Task or Decision form.
- Documents do not link to issues, and do not keep their own to-do lists. The exceptions are stage tasks and stage open items.
- Any record that an issue creates or changes cites that issue as its source, for example "Resolved in #12". This covers every ID type, plus document changes.
- Close the issue once the documents are updated.

Every issue carries this metadata:

| Field | Where | Values |
| --- | --- | --- |
| Stage | Milestone | One milestone per STG, such as "STG-2-DRV Motor and drive". Leave empty for project-wide work. |
| Type | Label | `type: task`, `type: decision`, `type: purchase`, `type: test`, `type: docs` |
| Subsystem | Label | `sub: <CODE>`, or `sub: system` for cross-cutting work |
| Out of scope | Label | `parking lot` |
| Status | [JoyRide project](https://github.com/users/Braden2n/projects/1) | Todo, In progress, Blocked, Done |
| Cycle step | JoyRide project | 1 to 7, or Not a cycle task |
| Estimate | JoyRide project | Hours, to plan against 6 to 10 hours a week |

The forms set the type label and add the issue to the project. Set the milestone, subsystem label, and project fields when filing.

## Agent work from issues

Agents run from `@claude` mentions in issues and PRs. The builder's latest comment overrides this section.

### Rules for every run

1. Read this file, the linked stage document, and the full issue thread before changing anything.
2. Work on a new branch from `main`, named `issue-N-short-slug`. Never commit to `main`, force-push, or delete files.
3. Open one PR per issue. The PR body cites the issue, for example "Refs #12".
4. Do not merge, close issues, or resolve decisions. The builder does those.
5. If the request is unclear, or a choice belongs to the builder, ask in a comment and stop.
6. Never invent a value. Write TBD, and add an open item to the owning document.
7. Record new ideas as a `parking lot` issue. Do not act on them.
8. Add any new directory to the Layout section in the same PR.

### Rules by issue type

| Issue | Agent action |
| --- | --- |
| `type: task` | Do the work in a branch and open a PR. Tick a stage task only when the builder asks. |
| `type: decision` | Draft the DEC, its decision log row, and the stage Decisions table link in one PR. Do not mark it accepted. |
| `type: purchase` | Do not order anything. Draft a budget row in PROJECT.md, with unknown costs marked TBD, and flag it for the builder. |
| `type: test` | Draft a TST report from [docs/templates/](docs/templates/README.md) in the subsystem's `docs/tests/`. Record only results the builder supplies. |
| `type: docs` | Edit only the documents the issue names, in a PR. |
| No type, or a question | Answer in a comment. Make no file changes. |
| `parking lot` | Take no action. |

### Dividing work

| Work | Agent | Builder |
| --- | --- | --- |
| Drafting documents, DEC drafts, journal entries, test report drafts | Drafts in a PR | Reviews, decides, and merges |
| Triage, summaries, finding related IDs | Comments | Confirms |
| Test results, measurements, costs | Records only what the builder supplies | Supplies the data |
| Decisions, goal and risk changes, requirement levels | Drafts only | Decides and approves |
| Safety judgments, sign-off, hardware, purchases | Drafts only, never final | Decides and does |

## Layout

The ID prefix decides where a record lives. Global IDs live in the root. IDs that carry a subsystem code live in that subsystem's home. Schemas for every ID type are in [docs/templates/README.md](docs/templates/README.md).

```
CLAUDE.md                          these rules
.github/ISSUE_TEMPLATE/          Task and Decision issue forms (issues are cited as #N)
docs/
  README.md                        index
  project/PROJECT.md               charter, constraints, process, safety, budget, rhythm
  project/GOALS.md                 NEED, system REQ, LRN
  project/RISKS.md                 RSK register
  architecture/SUBSYSTEMS.md       SUB blocks, architecture, ICD list
  architecture/interfaces/         ICD files (created with the first ICD)
  decisions/                       DEC files and the decision log
  journal/                         dated entries and checkpoints (created with the first entry)
  stages/                          STG documents
  templates/                       all templates and record schemas
```

Each subsystem home has this layout, whether it ends up as a folder or a submodule:

```
subsystems/<CODE>/
  docs/README.md                   from docs/templates/subsystem/README.md
  docs/REQUIREMENTS.md             subsystem REQs; each traces to a system REQ or an ICD
  docs/CYCLE.md                    learning notes, needs and MVP sketch, CON, PoC, PRT, FMEA, results
  docs/tests/TST-<CODE>-NNN.md     test reports
  <submodules>                     firmware, PCB, CAD, and so on
```

Create a subsystem home at step 2 of its cycle, by copying `docs/templates/subsystem/`. Create folders only when their first file exists.

## What to write

Necessary:

- Decisions, with the options that were rejected.
- System goals, risks, interfaces, and stage plans.
- Checkpoint outcomes and journal entries.
- Open items, each with an owner.
- Links between IDs, so items trace to each other.

Unnecessary, so leave it out:

- Content that already exists elsewhere. Link to it or cite its ID instead.
- Provenance notes, such as where a sentence came from.
- Preambles, such as "This document describes...".
- Boilerplate sentences repeated across documents. A template carries them once.
- Rationale that already lives in a DEC.
- New files when a row or a section would do.
- Scratch scripts, test files, or generated reports. Validate in a scratchpad and delete.

## Templates

- Every file in a multi-file folder follows that folder's template. See the catalog in [docs/templates/README.md](docs/templates/README.md).
- Single documents (PROJECT, GOALS, RISKS, SUBSYSTEMS, README) have no template. Their table rows follow the record schemas.
- Copy a template, fill in its placeholders, and delete its guidance comments.
- If a template does not fit, change the template first, then every file that uses it.

## Style

- Lead each section with its point.
- Use tables for items with attributes, numbered lists for ordered steps, and bullets for parallel items.
- Keep sentences under 25 words. Do not use emoji.
- Use relative links. Link to headings by their GitHub anchors.
- Citing an ID is fine. Restating its content is not.
- Write tasks as short imperatives.

## Organization

- Any core document with more than five `##` sections opens with a table of contents.
- The table of contents lists every `##` heading, in order, with exact anchors.
- Front matter keys are `id`, `status`, and `updated` (a date). The H1 is the title.
- `status` is draft, active, or done. A file that is itself a record (STG, DEC, ICD, TST) uses that record's status values instead.
- Stage documents add `stage_type` (system, cycle, or integration), `subsystem`, and `spark`.
- Decision files add `decided` (a date).

## Update flow

| Event | Update |
| --- | --- |
| Weekly session | Write a journal entry. Tick stage tasks. Update task issues. |
| Decision made | Add a DEC file and a decision log row. Link the DEC from the stage document's Decisions table. |
| Checkpoint held | Write a journal entry from the checkpoint variant. Update the stage document's status and open items. |
| Goal or risk changes | Edit its row in GOALS.md or RISKS.md. Note why in the journal. |
| Interface agreed | Add an ICD file and its row in the SUBSYSTEMS.md interface list. |
| Purchase | Log it in the budget tracker with a category and a subsystem code. |
| Cycle step 2 | Create the subsystem home from the templates. |
| Fold-back | Feed interface, goal, and risk changes back to the root documents. |
