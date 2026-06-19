# Document Templates

**Owner:** PO
**Read by:** Every agent session — referenced when producing or updating documents.
**Purpose:** Defines the canonical document set, the work hierarchy, inter-doc boundaries, the TASK spec format, init prompt format, and naming conventions that apply across all projects. Project-agnostic. Specific content lives in each project's own documents.

---

## Inter-doc boundaries (D12)

Every technical fact has **one canonical home** decided by which lens the fact represents.

| Lens | Doc | What lives here |
|---|---|---|
| **WHY** | `DECISIONS.md` | Cross-cutting choices + rationale. Kebab-case slug + ≤150-char summary + locked date. Body section for longer rationale. |
| **NOW** | `AGENTS.md` / `AGENTS_<component>.md` | Live architecture + rules + gotchas. One-line rules referencing `DECISIONS.md` slugs for the why. |
| **WHEN** | `CHANGELOG.md` | Per-release manifest. Cross-references `DECISIONS.md` slugs, `B-xxx` IDs, commits. |
| **HOW (per-Task)** | `docs/TASK_<id>/spec.md` (or archived) | Screen-level design calls, AC, EC, OQ. Cross-cutting calls promote to `DECISIONS.md`. |

**Cross-document references replace duplication.** Same fact in two places = boundary violation. Agents pick the doc by *which lens* the content represents, not by *which feels right*.

