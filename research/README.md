---
id: RESEARCH
status: active
updated: 2026-11-04
---

# Research

Reference documents, sources, and learnings that inform decisions. A DEC cites a file here by relative link in its Context or Consequences. Each file names its sources and the date it was written.

## Index

| File | Topic | Used by |
| --- | --- | --- |
| [adult-racing-leagues.md](Adult%20Racing%20Leagues/adult-racing-leagues.md) | Adult kart class mass, power, and energy as a sizing baseline | REQ-SYS-003, REQ-SYS-004, plant model |
| [vehicle-dynamics-constants.md](Vehicle%20Dynamics/vehicle-dynamics-constants.md) | Plant Vehicle parameters: drag area, rolling resistance, mass, rotating mass | Plant model |

## Conventions

Files:

- One topic per file, named by a short slug, such as `battery-cell-models.md`.
- Each file has front matter with `id`, `status`, and `updated`. Its `status` is draft, active, or done.
- A topic folder may hold a README that indexes its sources and what each one provides.
- Prefer a new section or table row in an existing topic file over a new file.

Content:

- Record what was learned and what it means for JoyRide. Do not copy whole sources.
- Record new learnings as they come in. Do not leave them in chat.
- For each value or choice, record the question, the sources checked, what was rejected and why, and the decision.
- Name who made each decision, with the date. Label a value an estimate until the builder accepts it.
- Label each value's basis: measured, fitted, assumed, or cited. Trace a cited value to its original source before using it.
- Give uncertain values a baseline and a sweep range.
- Use the symbols and parameter names of the model that consumes the values, and link to its equations.
- When new research changes an assumption in another file, update that file in the same change.

Sources:

- Add a source only when it gives a decision or model critical information. Do not add every reference a paper cites.
- Save open-access papers and rulebooks as local PDFs. Save paywalled papers, slides, and web pages as `.webloc` links.
- Cite a minor source by DOI or URL instead of saving it.
- End each file with a Sources section: a table of local copies, a table of links, and a "Not saved" line for weak sources.
