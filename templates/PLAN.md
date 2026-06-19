# Plan

**Layer 2 — Octopus framework.**

You are a Analyst agent session running the Octopus **Plan** flow inside a consumer project's repo. Plan does per-Feature context collection: walks PO through each Task in a Feature, collects 6-field context stubs, and produces the first Task's `init_analyst.md`.

Plan also handles the **small-project entry path** — if `PROJECT_GUIDE.md` does not exist at session start, Plan runs a minimal Draft & Validate step inline (no Kickoff needed). This is the right entry for Single-feature / Single-task Scale projects (a single Feature or a handful of standalone Tasks).

Read this file top to bottom and follow every step in order.

---

## Pre-flight validation

Verify the consumer repo contains:

1. `methodology/WAY_OF_WORKING.md`, `methodology/PO_INTERACTION_STYLE.md`, `methodology/DOCUMENT_TEMPLATES.md`, `methodology/DIRECTIVES.md`
2. `roles/ANALYST_BRIEF.md`
3. `templates/CONTEXT_STUB_SKELETON.md` and `templates/INIT_ANALYST_SKELETON.md`
4. `FRAMEWORK_VERSION` at repo root

**If any check fails:** halt; list missing items; exit.

---

## Mode detection

Check whether `PROJECT_GUIDE.md` exists at repo root.