**Practical writing rules:**
- A choice is locked → write `DECISIONS.md` row first; if it constrains future code, add a one-line gotcha in `AGENTS.md` with anchored reference.
- A live rule with no choice involved ("this is how the system works") → `AGENTS.md` only.
- A release shipped → `CHANGELOG.md` entry citing the slugs and bugs touched; no rationale (that's in `DECISIONS.md`).
- A screen-level design call → Task spec only; never promote to `DECISIONS.md` unless cross-cutting.

---

## No prose in tables (D10)

Tables hold atoms (slug, status, size, date, link). Any prose — rationale, scope description, demo bar, background — lives in body sections below the table, referenced by slug. The pattern is the one `DECISIONS.md` originated: index table + per-item body sections.

**Cell allowances:**
- **Default:** ≤80-char trailing parenthetical allowed (e.g. `Done — 2026-05-14 (superseded by DOMAIN_REWORK)`). Anything longer promotes to a body section.
- **`DECISIONS.md` Summary cell:** ≤150 chars (one-sentence authoritative statement).
- **Traceability ledgers (e.g. `PARITY_LOG.md`):** ≤200 chars — the prose is the trace record; strict body-section split doubles doc size for limited gain.

Applies to every doc in the canonical set.

---

## Work hierarchy

Three levels — Epic, Feature, Task. Their interpretation as Releases depends on **Project mode** (declared in `PROJECT_GUIDE.md § Project mode`):

| Project mode | Release maps to | Feature maps to |
|---|---|---|
| Epic-based (big project) | **Epic** (≥2 Features per Release) | Feature (a coherent piece of functionality) |
| Feature-based (small project) | **Feature** (one Feature per Release) | (no separate level) |

**Why:** The planning unit and the shipping unit are the same — one arc, tracked once. The Project mode choice picks whether that arc is named an Epic (big project) or a Feature (small project).

### Epic — strategic grouping (Epic-based projects only)

- Wraps ≥2 Features clustering under a shared strategic thrust.
- Sized in months.
- **No spec.** Just a name, a goal, and a list of child Features.
- Lives in `ROADMAP.md` as a Release.
- Naming: kebab-case (`payments-platform`, `multi-region-launch`).

### Feature — coherent piece of functionality

- A meaningful unit users or developers would recognize.
- Sized in weeks (S ≈ 1 week, M ≈ 2 weeks, L ≈ 3 weeks of solo part-time work).
- **No spec.** Just a name, a one-paragraph scope description, and a list of child Tasks.
- Lives under an Epic in Epic-based projects; lives directly as a Release in Feature-based projects.
- Naming: kebab-case (`kickoff-wizard`, `user-onboarding`).
- Splits into Tasks at Analyst scoping time.

### Task — the unit of delivery

- **The most common unit. Specs only exist at Task level.**
- Sized in days (typically 1–5 days of solo part-time work).
- One spec, one design (if visual), one branch, one DEV ⇄ QA loop.
- Lives in `docs/TASK_<id>/`.
- Tasks can be standalone — bug fixes and small chores don't require a parent Feature.

---

## The canonical document set

Every project uses some subset of the documents below. Not every project starts with all of them — add when earned (per `## Incremental adoption` below). Project-specific docs are also first-class — see `## Project-specific documents`.

### `PROJECT_GUIDE.md` — Registry and context card

The single document any agent reads first. It serves as:

- **Project Context Card** — Identity (Name, Description, Problem, Solution, Target user, Success criterion, Type), Surfaces, Tech stack, Active roles, Current focus.
- **Project mode** — per-project answers to framework configuration questions: Topology (in-repo / detached / no-repo), Scale (multi-feature / single-feature / single-task / one-shot), Release model, Versioning mode, Multi-surface, Surface column usage, Parity tracking.
- **File index** — the registry of every doc in use, including project-specific ones.
- **Documents earned later** — canonical docs not yet created, with the condition that earns each.
- **Project-specific rules** — extensions or overrides on Layer 1 directives.
- **Naming conventions** — project values for IDs, branches, scopes.

PO maintains. Updated when project scope, focus, or structure changes.

### `DECISIONS.md` — Cross-cutting decisions (WHY)

The canonical anchor target for cross-doc references (per Inter-doc boundaries). **Cross-cutting only** — choices affecting ≥2 Tasks, ≥2 files, or ≥2 roles. Single-screen design calls live in their originating Task spec.

**Canonical shape:** index table with kebab-case slugs + ≤150-char Summary + Locked date; body sections per slug for longer Value and Rationale.

`## Superseded Decisions` section at the bottom holds retired rows; old bodies stay in place with `Superseded by:` pointers; new bodies carry `Supersedes:` pointers.

Multi-component projects may add an optional `Surface` column to the index.

Analyst, Architect, or any agent that surfaces a decision per D2 writes the row after PO confirms via OQ. Decisions are immutable once written.

### `AGENTS.md` / `AGENTS_<component>.md` — Live technical context (NOW)

Architecture overview, tech stack detail, key files, live rules, known gotchas. **One-line rules** in this doc reference `DECISIONS.md` slugs for the rationale; multi-paragraph rationale never lives here. `AGENTS.md` is the emerging cross-agent convention for repo-level context; a project whose tooling requires a vendor-specific filename may keep one locally.

Multi-component projects use one `AGENTS_<component>.md` per surface (e.g. `AGENTS.md` + `AGENTS_WEB.md`).

DEV maintains.

### `ROADMAP.md` — Release plan (planning artifact)

Three sections, **current-first**:

1. **Current Release** — drilled down to active Feature(s) with per-Task status.
2. **Future Releases** — Features named with size + scope; no Task drill-down yet.
3. **Past Releases** — historical record.

**Multi-surface projects** split each section per surface.

**Past Releases mode** depends on Project mode versioning:
- `semver-tagged` → per-version rows (`<component>-vX.Y.Z`).
- `date-keyed` → per-Feature rows with shipped date (deploy-continuous projects).

Analyst maintains. Updated after each spec session (status) and after each release.

### `BACKLOG.md` — Tiered unassigned work items

Pure **impact × effort** matrix; time-to-ship in a separate `When` column.

| Tier | Impact | Effort |
|---|---|---|
| 1 | High | Low |
| 2 | High | Medium-high |
| 3 | Medium | Low-medium |
| 4 | Low | Any |

**Estimation gate (D14):** Items default to `## Needs estimation`. Promotion to any tier requires a DEV effort estimate on the row.

`## Retired` section at the bottom preserves IDs for items no longer planned.

Multi-component projects may add an optional `Surface` column.

Analyst maintains.

### `BUGS.md` — Open and fixed bugs

Two tables: Open and Fixed. Each entry has `B-xxx`, severity, repro steps, suspected component, date reported. When a bug is fixed, it moves from Open to Fixed in the same commit as the fix.

QA owns Open intake; DEV may create Open rows for bugs found incidentally during implementation; DEV owns Fixed move. Description cells stay short (symptom + location). Root-cause analysis lives in the fix commit message or in the relevant `qa_review.md` — never inline in `BUGS.md`.

### `CHANGELOG.md` — Per-release manifest (WHEN)

Per-version sections (semver-tagged) or per-feature sections (date-keyed). Cross-references `DECISIONS.md` slugs, `B-xxx` IDs, and commits. **No rationale** — that's `DECISIONS.md`'s job.

Analyst maintains. Written at release-marking Task closure, together with the tag suggestion (see `WAY_OF_WORKING.md` § Task closure). PO commits.

### `OPS.md` — Operations and deploy

Canonical home for ops config (per Inter-doc boundaries). Other docs reference here rather than duplicating.

Sections: Global rules (D13 stop-and-reopen, D1 PO-only deploys), Deploy commands, Infrastructure (with **UI-only callout** for one-time dashboard actions that can't be scripted), Secrets (names + locations only, never values), Procedures, File stewardship.

DEV maintains.

### `CONTRIBUTING.md` — Branch and commit conventions

Branch naming (`<type>/<scope>/<short-description>`), commit format (Conventional Commits — curated 7-type list: `feat`, `fix`, `docs`, `refactor`, `build`, `ci`, `revert`; no `chore`), direct-to-default-branch policy (`docs:` and one-liner `fix:` allowed), hotfix policy, release tags, review-request/merge policy. Names the project's default branch and review-request mechanism (e.g. `main` + pull/merge requests).

Project-specific branch scopes live here.

PO maintains.

### `PRELAUNCH_CHECKLIST.md` — Pre-launch blocking items

Earned when launch is in sight. Lists everything that must be true before public release.

**Multi-surface projects** use per-surface organization: `## Shared` section + one `## <Surface>` section per launchable surface, each with a `Pre-Launch Sign-Off` subsection.

**Pending decisions** subsection surfaces un-locked choices as checkbox items — routed to OQ → `DECISIONS.md` flow when answered.

PO maintains.

### `COLLAB_CONTEXT.md` — Collaboration framing (Detached topology only)

Present only for **Detached-topology** projects (Octopus in a personal folder; the subject is a different team's repo). Names the subject project, external team's methodology, PO's role, comms channel, access level, `inbox/` location, log of outputs handed back.

Plan produces it during setup when PO confirms the Detached topology. PO maintains thereafter.

---

## Project-specific documents

A project may invent docs beyond the canonical set when the work genuinely needs them. Examples: `PARITY_LOG.md` (multi-surface divergence tracking — opt-in template ships in `templates/`), `BRAND_GUIDE.md`, `RUNBOOK_<area>.md`, etc.

Project-specific docs are **first-class citizens** with the same rules:

1. Declare `**Owner:**` at top.
2. Follow Inter-doc boundaries — one lens, references don't duplicate.
3. Follow no-prose-in-tables (with the cell allowances above).
4. Listed in `PROJECT_GUIDE.md § File index` with Owner column — making `PROJECT_GUIDE.md` the **canonical registry** of every doc in use.
5. Cross-doc references use anchored slugs.

Octopus ships **opt-in skeletons** for the most common project-specific patterns (`PARITY_LOG_SKELETON.md`, optionally others as they earn the pattern). Genuinely bespoke docs don't need a skeleton — they need only the five rules above.

---

## Per-surface organization

Multi-surface projects (declared `Multi-surface: Yes` in `PROJECT_GUIDE.md § Project mode`) organize work-tracking docs by surface using one of three patterns:

| Pattern | Used in | When |
|---|---|---|
| **Per-surface sections** (`## Shared / ## <Surface>`) | `PRELAUNCH_CHECKLIST.md` | Section content is mostly per-surface with some shared |
| **Per-surface sub-blocks** within Current / Future / Past | `ROADMAP.md` | Status differs per surface; one block per surface |
| **Optional `Surface` column** | `BACKLOG.md`, `DECISIONS.md` | Same table, surface as a filterable column |

The choice is per-doc, codified in each doc's skeleton. The underlying principle — organize by surface in multi-surface projects — is consistent.

---

## The canonical TASK spec format

The TASK spec is the single most important per-Task artifact. Analyst produces it, UX designs from it, DEV implements against it, QA reviews against it. Its shape is consistent across projects.

### File location and naming

Active Tasks live in per-Task folders at `docs/TASK_<id>/`. Inside the folder, artifacts use short, role-keyed filenames: `context.md` (planning stub), `spec.md` (the Analyst deliverable), `init_<role>.md` (per role handoff), `qa_review.md`, `design.md` (when UX produces one).

Shipped Task folders move to `docs/archive/` after Task ships. Read-only history.

### Section structure

A TASK spec has the following sections, in this order:

**1. Header**

```
# <Project> — <Task name>
## TASK <id>: <short description>

**Status:** <Draft | Specced | In Progress | Shipped>
**Parent feature:** <feature kebab-name, or "standalone">
**Target release:** <version>
**Depends on:** <other Task IDs if any>
**Last updated:** <YYYY-MM-DD>
```

**2. Context** — One to three paragraphs. What this Task delivers, why now, what's bundled, what carry-over fixes are included.

**3. Entry points / scope (if applicable)** — When and how the user encounters this functionality.

**4. Functional spec sections** — Organized by sub-feature or by screen. Tables for fields and behaviors when scannable. Prose for flows and rationale.

**5. User Stories** — `**US-XX — <short title>** As a <user>, I want to <action>, so that <benefit>.` Numbered. Aim for 3–10.

**6. Acceptance Criteria** — `**AC-XX** — <testable assertion>.` Numbered. Yes/no answerable. Post-merge AC tagging available: `**AC-XX** — <testable assertion>. *[Verify after merge — <reason>.]*`

**7. Edge Cases** — `**EC-XX** — <condition>: <expected behavior>.`

**8. Open Questions** — `**OQ-XX** — <question>. <Who can answer, blocks DEV>.`

**9. Backlog Items Added** — New backlog items surfaced; PO confirms and Analyst adds to `BACKLOG.md`.

**10. DECISIONS.md updates required** — Rows written during this session, listed for PO review. `(none)` if no cross-cutting decisions surfaced.

### What a good TASK spec looks like

- **Behaviors are testable.** Every AC can be answered yes/no.
- **Edge cases are explicit.** Don't assume obvious cases are obvious.
- **Open questions are flagged, not glossed.**
- **No technical implementation.** That's DEV's call.
- **Length earns its keep.** A simple Task gets a short spec.

### Spec-less chore variant

A chore Task may run without `spec.md` when fully described by `BUGS.md` rows or PO instruction captured in the chore's `init_<role>.md`. Folder still exists; QA reviews against the bugs or instruction. Per Task closure section in `WAY_OF_WORKING.md`.

### Multi-page build scoping

A multi-page **presentational** build (vitrine / brochure site, every page on one locked design system) is scoped as a **single batched Task on the normal loop** — one spec covering the whole page-set, one design pass over every page's layout/IA, one branch, one QA gate — **not** one Task per page and **not** a one-shot. The build produces the page *structure* with placeholder copy; a separate later Task fills the real copy. The routing, design-depth, and precondition rules live in `WAY_OF_WORKING.md § Multi-page presentational builds`.

**Document set.** The build Task uses the ordinary per-Task folder (`spec.md`, `design.md`, `init_<role>.md`, `qa_review.md`) — it is a normal loop Task. The spec's build brief carries the page-set's per-page scope and the build constraints (no new design tokens, reuse components by composition, locked routes/nav, reuses list, "elevate the existing page" framing, placeholder-copy discipline, build-passes-clean gate). **Content-fill** is a separate later Task — a one-shot (copy is one-shot's native lane) or a spec-less content Task. **Hybrid rule:** any route with a spec or a visible API surface (contact form, auth, payments, SEO infra, deploy) is its own full-loop Task, not part of the presentational build.

### One-shot variant

A Task may declare `mode: one-shot` in its planning stub when the agent has design + copy + implementation latitude in a single session — no role handoffs, no `design.md`, no role-specific init prompts. Fits marketing copy, landing pages, README rewrites, single-section content, and content-fill of an already-built page-set — work where the cost of the role loop exceeds the cost of letting the agent decide.

The Task folder for a one-shot still exists; contents are minimal (`init.md` brief from PO, the output, PO review notes) — this reflects the compressed role loop. **Git and closure follow Topology (D1), not Scale:** an in-repo one-shot branches, commits, pushes, and gets a closure beat like any other Task; only a no-repo / standalone one-shot routes closure straight back to PO with disk-only saves. See `WAY_OF_WORKING.md § One-shot Scale`, `templates/ONESHOT.md`, and `roles/ONESHOT_BRIEF.md`.

**Copy / content ownership.** Marketing copy, prose content, voice work, and similar writing tasks route through one-shot mode — none of the five specialist roles owns copy as a lane. UX owns visual design (tokens, states, interactions) but not the words; Analyst writes specs about behavior, not prose. When a project needs copy work, the right entry is `roles/ONESHOT_BRIEF.md`, not a specialist Task.

### Spec shape in Detached topology

In **Detached-topology** projects (where `COLLAB_CONTEXT.md` is present), `spec.md` may take whatever shape the advisory deliverable requires — research memo, audit report, design review, recommendation summary — instead of the canonical 10-section TASK spec above. The companion files (`context.md`, `init_<role>.md`, `qa_review.md` when QA is invoked) stay canonical regardless of topology.

---

## Per-Task companion artifacts

The TASK spec is the central artifact, but the per-Task folder typically holds a few other short-named files:

- **`context.md`** — the planning stub produced **by a Plan session** before the Task's spec session runs. Six sections: Goal, Rough scope, Dependencies, Roles needed, Effort estimate, Open considerations. See `templates/CONTEXT_STUB_SKELETON.md`.
- **`init_<role>.md`** — one per role handoff for this Task (`init_analyst.md`, `init_dev.md`, `init_qa.md`, etc.). Format per `## Init prompt format` below.
- **`qa_review.md`** — QA's acceptance review document. When the spec has any AC tagged *[Verify after merge — …]*, the review ends with a `## Post-merge checklist` section listing each post-merge AC as an imperative for PO to run after merging.
- **`design.md`** — UX's design spec, when the Task has a visual surface.

None of these are mandatory for every Task — a bug fix folder may contain only `spec.md`, `init_dev.md`, `init_qa.md`, and `qa_review.md`. The folder grows as roles produce.

Intra-Kickoff handoffs (e.g., `docs/init_architect_kickoff.md`, `docs/init_analyst_kickoff_resume.md`) and the **Kickoff → Plan handoff** (`docs/init_analyst_plan_<feature-kebab>.md`) live at `docs/` root — they predate any per-Task folder and are Feature-level rather than Task-scoped.

---

## Init prompt format

When a role hands off to the next role in the common path, it produces an init prompt — a structured artifact that initializes the next session.

### Format

Init prompts are markdown files with YAML frontmatter. The frontmatter is machine-readable; the body is the human-readable prompt that the agent consumes.

```markdown
---
role: DEV
project: example-app
task_id: USER_AUTH
session_type: fresh
read_first_task:
  - docs/TASK_USER_AUTH/spec.md
  - docs/TASK_USER_AUTH/design.md
prior_outputs:
  - description: TASK spec
    path: docs/TASK_USER_AUTH/spec.md
  - description: Design spec
    path: docs/TASK_USER_AUTH/design.md
goal: Implement user authentication per the spec and design.
deliverable: A task branch with implementation, automated tests passing, per-change Conventional Commits, BUGS.md updates if any bugs are fixed in passing.
---

# DEV Init — User Auth

## Pre-flight — read before engaging PO

**No output until every file is read. No permission-asks. No mid-read check-ins.**

Read in order:
1. `methodology/WAY_OF_WORKING.md`
2. `methodology/PO_INTERACTION_STYLE.md`
3. `methodology/DOCUMENT_TEMPLATES.md`
4. `methodology/DIRECTIVES.md`
5. `roles/DEV_BRIEF.md`
6. `PROJECT_GUIDE.md`
7. `DECISIONS.md`
8. Project technical-context file (`AGENTS.md` or equivalent per `PROJECT_GUIDE.md § File index`).
9. Every path in `read_first_task` above, in order.

After reading: proceed directly to role work.

---

You are DEV for `example-app`. ...
```

### Canonical-set auto-load

Every session reads in this order at start:

1. **Layer 1 quartet** — `methodology/WAY_OF_WORKING.md`, `methodology/PO_INTERACTION_STYLE.md`, `methodology/DOCUMENT_TEMPLATES.md`, `methodology/DIRECTIVES.md`.
2. **The role brief** — `roles/<ROLE>_BRIEF.md` per the init prompt's `role:` field.
3. **Project core** — `PROJECT_GUIDE.md` plus the project docs the role brief's "Read at session start" lists (e.g. `DECISIONS.md`, `ROADMAP.md`, `AGENTS.md`).
4. **The init prompt's `read_first_task` entries** — the unique-to-this-session set.

Items 1–3 are the **canonical set**, owned by the role brief — agents load them automatically from the `role:` field. The init prompt's `read_first_task` is task-unique only. The produced prompt's body must **enumerate** this read order as concrete paths in its `## Pre-flight` block (see § Pre-flight block is required), not merely reference the auto-load convention.

**All four layers are read before producing any output.** See `WAY_OF_WORKING.md § Session protocol § At session start` and the pre-flight block in each init skeleton.

### Pre-flight block is required

Every produced init prompt for a fresh role session **must** include a `## Pre-flight — read before engaging PO` block in its human-readable body, enumerating the canonical read set (Layer 1 quartet → role brief → project core docs → `read_first_task`) as **concrete paths in read order** — as shown in the example above. A bare reference to the auto-load convention (e.g. *"auto-loaded from your `role:`"*) is **insufficient**: the convention is defined inside the methodology files the agent has not yet read, so a reference alone cannot bootstrap the read.

The producing agent **copies the target role's pre-flight block from `templates/INIT_<ROLE>_SKELETON.md`** — the single source of truth for each role's canonical file list. The block is not duplicated per role into this document. Project-specific path resolution (e.g. technical-context file not at `AGENTS.md`) follows `PROJECT_GUIDE.md § File index`, as the skeleton already shows.

Frontmatter is unaffected: `read_first_task` stays task-unique (canonical files are not added back to frontmatter). The enumerated list lives only in the body block.

**Exempt:** reopen briefs and detour handoffs (DEV→Analyst spec-ambiguity note, QA→DEV review, Analyst→Architect reopen brief) are not fresh-session role inits and carry no pre-flight block.

### Required frontmatter fields

| Field | Type | Description |
|---|---|---|
| `role` | string | One of: `Architect`, `Analyst`, `UX`, `DEV`, `QA`, `oneshot` |
| `project` | string | Project name (matches `PROJECT_GUIDE.md`) |
| `task_id` | string | Task this session works on; omit for non-task sessions |
| `session_type` | string | `fresh` or `reopen` |
| `read_first_task` | list | Task-unique paths the session must read at start |
| `prior_outputs` | list | What previous roles produced; each entry has `description` and `path` |
| `goal` | string | One-sentence description of what this session must achieve |
| `deliverable` | string | Concrete output expected at session pause |

Optional fields the project may add: `parent_feature`, `parent_epic`, `branch_name`, `tools_required`, `model` (when overriding the role's default).

### YAML frontmatter gotcha

Avoid internal `: ` (colon followed by space) inside any unquoted scalar value — strict YAML 1.1 parsers will read it as a nested mapping and reject the file. Either rewrite to remove the colon or quote the entire value with single quotes. The em-dash `—` is safe; colons are not.

### Where init prompts live

Inside the per-Task folder: `docs/TASK_<id>/init_<role>.md`. Init prompts are committed alongside other Task artifacts as the durable record of how each handoff was framed.

In detour cases (DEV → Analyst reopen, QA → DEV after Fail/Flag, Analyst → Architect reopen), the init prompt is replaced by the document that triggered the detour — the spec ambiguity note, the QA review report, or the short Architect reopen brief.

---

## Naming conventions

### Hierarchy and IDs

| Level | Naming | Example |
|---|---|---|
| Epic | kebab-case | `payments-platform`, `multi-region-launch` |
| Feature | kebab-case | `kickoff-wizard`, `user-onboarding` |
| Task | Folder `TASK_<id>/` with short-named contents | `docs/TASK_USER_AUTH/spec.md` |

### Item IDs

| Prefix | Used for | Example |
|---|---|---|
| `B-xxx` | Bugs in `BUGS.md` | `B-012` |
| `I-xxx` | Backlog items in `BACKLOG.md` | `I-43` |
| `P-xxx` | Parity items in `PARITY_LOG.md` (multi-surface only) | `P-04` |
| `D<n>` | Directives in `DIRECTIVES.md` | `D1`, `D14` |
| `US-XX` | User stories within a Task spec | `US-01` |
| `AC-XX` | Acceptance criteria within a Task spec | `AC-05` |
| `EC-XX` | Edge cases within a Task spec | `EC-02` |
| `OQ-XX` | Open questions within a Task spec | `OQ-01` |

`B-xxx`, `I-xxx`, `P-xxx` are project-wide and never reused. `US-xx`, `AC-xx`, `EC-xx`, `OQ-xx` are scoped to their Task spec.

### Branches

Format: `<type>/<scope>/<task-short-description>`. **One branch per Task.** Branches are not per Feature — Features that span multiple Tasks ship as multiple branches over multiple DEV ⇄ QA loops.

Types: `feat`, `fix`, `refactor`, `build`, `ci`, `docs`, `hotfix`, `spike`. Scopes are project-specific and named in the project's `CONTRIBUTING.md`.

### Commits

Conventional Commits format: `<type>(<scope>): <imperative subject ≤72 chars>`. Curated 7 types: `feat`, `fix`, `docs`, `refactor`, `build`, `ci`, `revert`. Detail in `CONTRIBUTING_SKELETON.md`.

### Release tags

Format: `<component>-v<semver>` for semver-tagged components. Date-keyed projects (per Project mode) do not use tags — the commit date serves as the key.

### Dates

Always `YYYY-MM-DD`. Never `MM/DD/YYYY`, never `DD-MM-YYYY`, never written-out months.

---

## Incremental adoption

A new project does not need every document on day one. Minimum to bootstrap:

- `PROJECT_GUIDE.md` (even sparse — Identity, Surfaces, Active roles, Project mode).
- `AGENTS.md` (even just tech stack + codebase root pointer).
- `DECISIONS.md` (empty, ready to fill).

Add the rest as the project earns them — record the planned additions in `PROJECT_GUIDE.md § Documents earned later` with the trigger condition:

- `ROADMAP.md` / `BACKLOG.md` — when there are enough items to organize.
- `BUGS.md` — when bugs start arriving (i.e. when there are users).
- `CHANGELOG.md` — when the first release ships.
- `OPS.md` — when there's something operational to document.
- `CONTRIBUTING.md` — when more than one branch type exists.
- `PRELAUNCH_CHECKLIST.md` — when launch is in sight.
- `PARITY_LOG.md` — when ≥2 surfaces ship in parallel with potential divergence.

Pre-creating empty documents is a smell — they pretend the project has structure it hasn't earned, and invite filler content.

Init prompts are produced from the first Task onward, regardless of project maturity.

---

*Layer 1 — methodology baseline. Project-agnostic. Updated when the canonical document set, inter-doc boundaries, work hierarchy, TASK spec format, init prompt format, or naming conventions evolve.*
