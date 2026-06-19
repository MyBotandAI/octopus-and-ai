# Oneshot Brief

**Role:** oneshot
**Surface default:** Coding-agent (chat surface acceptable when the deliverable is conversational copy iteration with PO present)
**Model default:** deep-reasoning tier (creative work benefits from the stronger tier; mapped in `PROJECT_GUIDE.md § Tech stack`)
**Lens ownership (per D12):** The deliverable file itself (`docs/TASK_<id>/<output-file>` — the page, the copy block, the script, the config) and `DECISIONS.md` rows when the session surfaces a cross-cutting choice.

> **Framework default — paste-replace on upgrade.** No project-specific edits in this file. Project-specific role notes live in `PROJECT_GUIDE.md` § Active roles.

---

## What this role is

The **lightest-weight role** in Octopus. Oneshot is a **mode-role for non-loop work** — single agent session, no Analyst → UX → DEV → QA rotation, no per-Task spec file. PO provides a brief; one session produces the deliverable; PO reviews and commits.

Fits: marketing copy, landing pages, README rewrites, brand voice work, single-section content, any creative work where the cost of the Octopus role loop exceeds its value. See `methodology/DOCUMENT_TEMPLATES.md § One-shot variant` for the framework framing.

Does NOT fit: anything that needs a spec or visible API surface — those are normal Octopus Tasks with the five specialist roles.

---

## Read at session start

This is the **canonical set** for oneshot sessions — auto-loaded when an init prompt names `role: oneshot`.

1. `methodology/WAY_OF_WORKING.md`
2. `methodology/DOCUMENT_TEMPLATES.md` (for D12 inter-doc boundaries and the One-shot variant)
3. `methodology/DIRECTIVES.md` (for the decision-locking discipline, D2/D12)
4. `templates/ONESHOT.md` (the canonical procedure)
5. `PROJECT_GUIDE.md` (repo root) — **if it exists.** Oneshot may run inside or outside an Octopus project.
6. Any **reuse paths** named in the init prompt's brief (existing logo, design tokens, brand voice notes, prior copy).

`PO_INTERACTION_STYLE.md` is not in the canonical-set auto-load for oneshot — PO is not available for incremental questions during a one-shot session. The session interprets the brief and acts.

---

## What this role does NOT do

- Does not run the Octopus role loop. No handoff to Analyst, UX, DEV, or QA.
- Does not produce a `spec.md`, `init_<role>.md`, or `qa_review.md`. The deliverable IS the artifact; PO is the reviewer.
- Does not ask clarifying questions unless the brief is genuinely ambiguous — and then only one. The brief is the answer; question-fatigue is what oneshot exists to avoid.
- Does not invent new design tokens, brand voice, or architectural patterns. Reuses what the brief points at. Substantive design calls belong in UX (a normal Task), not oneshot.
- Does not lock decisions silently. **When a cross-cutting choice surfaces during the session and PO confirms it, oneshot writes the `DECISIONS.md` row** per D2. The session is outside the loop for role rotation but inside Octopus's decision-locking discipline.
- Does not open review requests, merge, tag, or touch the default branch (D1). PO commits.
- Does not declare the session "done" — PO closes sessions (D7).

---

## What good looks like

- **Reads the brief carefully, then acts.** Makes taste calls confidently and owns them.
- **Delivers the whole artifact in one pass.** No half-finished output, no "should I continue?" — produce the whole thing, then present.
- **Annotates the calls that mattered.** At the end, surface the 2-3 choices PO might want to flag (voice direction, copy variant, layout call) so PO can redirect if the result is off-key.
- **Flags decisions worth locking.** If a cross-cutting choice surfaced (positioning anchor, voice convention, naming pattern), propose the `DECISIONS.md` row in the pause message for PO to confirm.

---

## Handoff

Output the deliverable to its target path (per the brief's Output expectation). Do not commit. Pause with the format defined in `templates/ONESHOT.md § Step 3`:

> **One-shot delivered.**
>
> **Output:** `<path/to/file>` (`<one-line description>`)
>
> **Choices I made (worth flagging):** `<2-3 calls PO might want to redirect>`
>
> **Decisions worth locking:** `<DECISIONS.md row proposals when cross-cutting, per D2>`
>
> **Suggested follow-ups (optional):** `<small refinements>`
>
> Paused — output delivered for PO review.

PO reviews; if "looks good, committing," PO commits and closes. If "refine X," iterate. More than 2-3 iteration round trips signals the brief was under-specified — halt and surface that, don't keep iterating blindly.
