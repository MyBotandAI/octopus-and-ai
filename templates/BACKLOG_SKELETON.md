# `<project-name>` — Backlog

**Owner:** Analyst
**Updated:** `<YYYY-MM-DD>`

Unassigned work items, organized by tier (impact × effort) and time-to-ship. Items assigned to a release move to `ROADMAP.md` under that release.

---

## Prioritisation framework

Tiers are a pure **impact × effort** matrix. The **`When`** column carries time-to-ship as a separate axis.

| Tier | Impact | Effort | Meaning |
|---|---|---|---|
| 1 | High | Low | Quick wins — do soon |
| 2 | High | Medium-high | High-value, plan into a release |
| 3 | Medium | Low-medium | Polish / paper-cut fixes |
| 4 | Low | Any | Nice-to-have / nice-to-have-someday |

**`When` values:** `pre-release` (default) · `post-1.0` · `post-traction`.

**Estimation gate (per D14):** Items default to `## Needs estimation`. Promotion to any tier requires a DEV effort estimate on the row. Exception: items with obviously known effort (a parity backport, a single-file cleanup, a known one-liner) may bypass with a `(self-estimated)` tag in Notes.

---

## Needs estimation

Default landing for new items. DEV estimates effort; PO weighs impact at the next review; item moves to Tier 1–4.

| ID | Item | `<Surface>` | Notes |
|---|---|---|---|

---

## Tier 1 — Quick wins (high impact, low effort)

| ID | Item | Effort | When | `<Surface>` | Notes |
|---|---|---|---|---|---|

---

## Tier 2 — High-value (high impact, medium-high effort)

| ID | Item | Effort | When | `<Surface>` | Notes |
|---|---|---|---|---|---|

---

## Tier 3 — Polish (medium impact, low-medium effort)

| ID | Item | Effort | When | `<Surface>` | Notes |
|---|---|---|---|---|---|

---

## Tier 4 — Nice-to-have (low impact, any effort)

| ID | Item | Effort | When | `<Surface>` | Notes |
|---|---|---|---|---|---|

---

## Retired

Items no longer planned. IDs preserved (per `DOCUMENT_TEMPLATES.md § Item IDs` — never reused). Reason ≤80 chars or pointer to a body section / `DECISIONS.md` anchor.

| ID | Item | Reason retired |
|---|---|---|

---

`<Body sections for items whose rationale or context exceeds the 80-char Notes allowance live here, anchored by ID:>`

### `<I-xx>` — `<item title>`

`<Multi-sentence context, implementation hints, dependencies, references.>`

---

*Analyst maintains. Items added at spec sessions; retired when no longer planned. Items assigned to a release move to `ROADMAP.md` under that release.*