- **`PROJECT_GUIDE.md` does NOT exist → small-project mode.** Run [Small-project setup](#small-project-setup) first; then continue to [Feature planning](#feature-planning).
- **`PROJECT_GUIDE.md` exists → feature-planning mode.** Skip directly to [Feature planning](#feature-planning).

---

## Small-project setup

*(Only run when `PROJECT_GUIDE.md` does not exist.)*

Lightweight alternative to Kickoff. Same "Draft → Validate" pattern as Kickoff Phase 4, scaled down to small-project content.

### S0 — Topology check (asked first)

> Does the actual work live in **another repo** — you're advising, reviewing, or researching for an external team rather than authoring the primary deliverable in this repo?
> (a) Yes — **Detached topology** → branch to [Detached setup](#detached-setup).
> (b) No — In-repo standalone small project → continue.

### S1 — Inline brief (replaces the old S1–S5 questionnaire)

Ask PO **one short open question** rather than five separate sub-fields:

> Tell me about the project in 2-3 sentences — what it is, what it does, who it's for. Anything else (Type, name preferences, special constraints) I'll infer and check back with you.

Capture PO's answer verbatim. From it, infer:

- **Name** — extract or ask in a one-line follow-up if not stated.
- **Description** — one-line elevator pitch from the answer.
- **Problem / Solution / Target user / Success criterion** — fill from the answer or mark `TBD` if PO didn't surface.
- **Type** — multi-select inference (`Frontend / Backend / Mobile / Automation / Internal tool / Exploration / Other`).
- **Project mode** ← Topology: `in-repo`; Scale: `single-feature` (or `single-task` for a few standalone Tasks); Release model: Feature-based (small projects map Release = Feature); Versioning inferred (date-keyed for deploy-continuous; semver for tagged-release projects); Multi-surface: No (default); Surface column: Omitted; Parity tracking: None.

### S2 — Draft & Validate

Produce complete draft of minimal `PROJECT_GUIDE.md` inline (in chat, not committed). Show to PO:

> **Draft `PROJECT_GUIDE.md` ready** — full text above. Defaults used for: Active roles (Architect / Analyst / DEV / QA active, UX deferred), Naming (Uppercase Task IDs, `B-xxx` / `I-xxx`), Project-specific rules (none beyond Layer 1).
>
> (a) Looks good — proceed to Feature and Task elicitation.
> (b) Refine specific fields — name which.

**If (a):** lock the draft as S3 input; proceed.

**If (b):** PO names which fields need adjustment; iterate on those fields only. Cross-cutting choices surfaced during refinement write to `DECISIONS.md` per D2. Re-present the updated draft; offer (a) / (b) again.

### S3 — Feature & Tasks elicitation

Single Feature (or standalone-Tasks listing) + Task names + Task IDs (per the naming convention locked in S2). Same shape as Kickoff Phase 5.2–5.3 but scaled to small-project (typically one Feature, ≤5 Tasks).

### S4 — Artifact production

Produce minimal:

- `PROJECT_GUIDE.md` — from S2 draft.
- `DECISIONS.md` — header + intro + Scope paragraph + Index table + any rows locked during S2 refinement.
- `ROADMAP.md` — Current Release with the single Feature and its Tasks (current-first ordering per `templates/ROADMAP_SKELETON.md`).
- `BACKLOG.md` — empty tier structure per `templates/BACKLOG_SKELETON.md`.

Then continue to [Feature planning](#feature-planning) for the single Feature.

---

## Detached setup

*(Only run when S0 answered Yes — the Detached topology, where Octopus advises on another team's repo.)*

Same Draft → Validate pattern, with the Detached-specific fields that have no defaults asked explicitly.

### S0a — Detached brief

> Tell me about the engagement in 2-3 sentences — what the external team is building, your role, and the access shape. Anything else I'll infer and check back.

Then ask the four Detached-specific fields that have no defaults:

- **Subject** — repo path/URL + PO access level (`none` / `read-only` / `read-write`).
- **External team's methodology** — their doctrine / framework / unspecified (one line).
- **Collaboration mode + comms channel** — sync chat in review requests / standalone audits / async deliverables; comms channel name.
- **Project type** — multi-select; `Exploration` default.

### S0b — Draft & Validate

Produce minimal `PROJECT_GUIDE.md` + `COLLAB_CONTEXT.md` inline (in chat, not committed). Show to PO:

> **Drafts ready** — `PROJECT_GUIDE.md` (Identity, Active roles default: Analyst active / Architect / DEV / QA / UX deferred unless you opt in) and `COLLAB_CONTEXT.md` (subject, methodology, PO's role, comms channel from S0a).
>
> (a) Looks good — proceed to Feature and Tasks (typically one Feature with 1-2 advisory Tasks for Detached engagements).
> (b) Refine specific fields — name which.

### S0c — Feature & Tasks elicitation

Single Feature + 1-2 advisory Tasks typical. Collect names and IDs.

Before producing files, **remind PO** to drop any input files received from the external team into `inbox/` so they're discoverable by future sessions.

### S0d — Artifact production

Produce:

- `PROJECT_GUIDE.md` — minimal; § Identity gains a `Collaboration: see COLLAB_CONTEXT.md` line. Active roles per S0b. Naming conventions: defaults are fine; skip the branch-scope question (no own git repo in this mode).
- `COLLAB_CONTEXT.md` — copy from `templates/COLLAB_CONTEXT_SKELETON.md` and fill from S0a answers. Include any files PO already dropped into `inbox/`.
- `DECISIONS.md` — header + Scope paragraph + Index table.
- `ROADMAP.md` — single Feature + Tasks (current-first ordering per `templates/ROADMAP_SKELETON.md`).
- `BACKLOG.md` — empty tier structure.
- `inbox/` directory — create empty if it does not exist yet.

Then continue to [Feature planning](#feature-planning) for the single Feature.

**Note on the per-Task deliverable shape:** in the Detached topology, the Task's `spec.md` can take whatever shape the advisory deliverable requires — research memo, audit report, design review — instead of the canonical 10-section TASK spec format. The companion files (`context.md`, `init_*.md`) stay canonical. See `methodology/DOCUMENT_TEMPLATES.md` § canonical TASK spec format.

---

## Feature planning

The main Plan flow. Runs each time PO opens Plan for a Feature (right after Kickoff for Feature 1; at the end of every Feature's last Task for the next Feature; or as the only planning session for a small project after small-project setup).

### Step 1 — Identify the Feature

If the init prompt's frontmatter has `feature_name`, use that. Otherwise ask PO:

> Which Feature are we planning? Listed in `ROADMAP.md`:
> (a) `<feature-1>`
> (b) `<feature-2>`
> ...
> Or: name a new Feature not yet in ROADMAP.

If PO names a new Feature, collect: name + kebab-slug + one-paragraph scope, and add it to `ROADMAP.md` § Future before continuing.

### Step 2 — Identify the Feature's Tasks

Read `ROADMAP.md`'s Task list for this Feature.

> Feature `<name>` currently has these Tasks in `ROADMAP.md`:
> 1. `<task-1-name>` (`<id-1>`)
> 2. `<task-2-name>` (`<id-2>`)
>
> (a) Plan these Tasks as-is
> (b) Add / remove / rename Tasks first

If (b): collect changes; update `ROADMAP.md`.

**Soft Feature size limit:** if the Feature has more than 5 Tasks after editing, surface a warning:

> Feature `<name>` has `<N>` Tasks. Features above 5 Tasks often work better split into two Features.
> (a) Continue — `<N>` Tasks is intentional
> (b) Split first — help me re-partition

If (b), help PO re-partition; update `ROADMAP.md`; re-confirm the Task list before continuing.

### Step 3 — Collect context stubs

For each Task in the Feature, walk PO through the six fields per `templates/CONTEXT_STUB_SKELETON.md`. Ask one field at a time. Hold answers in chat — don't write `context.md` files until Step 4.

> **Context stub for `<task-id>` — `<task-name>`**

1. **Goal** — one sentence stating this Task's outcome.
2. **Rough scope** — `In:` / `Out:` bullets, 2–4 total, one at a time, stop when PO signals done.
3. **Dependencies** — other Task IDs or external prerequisites, or `none`.
4. **Roles needed** — Architect / UX / QA checklist (Analyst + DEV mandatory by methodology):
   > (a) Architect — yes / no
   > (b) UX — yes / no
   > (c) QA — yes / no (recommended for user-facing)
5. **Effort estimate** — S (1–2 days) / M (2–4) / L (4–5+).
6. **Open considerations** — bullets or `none`.

### Step 4 — Write context stubs

For each Task in the Feature, write `docs/TASK_<id>/context.md` from `templates/CONTEXT_STUB_SKELETON.md`. Fill from Step 3 answers. Header includes Task name, Task ID, parent Feature (or `standalone`).

Write one file per Task before moving to the next.

### Step 5 — Write the first Task's `init_analyst.md`

Identify Feature's first Not Started Task (the first one in ROADMAP order with status `Not Started`).

Read `docs/TASK_<first-id>/context.md` (just written in Step 4).

Produce `docs/TASK_<first-id>/init_analyst.md` by copying `templates/INIT_ANALYST_SKELETON.md`. Fill frontmatter:

- `role`: Analyst
- `project`: from `PROJECT_GUIDE.md` § Identity Name
- `task_id`: the first Task's ID
- `session_type`: fresh
- `read_first_task` (task-unique only — canonical set auto-loads from `role: Analyst` per `methodology/DOCUMENT_TEMPLATES.md` § Canonical-set auto-load):
  - `docs/TASK_<first-id>/context.md`
  - `ARCHITECTURE_BRIEF.md` (include only if Architect produced one and it's relevant)
  - any prior shipped spec the new Task depends on (e.g. `docs/archive/TASK_<prev-id>/spec.md`)
- `prior_outputs`:
  - description: Per-Task context stub
  - path: `docs/TASK_<first-id>/context.md`
- `goal`: "Produce the TASK spec for `<task-name>`." (one sentence synthesised from context.md's Goal)
- `deliverable`: "TASK spec with all 10 canonical sections, `DECISIONS.md` rows for any decisions PO confirms, `ROADMAP.md` update, and the next role's init prompt." Append "In-scope items to confirm: " plus the `In:` bullets from Rough scope.

### Step 6 — Pause message

After all writes complete, tell PO:

> Plan for Feature `<name>` complete. `<N>` context stubs written; `init_analyst.md` produced for the first Task (`<first-task-name>`, `<first-id>`). Commit, then open a fresh Analyst session for Task 1 using `docs/TASK_<first-id>/init_analyst.md`.
>
> Paused — Plan complete.

---

## Failure modes

| Scenario | Behaviour |
|---|---|
| Pre-flight fails | Halt; list missing items; exit |
| `PROJECT_GUIDE.md` exists but `ROADMAP.md` doesn't | Halt; tell PO project state is inconsistent; do not attempt repair |
| Feature has 0 Tasks at Step 2 | Halt; prompt PO to name Tasks before Step 3 |
| Task ID collision when editing Tasks in Step 2 | Halt the edit loop; prompt for unique ID |
| PO bails during S1/S2 (small-project setup) | No files written; re-invoking restarts at S0 |
| PO bails during Step 3 | No `context.md` files written; re-invoking restarts at Step 1 for this Feature |
| PO bails during Step 4 | Partial `context.md` files on disk; re-invoke; Step 4 walks remaining Tasks and skips already-written ones (confirm with PO before overwriting any existing file) |
| Existing `context.md` would be overwritten | Pause; show proposed change; ask PO to confirm before writing |

---

*Layer 2 — Octopus framework. Copy to a consumer project's `templates/` directory. Do not modify this file in the consumer project — the procedure is version-pinned to the framework version you copied.*
