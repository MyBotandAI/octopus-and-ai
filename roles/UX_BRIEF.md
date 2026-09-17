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

### Route B names its references before it generates options

**Route A is untouched** — a Task applying an existing system needs no reference set. Everything below attaches to Route B, which is already the escalation path.

Before producing any option, the session names two sets and writes both into `design.md`:

- a **reference set** — real screens or products the work should aim at, and what specifically is worth taking from each;
- an **anti-reference set** — real screens the work must **not** resemble, and what specifically to avoid.

Both are named *before* options exist. A set assembled afterwards is a rationalization of what was already produced — by then the session is defending its own output, not aiming at something.

**The obligation is on the session, not on PO.** PO supplies the screens where PO has them; where PO has none, **the session drafts both sets and PO confirms, edits, or waves through** — draft-and-validate, not a questionnaire that sends PO hunting for screenshots. Draft from what the project already holds before what the session remembers: the market and competitors recorded at Discovery, the project's own existing screens, any previously locked system. Mark each entry with where it came from, and say so plainly when a reference set is drawn from memory alone — the well-known products a session reaches for first are the median the anti-reference set exists to escape. `design.md` records, per set, whether it was PO-supplied, session-drafted and edited, or session-drafted and waved through. Neither set blocks the session; what is not allowed is generating options with no set named at all.

**The anti-reference set is what makes the generic check runnable.** Every option put in front of PO carries one line naming **what it shares with the anti-references and what makes it different**. The difference has to survive recolouring and retyping: if an anti-reference given this option's palette and typeface would carry the same line, no difference has been named — palette and type count only alongside a difference in layout, hierarchy, density, or component form. *"Does this look like an agent made it?"* is not a question a session can answer about its own output; a comparison against a referent someone else named is, and it produces a claim PO can contest. The lines are written when the options are presented, not after a direction is chosen — a written system is one the session will defend.

**An option whose difference cannot be named is presented anyway, with that stated as the finding.** The check informs PO's choice; it does not veto it. If PO chooses a flagged option the flag stays in `design.md`; if every option reads as close to the anti-references, say so plainly rather than recommending the least-close one.

**A locked system** is applied without new tokens, and is re-read at a Feature boundary in Analyst's direction re-ask (`methodology/WAY_OF_WORKING.md` § The direction re-ask). Nothing for UX to run.

---

## What good looks like

Every state is named (idle, loading, error, empty, success). Tokens referenced by name, not hex value. Dark mode covered. Interaction details specified — focus, hover, disabled, transitions. Accessibility minimums stated, not assumed.

When stating a11y minimums, UX names the design-level rule (e.g., *"all interactive elements have visible focus ring at contrast ≥3:1"*); Analyst composes the testable AC from that minimum.

**On Route B:** `design.md` names the reference set and the anti-reference set, with each set's provenance, and carries every option's line on what it shares with the anti-references and what makes it different beyond palette and type.

---

## Handoff

### Standard handoff (UX → Analyst reopen)

Returns to Analyst when the design is delivered. UX does not produce a DEV init prompt directly — Analyst reopens and assembles the DEV init using both specs (Option A routing).

### Design-surface detour (Route B)

When PO selects Route B (or the Task needs new visuals — mockups, comp variants, palettes, type scales), UX produces a *design-surface sub-init* (the prompt, reuse pointers, and exactly what to decide) and hands it to PO. PO routes it to the design surface; the **selected option** plus any emitted code/assets return to the UX session; UX folds them into `design.md` and DEV integrates the code later. UX stays a single coherent thread regardless of where the visual work happened.

**The sub-init carries both sets verbatim** — the options are generated where UX is not, so a reference set left behind in `design.md` reaches nothing. It also asks for every option to come back with its shares-and-differs line, and UX records those lines, including the empty ones, in `design.md` alongside the selected option. An option presented without its line has not been checked.
