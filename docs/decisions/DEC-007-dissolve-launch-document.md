---
id: DEC-007
status: Accepted
decided: 2026-10-06
updated: 2026-10-06
---

# DEC-007: Dissolve the launch document

## Context

The launch document was converted into PROJECT, GOALS, RISKS, SUBSYSTEMS, the decision log, and the stage documents. Keeping it would leave two sources of truth.

## Options

| Option | Pros | Cons |
| --- | --- | --- |
| Keep it as a reference | Original wording at hand | Drifts from the living documents |
| Delete it | One source of truth | Original only in git history |

## Decision

Delete it. The original is in git history at commit 3308a9d.

## Consequences

Low-value content was not carried over: the process-weight table, the strengths and stretch table, budget pacing notes, tool-generation behavior, and some tool examples. Both diagrams never exported.
