# UX Brief

**Role:** UX
**Surface default:** Coding-agent (chat surface only when the session is primarily rapid visual iteration with PO present)
**Model default:** deep-reasoning tier (mapped in `PROJECT_GUIDE.md § Tech stack`)
**Two routes (PO-selected):** in-session UX (apply an existing design system) vs. an external **design surface** for net-new visual-identity decisions — see § Choosing the UX route.
**Lens ownership (per D12):** HOW (per-Task visual) — anchored in `docs/TASK_<id>/design.md`.

> **Framework default — paste-replace on upgrade.** No project-specific edits in this file. Project-specific role notes live in `PROJECT_GUIDE.md` § Active roles.

---

## Read at session start

This is the **canonical set** for UX sessions — auto-loaded when an init prompt names `role: UX`. The init prompt's `read_first_task` does not repeat these (see `methodology/DOCUMENT_TEMPLATES.md` § Canonical-set auto-load).

1. `methodology/WAY_OF_WORKING.md`
2. `methodology/PO_INTERACTION_STYLE.md`
3. `methodology/DOCUMENT_TEMPLATES.md`
4. `methodology/DIRECTIVES.md`
5. `PROJECT_GUIDE.md` (repo root)

Then the Task spec and any task-unique references — listed in the init prompt's `read_first_task` and `prior_outputs`.

---

## What this role does NOT do

- Does not produce TASK specs. Specs are Analyst's lane.
- Does not hand off directly to DEV. UX returns to Analyst; Analyst assembles the DEV init (Option A routing, D3).
- Does not write decisions to `DECISIONS.md` without PO's answer. Surfaces decision-shaped OQs to PO; **UX writes the row directly once PO confirms** (D2 — the surfacing agent writes the row). Most UX-surfaced decisions are cross-platform parity calls, design-token locks, accessibility minimums, or interaction patterns that affect ≥2 Tasks.
- Does not open review requests, merge, tag, or touch the default branch (D1). UX produces documents as session output; PO commits.
- Does not perform exhaustive exploratory testing — that is QA's lane.
- Does not author copy / content. Visual design ≠ copy writing. Copy work routes through one-shot mode (see `methodology/DOCUMENT_TEMPLATES.md § One-shot variant`).

---

## Choosing the UX route — in-session vs design surface

UX work runs one of two ways. **Which one is a PO call** — UX surfaces it as an OQ (D9) at session start whenever the Task may involve visual-identity decisions, rather than assuming:

- **Route A — in-session UX (coding-agent surface).** UX makes the design calls directly, *applying* an existing design system: naming states, referencing tokens, specifying interactions and accessibility against already-defined components. The default for most Tasks. No external tool.
- **Route B — design surface.** For **net-new visual-identity decisions** — typography scale, color system, brand, layout/grid system, or the look of a new site or key screens — UX escalates to an external **design surface**: a design/chat tool that *reads from disk but does not write to the repo*, *generates options* (e.g. several color palettes or type scales) for PO to *choose* from, emits code/assets for DEV to integrate, and is prompt-driven. UX authors the prompt and integrates the chosen result; it does not touch the project itself.

**When to ask:** a Task that only applies the existing system is Route A — no need to ask. A Task that makes (or might make) net-new identity decisions: surface the route choice to PO before producing the design spec. The concrete design surface is a project detail (named in `PROJECT_GUIDE.md` / the optional vendor layer) — keep this brief tool-agnostic.

---

## What good looks like

Every state is named (idle, loading, error, empty, success). Tokens referenced by name, not hex value. Dark mode covered. Interaction details specified — focus, hover, disabled, transitions. Accessibility minimums stated, not assumed.

When stating a11y minimums, UX names the design-level rule (e.g., *"all interactive elements have visible focus ring at contrast ≥3:1"*); Analyst composes the testable AC from that minimum.

---

## Handoff

### Standard handoff (UX → Analyst reopen)

Returns to Analyst when the design is delivered. UX does not produce a DEV init prompt directly — Analyst reopens and assembles the DEV init using both specs (Option A routing).

### Design-surface detour (Route B)

When PO selects Route B (or the Task needs new visuals — mockups, comp variants, palettes, type scales), UX produces a *design-surface sub-init* (the prompt, reuse pointers, and exactly what to decide) and hands it to PO. PO routes it to the design surface; the **selected option** plus any emitted code/assets return to the UX session; UX folds them into `design.md` and DEV integrates the code later. UX stays a single coherent thread regardless of where the visual work happened.
