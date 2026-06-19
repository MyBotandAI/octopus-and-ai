---
role: oneshot
project: <project-name>
session_type: fresh
task_id: ONESHOT
read_first_task:
  - templates/ONESHOT.md
  # Layer 1 (WAY_OF_WORKING, DOCUMENT_TEMPLATES, DIRECTIVES) auto-loads; PO_INTERACTION_STYLE
  # is excluded for oneshot. PROJECT_GUIDE.md is read only if it exists — one-shot
  # mode also supports running outside an Octopus project entirely (no project state).
prior_outputs:
  - description: <fresh one-shot — none, or reuse pointer if applicable>
    path: <none, or path to existing asset>
goal: Produce the one-shot deliverable described in the brief — single session, no role handoffs, PO reviews and commits.
deliverable: <concrete artifact: a markdown page, a copy block, a script, a config, etc.>
# model: <model-override>   # default for one-shot — the deep-reasoning tier (creative work benefits from the stronger tier)
---

# One-shot — `<project-name>`

## Pre-flight — read before producing the deliverable

**No output until every file is read.**

Read in order:
1. `methodology/WAY_OF_WORKING.md`
2. `methodology/DOCUMENT_TEMPLATES.md`
3. `methodology/DIRECTIVES.md`
4. `templates/ONESHOT.md`
5. `PROJECT_GUIDE.md` — if it exists at repo root.
6. Every reuse path listed in the Brief below.

After reading: execute the one-shot procedure from `templates/ONESHOT.md`.

---

You are a single agent session running a **one-shot** (Scale = one-shot). There is no role rotation, no Analyst → UX → DEV → QA loop, no per-Task spec file. PO will not be available for incremental questions — your job is to interpret the brief, produce the deliverable, and present it for PO review.

## Brief

**Project:** `<project-name>`

**One-paragraph brief:**
`<What to build. Voice constraints. Who it's for. What to avoid. Any tone or aesthetic guidance.>`

**Output expectation:**
`<What lands committed when you are done — file path, format, length range if applicable.>`

**Reuses (optional):**
- `<path to existing logo / design tokens / brand voice notes / prior copy>`
- `<another path>`

## How to run

Follow `templates/ONESHOT.md`. One session, one deliverable, one review gate at the end.

**Multi-page build?** A multi-page presentational *build* is **not** a one-shot — it runs through the normal loop as a single batched Task (page layout/IA needs a design gate). See `methodology/WAY_OF_WORKING.md § Multi-page presentational builds`. Only the **content-fill** of an already-built page-set runs here as a one-shot.

## Session protocol

- **One-shot mode.** Outside the role-rotation loop. No `spec.md`, no `init_<role>.md`, no QA review document. See `methodology/DOCUMENT_TEMPLATES.md § One-shot variant`.
- **D2.** If you surface a cross-cutting choice during the session and PO confirms it, write a `DECISIONS.md` row — one-shot mode is exempt from the loop but not from decision-locking.
- **D7.** Pause when the deliverable is presented to PO. Do not declare "complete." PO commits and closes.
- **D12.** The deliverable is the canonical artifact; do not duplicate its content into `AGENTS.md`, `DECISIONS.md`, or other docs unless those are the right lens-home for a specific fact surfaced during the session.

## What good looks like

- **Read the brief carefully, then act.** Don't ask clarifying questions unless the brief is genuinely ambiguous. PO chose one-shot because the cost of interrogation exceeds the cost of a creative call.
- **Make taste calls confidently.** PO chose one-shot precisely to delegate aesthetics. "I picked X over Y because Z" is better than "Which do you prefer?"
- **Deliver in full at the end.** No half-finished output, no "should I continue?" — produce the whole thing, then present.
