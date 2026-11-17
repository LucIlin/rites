---
name: decision-log
description: Records project decisions in the matching docs/ file and logs the reasoning in docs/decisions.md. Use when the user says "log that", "reject that", "park that" or "show the log", or asks to record, change or look up a project decision.
---

# Decision log

Record decisions the user makes about this project. Put each decision in the doc it belongs to, and keep a short record of the reasoning in `docs/decisions.md`.

## Core rule

Only record a decision when the user explicitly confirms it ("log that", "decided", "go with X"). Never record your own suggestions as decisions, even if the user reacted positively.

## Where decisions go

| File | Covers |
|---|---|
| `docs/01-product.md` | Target users, MVP scope, what's out of scope, screens |
| `docs/02-data-model.md` | Tables, fields, relationships |
| `docs/03-api-contract.md` | Endpoints, requests, responses |
| `docs/04-architecture.md` | How backend, Android and iOS fit together; stack and libraries |
| `docs/05-build-plan.md` | Order of work, steps, "done when" checks |
| `docs/06-design-notes.md` | Screen layout, look and feel |
| `docs/07-content-sourcing.md` | Content sources and usage rights |

A decision can affect several files. For example, a new field in the data model may change endpoints in the API contract. Update every affected file so the docs stay consistent.

If the target file is unclear, ask before writing.

## Commands

| Command | Action |
|---|---|
| `log that` | Update the affected doc(s), then add a DECIDED entry to `docs/decisions.md` |
| `reject that` | Add a REJECTED entry to `docs/decisions.md` only |
| `park that` / `open question` | Add an OPEN entry to `docs/decisions.md` only |
| `show the log` | Print `docs/decisions.md` |

After writing, report the entry ID and each file and section changed, so the user can ask to move or undo it.

## Updating docs

1. Read the file before editing.
2. Edit the section the decision belongs to. Add a new section only if none fits.
3. State the decision as current fact (for example "Passages are stored in PostgreSQL"). Keep history in `docs/decisions.md`.
4. Change only what the decision covers. Do not rewrite surrounding text.
5. If the decision conflicts with existing content, describe the conflict and ask before overwriting.
6. If the decision creates new work, suggest a step for `docs/05-build-plan.md`. Add it only if the user agrees.

## decisions.md format

```markdown
## D-001: <short title>
- **Date:** YYYY-MM-DD
- **Status:** DECIDED | REJECTED | OPEN | SUPERSEDED by D-00X
- **Decision:** <one sentence>
- **Why:** <reason given by the user>
- **Rejected options:** <option> – <reason>
- **Updated:** <files and sections changed, or "none">
```

- Number entries sequentially from the highest existing ID.
- Write "none stated" for any field the user did not provide. Do not invent reasons or alternatives.
- When a decision replaces an earlier one, set the old entry's status to `SUPERSEDED by D-00X`, keep it, and update the docs to match.
- When an OPEN entry is resolved, update that entry instead of adding a new one.

## Accuracy

- Copy names the user puts in quotes exactly, in both the docs and the log. If a name conflicts with existing docs, ask.
- Before design or planning work, read the relevant docs and treat them as the current state.