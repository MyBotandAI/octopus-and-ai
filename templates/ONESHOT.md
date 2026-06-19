# One-shot procedure

**Layer 2 — Octopus framework.**

You are a single agent session running a one-shot (Scale = one-shot). **No role handoffs. No `spec.md`. No QA loop.** PO provides a brief; you produce the deliverable; PO reviews. (Git follows Topology, not Scale — see Steps 3 and 5.)

This procedure is the right entry for: marketing copy, landing pages, README rewrites, brand voice work, single-section content, content-fill of an already-built multi-page site, and any creative work where the cost of the Octopus role loop exceeds its value.

A multi-page presentational **build** (designing and building a whole page-set on a locked design system) is **not** a one-shot — page layout/IA is real design work that needs a UX gate, so it runs through the normal loop as a single batched Task. See `methodology/WAY_OF_WORKING.md § Multi-page presentational builds`. Only the **content-fill** of an already-built page-set runs here.

Read this file top to bottom and follow every step in order.

---

## Pre-flight validation

Verify the consumer environment contains:

1. `methodology/WAY_OF_WORKING.md`, `methodology/DOCUMENT_TEMPLATES.md` (One-shot variant reference), and `methodology/DIRECTIVES.md`.
2. Any reuse paths named in the init prompt's Reuses section (logo, tokens, prior copy).

**If a referenced reuse path doesn't exist:** surface to PO before proceeding; do not improvise.

If running **outside** an Octopus project entirely (PO invoked one-shot directly on a folder with no `methodology/`), proceed without the framework reference — the procedure below stands on its own.

---

## Step 1 — Internalize the brief

Read the brief from the init prompt. Three checks before generating:

1. **Output expectation is concrete.** A file path or named artifact, not "a section about X." If genuinely ambiguous, ask one clarifying question — but only one. One-shot's value is bypassing question-fatigue.
2. **Voice and constraints are clear.** Who is this for; what to avoid; tone notes. If the brief has none, default to PO's existing voice (read project's existing artifacts if available).
3. **Reuses are loaded.** If the brief points at design tokens, brand voice notes, or prior copy, read them now — they shape the deliverable.

Do **not** ask the brief's questions back to PO. The brief is the answer.

---

## Step 2 — Produce the deliverable

Generate the whole artifact in one pass. Make taste calls confidently and own them:

- **Voice:** match the constraints in the brief; otherwise match the project's existing voice (per Step 1).
- **Visual:** if relevant, reuse design tokens from the brief's Reuses; never invent new design tokens in a one-shot (that's a real design call belonging in a UX session).
- **Length:** match the output expectation; if the brief says "≤200 words," cap there.
- **References:** if the brief mentions specific receipts (shipped products, prior projects), incorporate them concretely with named anchors.

When a choice surfaces between two defensible options (e.g., scarcity-flavored CTA vs urgency-flavored CTA, "founder" vs "solo operator"), **pick one and proceed** — annotate the choice briefly at the end of the session so PO can flag if they want the alternative.

---

## Step 3 — Present for PO review

Output the deliverable to its target path (per the brief's Output expectation), then pause for PO review.

**Git follows Topology (D1), not Scale** — Scale = one-shot compresses the role loop, not the git discipline:

- **In-repo** — work on a task branch, commit per logical change, and push at this pause, exactly as any in-repo session does (D1). PO reviews and merges.
- **No-repo / standalone** — do not commit; PO handles any saving. This is the only case that matches the old "PO commits" default.

Pause with this format:

> **One-shot delivered.**
>
> **Output:** `<path/to/file>` (`<one-line description of what's in it>`)
>
> **Choices I made (worth flagging):**
> - `<choice 1 — one-line gloss>`
> - `<choice 2 — one-line gloss>`
>
> **Decisions worth locking (per D2):**
> - `<if any cross-cutting choice surfaced — propose a DECISIONS.md row for PO to confirm>`
>
> **Suggested follow-ups (optional):**
> - `<small refinements, alternative angles, or future iterations>`
>
> Paused — output delivered for PO review.

---

## Step 4 — Iterate if PO asks

PO may respond with:

- **"Looks good — committing"** → session ends; PO commits.
- **"Refine X"** → make the focused change, present again. One iteration loop typical; more than 2-3 round trips is a signal that the brief was under-specified.
- **"Different direction entirely"** → if the redirect is substantial, halt and surface that a fresh one-shot might be cleaner than continuing this one. PO decides.

If PO confirms a decision-shaped choice during iteration, write the `DECISIONS.md` row per D2 before pausing again.

---

## Step 5 — Closure

When PO accepts the deliverable, the session pauses (per D7); PO closes. Closure follows Topology (D1): an **in-repo** one-shot gets the normal closure beat — the branch merges and the Task is recorded in `ROADMAP.md` / archived like any other; a **no-repo / standalone** one-shot closes straight back to PO with disk-only saves. Either way the Task folder (`docs/TASK_<id>/` or wherever the brief named) ends up containing only:

- `init.md` (the brief PO pasted to start the session)
- The deliverable
- PO's review notes (optional, free-form)

No `spec.md`, no `init_<role>.md`, no `qa_review.md` — the role loop is compressed even though git is not. This is the point of one-shot.

---

## Failure modes

| Scenario | Behaviour |
|---|---|
| Brief is genuinely ambiguous | Ask ONE clarifying question; if still unclear, halt and ask PO to revise the brief |
| Reuse path doesn't exist | Halt; surface to PO; do not improvise replacements |
| Cross-cutting decision surfaces | Write the `DECISIONS.md` row per D2; do not bury the choice silently |
| PO asks for >3 iterations | Halt; surface that the brief was under-specified; offer to restart with a tighter brief |

---

*Layer 2 — Octopus framework. Copy to a consumer project's `templates/` directory. One-shot mode does not lock the framework version — it's a single-session entry point that can run independently of project state.*
