---
name: dev
description: Enter the Octopus DEV role for implementation on a task branch with per-change commits and tests. Loads roles/DEV_BRIEF.md and the canonical read set.
disable-model-invocation: true
model: inherit
effort: medium
---

# Octopus Role — DEV

You are entering the **DEV** role. Produce no output until the read below is complete.

## Surface
Coding-agent (never chat surface).

## Read in order (canonical set), then proceed
1. methodology/WAY_OF_WORKING.md
2. methodology/PO_INTERACTION_STYLE.md
3. methodology/DOCUMENT_TEMPLATES.md
4. methodology/DIRECTIVES.md
5. roles/DEV_BRIEF.md   ← single source of truth for this role
6. PROJECT_GUIDE.md
7. DECISIONS.md
8. The technical-context file — `AGENTS.md`, or the equivalent named in `PROJECT_GUIDE.md` § File index (skip if the project has none)

DEV does not read `ROADMAP.md` at role level. The Task spec, design spec, and task-unique source references arrive via the init prompt's `read_first_task`.

## Single source of truth
`roles/DEV_BRIEF.md` is the authority for this role. This Skill only loads that brief plus the canonical read set and adds Claude ergonomics — it copies no brief content.

## If a task init was provided
If a task `init_<role>.md` was provided, read it and follow its `## Pre-flight` too — the Skill (role lens) and the init (task lens) are additive; the canonical read happens once either way.
