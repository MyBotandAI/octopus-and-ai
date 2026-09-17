# `<project-name>` — DECISIONS

**Owner:** Analyst / Architect (writes rows after PO confirms via OQ per D2)
**Updated:** `<YYYY-MM-DD>`

Cross-cutting decisions for the `<project-name>` project. The record is immutable — a written decision is never edited or deleted; to change one, supersede it with a new row and move the old one to `## Superseded Decisions` at the bottom. Whether a decision is still *right* stays askable at any time (D2).

This file is the **canonical anchor target** for cross-doc references (per D12 inter-doc boundaries). Other docs (`AGENTS.md`, `ROADMAP.md`, `BACKLOG.md`, Task specs) cite kebab-case slugs from the index below; the rationale lives here once.

---

## Scope

**`DECISIONS.md` is for cross-cutting decisions only** — choices that affect **≥2 Tasks, ≥2 files, or ≥2 roles**. Single-screen design calls live in their originating Task spec; single-component code rules live as one-line gotchas in `AGENTS.md` (with anchored reference back to the relevant DECISIONS row when there is a choice involved).

---

## Format

The **index table** below is the scannable pointer. Each row carries a **kebab-case slug** (the cross-document anchor target), a **≤150-char Summary**, and the **Locked date** — plus a **State** cell once the project has earned that column (see § State).

When a decision's rationale exceeds one row, it promotes to a **body section** anchored by the slug. The index points at the body via the slug link; the body holds the full Value and Rationale. Cells stay one physical line, ≤150 chars.

Projects whose decisions all fit short rows may keep the index table only — body sections are optional per row. Promote any row to a body section the moment its rationale needs more than the cell can hold.

---

## State

A row is **`Locked`** unless it is **`Provisional`** — bound now, carrying a written **`Revisit when:`** trigger that names the specific thing which re-opens it (D2). A provisional row **binds exactly as a locked one does**; the only difference is that the moment it gets re-examined is written down instead of assumed. Prefer it to a full lock whenever the rationale itself rests on an estimate.

When evidence contradicts a row, its State cell gains **` — challenged`** and its body a **`Challenged:`** line pointing at the document that holds the evidence. The row still binds — the mark is what stops a later reader taking the lock as unexamined.

The **State** column is added to the index the first time this project writes a provisional or challenged row. A project with neither omits the column, and every row without it reads as locked.

---

## Index

| Slug | Summary | `<State>` | `<Surface>` | Locked |
|---|---|---|---|---|
| [`<kebab-case-slug>`](#kebab-case-slug) | `<≤150-char authoritative summary>` | `Locked` | `<surface>` | `<YYYY-MM-DD>` |
| [`<provisional-slug>`](#provisional-slug) | `<≤150-char authoritative summary>` | `Provisional` | `<surface>` | `<YYYY-MM-DD>` |
| [`<contested-slug>`](#contested-slug) | `<≤150-char authoritative summary>` | `Locked — challenged` | `<surface>` | `<YYYY-MM-DD>` |

`<State column is optional until the first provisional or challenged row — see § State above; omit it while every row is a plain lock.>`

`<Surface column is optional — include in multi-component projects (declared `Surface column: Used` in `PROJECT_GUIDE.md § Project mode`); omit otherwise.>`

---

## Decisions

### `<kebab-case-slug>`

**Locked:** `<YYYY-MM-DD>`

**Value.** `<one-sentence authoritative statement of what was decided>`

**Rationale.** `<why this and not the alternatives — surface the cost of the chosen option honestly. Multi-paragraph OK here; this is the durable home.>`

`<Optional cross-references: Closes parity item P-xx · Surfaced at TASK_X · Implemented in AGENTS.md § N>`

---

### `<provisional-slug>`

**Locked (provisional):** `<YYYY-MM-DD>`
**Revisit when:** `<the specific thing that re-opens this — a number measured, a customer signed, a threshold reached. Not "when we know more".>`

**Value.** `<what binds today — written as firmly as any other row>`

**Rationale.** `<why this binds now, and what is not yet known. Name the estimate the decision rests on rather than letting it read as a measurement.>`

---

### `<contested-slug>`

**Locked:** `<YYYY-MM-DD>`
**Challenged:** `<YYYY-MM-DD>` — `<one line naming what contradicts this>` → `<path/to/the/document.md>`

**Value.** `<what still binds — a challenged row is not a retracted one>`

**Rationale.** `<the original rationale, unedited. The challenge does not rewrite it; the line above records that it is contested.>`

`<A challenge is anchored here by the agent that surfaced it, whether or not PO supersedes the row (D2), and one line is added per challenge. It is never edited away: the supersession that resolves it moves this row to § Superseded Decisions with its rationale and its challenges intact, and the new row carries the answer.>`

---

## Superseded Decisions

Locked decisions that no longer apply. IDs (slugs) are preserved — never reused. Original Value + Rationale stay in this file as historical record; the body anchor remains reachable.

| Slug | Summary | Superseded by | Locked / Retired |
|---|---|---|---|
| [`<old-slug>`](#old-slug) | `<original summary>` | [`<new-slug>`](#new-slug) | `<old-locked YYYY-MM-DD> → <retired YYYY-MM-DD>` |

A superseded decision's body section gains a top-line **Superseded by:** pointer to the new slug. The new slug's body gains a **Supersedes:** pointer to the old one. Both stay in the file; only the index entry moves between sections.

---

*The record is immutable; the question stays open (D2 in `methodology/DIRECTIVES.md`). PO confirms decisions via OQ; Analyst, Architect, or any agent that surfaces a decision writes the row — and any agent holding evidence against a row is expected to surface the supersession OQ rather than file the contradiction elsewhere. To supersede: write the new row in the active index; move the old row to the `## Superseded Decisions` section; add `Superseded by:` to old body and `Supersedes:` to new body.*
