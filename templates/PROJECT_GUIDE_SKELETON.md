# `<project-name>` — Project Guide

**Owner:** PO
**Updated:** `<YYYY-MM-DD>`

This is the single entry point for the repo. Read this first when starting a fresh session.

---

## Identity

The canonical Identity table is required for every project. Complex multi-surface projects may add a short prose paragraph above the table to frame the project, but the structured sub-fields below remain mandatory — they answer the questions a fresh agent needs.

- **Name:** `<project-name>`
- **Description:** `<one-line elevator pitch — what this is>`
- **Problem:** `<one sentence on what's broken or missing today>`
- **Solution:** `<one sentence on what this project provides — distinct from Description; the offering>`
- **Target user:** `<who benefits>`
- **Success criterion:** `<how PO will know it worked>`
- **Intent:** `<personal | prospective | commercial>`
- **Market:** `<who else already does this, and what people use today — one or two sentences. "Not looked at yet" when that is the truth; never blank.>`
- **Type:** `<comma-separated from: Frontend, Backend, Mobile, Automation, Internal tool, Exploration, Other>`
- **Collaboration:** `<see COLLAB_CONTEXT.md — present only when this project's Topology is Detached; omit this line otherwise>`

**Intent** answers *why this is being built*, and it is a closed choice because the framework reads it: `personal` (a tool, an exploration, or a project PO steers for someone else — nobody outside is meant to pay; a community or open-source project with no revenue intent files here), `prospective` (built as an MVP with the prospect of becoming a business), `commercial` (someone is meant to pay for it now). `prospective` and `commercial` earn `CANVAS.md`. Intent is expected to move — a project that starts `personal` and becomes `prospective` updates this line and earns its canvas then.

**Market** is the counterpart fact and stays prose. It goes stale by nature; a stale answer that says when it was looked at beats a blank that reads as "no competitors."

---

## Surfaces

| Surface | Status |
|---|---|
| `<surface-name>` | `<Active | Future — <feature-kebab-slug>>` |

---

## Tech stack

| Surface | Technology | Status |
|---|---|---|
| `<surface-name>` | `<technology>` | `<Locked — <decision-slug> | TBD>` |

Status references a row in `DECISIONS.md` by kebab-case slug. When `<technology>` is TBD, the cell stays `TBD` and is filled when Architect or Analyst locks it.

### Model tiers

Octopus role briefs reference **capability tiers**, not vendor model versions. This is the one place the tiers map to concrete models for this project:

| Tier | Model | Used by |
|---|---|---|
| `deep-reasoning` | `<your strong reasoning model>` | Architect, Analyst, UX, oneshot; DEV / QA for hard cases |
| `fast-execution` | `<your fast implementation model>` | DEV, QA (default) |

---

## Active roles

| Role | Status | Notes |
|---|---|---|
| Architect | `<Active | Deferred>` | `<notes>` |
| Analyst | `<Active | Deferred>` | `<notes>` |
| UX | `<Active | Deferred>` | `<notes>` |
| DEV | `<Active | Deferred>` | `<notes>` |
| QA | `<Active | Deferred>` | `<notes>` |

---

## Project mode

Per-project answers to framework configuration questions. Recorded here so a fresh agent doesn't have to infer them from doc shapes.

| Choice | Value | Locked |
|---|---|---|
| Topology | `<in-repo | detached | no-repo>` | `<YYYY-MM-DD>` |
| Scale | `<multi-feature | single-feature | single-task | one-shot>` | `<YYYY-MM-DD>` |
| Release model | `<Epic-based | Feature-based>` | `<YYYY-MM-DD>` |
| Versioning | `<semver-tagged | date-keyed>` | `<YYYY-MM-DD>` |
| Multi-surface | `<No | Yes — surface-A, surface-B, ...>` | `<YYYY-MM-DD>` |
| Surface column in BACKLOG / DECISIONS | `<Omitted | Used>` | `<YYYY-MM-DD>` |
| Parity tracking | `<None | PARITY_LOG.md active>` | `<YYYY-MM-DD>` |

The choices link to framework directives:

