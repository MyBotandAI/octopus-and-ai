# `<project-name>` — DECISIONS

**Owner:** Analyst / Architect (writes rows after PO confirms via OQ per D2)
**Updated:** `<YYYY-MM-DD>`

Cross-cutting decisions for the `<project-name>` project. Decisions are immutable once written; to change a decision, supersede it with a new row and move the old one to `## Superseded Decisions` at the bottom.

This file is the **canonical anchor target** for cross-doc references (per D12 inter-doc boundaries). Other docs (`AGENTS.md`, `ROADMAP.md`, `BACKLOG.md`, Task specs) cite kebab-case slugs from the index below; the rationale lives here once.

---

## Scope

**`DECISIONS.md` is for cross-cutting decisions only** — choices that affect **≥2 Tasks, ≥2 files, or ≥2 roles**. Single-screen design calls live in their originating Task spec; single-component code rules live as one-line gotchas in `AGENTS.md` (with anchored reference back to the relevant DECISIONS row when there is a choice involved).

---

## Format

The **index table** below is the scannable pointer. Each row carries a **kebab-case slug** (the cross-document anchor target), a **≤150-char Summary**, and the **Locked date**.

When a decision's rationale exceeds one row, it promotes to a **body section** anchored by the slug. The index points at the body via the slug link; the body holds the full Value and Rationale. Cells stay one physical line, ≤150 chars.

Projects whose decisions all fit short rows may keep the index table only — body sections are optional per row. Promote any row to a body section the moment its rationale needs more than the cell can hold.

---

## Index

| Slug | Summary | `<Surface>` | Locked |
|---|---|---|---|
| [`<kebab-case-slug>`](#kebab-case-slug) | `<≤150-char authoritative summary>` | `<surface>` | `<YYYY-MM-DD>` |

`<Surface column is optional — include in multi-component projects (declared `Surface column: Used` in `PROJECT_GUIDE.md § Project mode`); omit otherwise.>`

---

## Decisions

### `<kebab-case-slug>`

**Locked:** `<YYYY-MM-DD>`

**Value.** `<one-sentence authoritative statement of what was decided>`

**Rationale.** `<why this and not the alternatives — surface the cost of the chosen option honestly. Multi-paragraph OK here; this is the durable home.>`

`<Optional cross-references: Closes parity item P-xx · Surfaced at TASK_X · Implemented in AGENTS.md § N>`

---

## Superseded Decisions

Locked decisions that no longer apply. IDs (slugs) are preserved — never reused. Original Value + Rationale stay in this file as historical record; the body anchor remains reachable.

| Slug | Summary | Superseded by | Locked / Retired |
|---|---|---|---|
| [`<old-slug>`](#old-slug) | `<original summary>` | [`<new-slug>`](#new-slug) | `<old-locked YYYY-MM-DD> → <retired YYYY-MM-DD>` |

A superseded decision's body section gains a top-line **Superseded by:** pointer to the new slug. The new slug's body gains a **Supersedes:** pointer to the old one. Both stay in the file; only the index entry moves between sections.

---

*Decisions immutable once written. PO confirms decisions via OQ per D2 in `methodology/DIRECTIVES.md`; Analyst, Architect, or any agent that surfaces a decision writes the row. To supersede: write the new row in the active index; move the old row to the `## Superseded Decisions` section; add `Superseded by:` to old body and `Supersedes:` to new body.*
