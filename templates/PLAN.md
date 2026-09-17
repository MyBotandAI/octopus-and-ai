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

Read `ROADMAP.md`'s Task list for this Feature. For each Task, check whether `docs/TASK_<id>/context.md` already exists — a Task with a stub is **already planned**; a Task with none is **not planned yet**. This check is what makes re-invoking Plan on a Feature that already has Tasks in `ROADMAP.md` but no `docs/` at all (a half-planned project) recover cleanly rather than re-eliciting or overwriting anything already on disk.

> Feature `<name>` currently has these Tasks in `ROADMAP.md`:
> 1. `<task-1-name>` (`<id-1>`) — already planned
> 2. `<task-2-name>` (`<id-2>`) — not planned yet
>
> (a) Plan the not-planned Tasks — Tasks that already have a context stub are left untouched
> (b) Add / remove / rename Tasks first

If (b): collect changes; update `ROADMAP.md`; re-check stub presence for the edited list before continuing.

**If every Task already has a `context.md`,** tell PO: "Every Task in `<name>` is already planned — nothing to write here. Open Run to continue the loop." and stop; do not run Steps 3–5.

**Soft Feature size limit:** if the Feature has more than 5 Tasks after editing, surface a warning:

> Feature `<name>` has `<N>` Tasks. Features above 5 Tasks often work better split into two Features.
> (a) Continue — `<N>` Tasks is intentional
> (b) Split first — help me re-partition

If (b), help PO re-partition; update `ROADMAP.md`; re-confirm the Task list before continuing.

### Step 3 — Draft & Validate context stubs (replaces the old field-by-field questionnaire)

For the **not-planned** Tasks identified in Step 2 only — a Task that already has a `context.md` is skipped entirely here, never re-drafted — **draft each Task's six-field context stub** from what you already have (the Feature and Task names, `PROJECT_GUIDE.md`, `DECISIONS.md`, and any prior shipped specs the Tasks depend on), rather than interrogating PO field by field. Hold the drafts in chat — don't write `context.md` files until Step 4.

Draft all six fields per `templates/CONTEXT_STUB_SKELETON.md`, **proposing** sensible values PO can correct:

1. **Goal** — one sentence stating the Task's outcome, synthesised from its name + the Feature's scope.
2. **Rough scope** — `In:` / `Out:` bullets (2–4 total) inferred from the Task's role in the Feature.
3. **Dependencies** — other Task IDs (infer from execution order / names) or external prerequisites, or `none`.
4. **Roles needed** — Analyst + DEV are mandatory; **propose** UX (if the Task has a visual surface), QA (recommended for anything user-facing), and Architect (if it carries a structural decision).
5. **Effort estimate** — a **proposed** S (1–2 days) / M (2–4) / L (4–5+); PO (or DEV at the estimation gate, D14) corrects it.
6. **Open considerations** — bullets or `none`.

Present **all** drafted stubs together and ask PO to validate — the same Draft → Validate shape as S2:

> **Draft context stubs ready** — `<N>` stubs above (`<task-1-name>`, `<task-2-name>`, …). Proposed roles, dependencies, and effort per Task are my inference from the Feature — correct anything I got wrong.
>
> (a) Looks good — proceed to write them.
> (b) Refine specific stubs or fields — name which.

**If (a):** proceed to Step 4.

**If (b):** PO names which stubs/fields need adjustment; iterate on those only. Cross-cutting choices surfaced during refinement write to `DECISIONS.md` per D2. Re-present the updated drafts; offer (a) / (b) again.

A field you genuinely can't infer (a dependency only PO knows) is drafted as a best guess or `TBD` — the validate step is where PO fills it, exactly as S1 marks un-surfaced pitch fields `TBD`.

### Step 4 — Write context stubs

For each Task drafted in Step 3 (the not-planned ones only), write `docs/TASK_<id>/context.md` from `templates/CONTEXT_STUB_SKELETON.md`. Fill from the Step 3 drafts as validated by PO. Header includes Task name, Task ID, parent Feature (or `standalone`).