- **Topology** — where Octopus's layers live and where output goes; drives the git/state rules in D1. `in-repo` (copied into the project repo — greenfield or brownfield), `detached` (Octopus in a personal folder; subject is a different team's repo — see `COLLAB_CONTEXT.md`), `no-repo` (no subject repo; output is documents/artifacts). See `WAY_OF_WORKING.md § Setting up a new project`.
- **Scale** — how much loop and which entry point: `multi-feature` (Kickoff → Plan), `single-feature` / `single-task` (Plan directly), `one-shot` (no loop). The two dials are independent — any Topology pairs with any Scale.
- **Release model** — Epic-based for projects with ≥2 Features per release; Feature-based for projects where one Feature = one release. See `DOCUMENT_TEMPLATES.md § Work hierarchy`.
- **Versioning** — semver-tagged for projects with explicit releases; date-keyed for deploy-continuous projects (consulting sites, content sites) that ship per-commit. See `DOCUMENT_TEMPLATES.md § ROADMAP`.
- **Multi-surface** — Yes when the project ships ≥2 independently-versioned surfaces (e.g. a web and a mobile client). Drives per-surface organization in ROADMAP and `Surface` column in BACKLOG / DECISIONS.
- **Parity tracking** — opt in for multi-surface projects with intentional or unintentional divergence between surfaces. See `PARITY_LOG_SKELETON.md`.

---

## Current focus

- **Release:** `<release-name>` — `<release-slug>` `<(Epic or Feature, per Project mode)>`
- **Active Task:** `<task-name>` (`<task-id>`) — `<status>`

For projects between releases: replace "Active Task" line with a one-line prose status (e.g. *"Between releases — next: open Plan for Feature `user-accounts`."*).

---

## File index

`PROJECT_GUIDE.md` is the **registry of all docs in use** in this project. The canonical set below is filtered to what this project has created; project-specific docs are listed alongside.

### Layer 1 — Octopus methodology (framework-owned)

| File | Purpose |
|---|---|
| `methodology/WAY_OF_WORKING.md` | Roles, loop, document maintenance, session protocol, layer model |
| `methodology/PO_INTERACTION_STYLE.md` | Communication contract |
| `methodology/DOCUMENT_TEMPLATES.md` | Canonical document set, work hierarchy, naming conventions |
| `methodology/DIRECTIVES.md` | The non-negotiable directives (D1–D14) |
| `FRAMEWORK_VERSION` | Pinned Octopus framework version |

### Layer 2 — Role briefs and templates (framework-owned)

| File | Read by |
|---|---|
| `roles/<ROLE>_BRIEF.md` | Per-role session start |
| `templates/` | Document and init prompt skeletons |

### Layer 3 — Project-owned

| File | Owner | Purpose |
|---|---|---|
| `PROJECT_GUIDE.md` | PO | This file — project registry and context card |
| `DECISIONS.md` | Analyst/Architect | Cross-cutting decisions |
| `ROADMAP.md` | Analyst | Release plan |
| `BACKLOG.md` | Analyst | Unassigned tiered work items |
| `OPS.md` | DEV | Deploy commands, infra config, procedures |
| `AGENTS.md` (or `AGENTS_<component>.md` per surface) | DEV | Live technical context |
| `<additional-project-docs>` | `<owner>` | `<purpose>` |

Project-specific docs (e.g. `PARITY_LOG.md`, `PRELAUNCH_CHECKLIST.md`, anything the project earns) are listed in the Layer 3 table above with their owner and purpose. They follow the same Layer 1 directives as canonical docs.

---

## Documents earned later

Canonical docs not yet created. Each will be added to the Layer 3 file index above when first written.

| File | When earned |
|---|---|
| `BUGS.md` | When bugs start arriving (i.e. when there are users) |
| `CHANGELOG.md` | When the first release ships |
| `CONTRIBUTING.md` | When more than one branch type exists or scopes need defining |
| `PRELAUNCH_CHECKLIST.md` | When launch is in sight |
| `CANVAS.md` | When `§ Identity` records Intent as `prospective` or `commercial` — including when Intent later changes to one of them |
| `<additional>` | `<condition>` |

The `CANVAS.md` row stays in this table for as long as Intent is `personal`, so a later change of Intent has something to fire against. Move it to the Layer 3 file index above when the canvas is written.

Pre-creating empty documents is a smell — they pretend structure that hasn't been earned. Wait until there's content to put in.

---

## Project-specific rules

Extensions or overrides on Layer 1 directives.

`<Project-specific rules go here, numbered. Examples:>`

1. `<rule>`
2. `<rule>`

*"None beyond Layer 1 directives at this stage."* if empty.

---

## Naming conventions

Project-specific values for the conventions defined in `DOCUMENT_TEMPLATES.md`.

**Task IDs:** `<convention, e.g., "Uppercase descriptive tag" or "sequential numbers">`

**Branch scopes:**

| Scope | Used for |
|---|---|
| `<scope>` | `<description>` |

**Bug IDs:** `B-xxx` (sequential, never reused). Tracked in `BUGS.md` when earned.

**Backlog IDs:** `I-xxx` (sequential, never reused). Tracked in `BACKLOG.md`.

`<Project-specific ID series, e.g. `P-xxx` for parity items in `PARITY_LOG.md`.>`

---

*Last updated: `<YYYY-MM-DD>` — `<one-line note on what changed>`.*