Write one file per Task before moving to the next. **Never overwrite a Task's existing `context.md`** — Step 2/3 already excluded any Task that has one, so this step only ever creates new files. This is what makes recovery idempotent: re-running Plan on the same Feature after every Task is planned writes nothing and changes nothing on disk.

### Step 5 — Write the first Task's `init_analyst.md`

**Identify the target Task from the Tasks *this session* just planned in Step 4 (its stub-write batch) — never from ROADMAP status text.** ROADMAP `Status` cells are not kept in sync with planned/not-planned state (that's `context.md` presence, Step 2's concept), so "the first ROADMAP row reading `Not Started`" can silently be a *different*, already-planned Task in a recovery session — picking it would hand `init_analyst.md` to the wrong Task and leave the Task this session actually recovered with no handoff at all, permanently (re-running Plan later finds every Task planned and stops at Step 2, so this never self-heals).

Search Step 4's write batch, in ROADMAP order, for the first Task whose `docs/TASK_<id>/init_analyst.md` does not yet exist — call it `<first-id>`.

- **If Step 4's batch is empty** (Step 2 already found every Task planned and stopped before Step 3), there is nothing to hand off — skip this step entirely.
- **If every Task in the batch already has an `init_analyst.md`** (unexpected — a newly-stubbed Task normally has no handoff yet), skip this step; nothing to write.
- **Otherwise, if `docs/TASK_<first-id>/init_analyst.md` already exists** for the resolved Task, leave it untouched and skip this step — that Task was already handed to Analyst.

Read `docs/TASK_<first-id>/context.md` (written in Step 4).

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

> Plan for Feature `<name>` complete. `<N>` context stubs written`<, M already planned and left untouched>` (omit the `M` clause when it's zero); `init_analyst.md` produced for the first Task (`<first-task-name>`, `<first-id>`)`< — already existed, left untouched>` (use the second form when Step 5 was skipped). Commit, then open a fresh Analyst session for Task 1 using `docs/TASK_<first-id>/init_analyst.md`.
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
| PO bails during Step 4 | Partial `context.md` files on disk for this session's not-planned batch; re-invoking re-runs Step 2, which finds the still-unstubbed Tasks and re-offers only those in Step 3 — nothing already written is touched |
| A Task already has a `context.md` that Step 2's check didn't expect (concurrent edit/race) | Pause; show the proposed change; ask PO to confirm before writing — never silently overwrite |
| **Recovery — Feature's ROADMAP Tasks exist but `docs/` never existed** (the half-planned-project shape) | Step 2 finds every Task not-planned; Step 3 walks all of them; Step 4 writes every stub; Step 5 writes the first Task's `init_analyst.md` from that same batch — identical to planning a brand-new Feature, no special-casing needed |
| **Recovery — some Tasks already planned, others not** (a genuine mid-planning state, not the ROADMAP's `Status` text) | Step 2 finds and skips the already-planned Tasks; Step 3/4 walk and stub only the not-planned ones; **Step 5 targets the first Task in *that* batch**, never "the first ROADMAP row reading `Not Started`" — an already-planned Task's stale ROADMAP status must never steal the handoff meant for the Task this session actually recovered (B-026) |
| Every Task in the Feature already has a `context.md` (re-invoking an already-planned Feature) | Step 2 reports nothing to do; Steps 3–5 do not run; no files are read or written — idempotent no-op |
| A Task was planned in an earlier session but still has no `init_analyst.md` (that session ended before its own Step 5, or wrote it for a different Task), and this session's Step 2 finds no not-planned Tasks left to recover | Step 4's batch is empty this session (nothing new to stub), so Step 5 has no batch to search and skips — this stale Task's missing handoff is **not** self-healed by re-invoking Plan. Surface it to PO as an Open Question rather than silently leaving it stuck; `docs/TASK_<id>/init_analyst.md` can be produced directly from the existing `context.md` as a one-off if PO confirms |

---

*Layer 2 — Octopus framework. Copy to a consumer project's `templates/` directory. Do not modify this file in the consumer project — the procedure is version-pinned to the framework version you copied.*
