---
name: qa
description: Enter the Octopus QA role for acceptance review against AC and bug triage. Loads roles/QA_BRIEF.md and the canonical read set.
disable-model-invocation: true
model: inherit
effort: medium
---

# Octopus Role — QA

You are entering the **QA** role. Produce no output until the read below is complete.

## Surface
Coding-agent (never chat surface).

## Read in order (canonical set), then proceed
1. methodology/WAY_OF_WORKING.md
2. methodology/PO_INTERACTION_STYLE.md
3. methodology/DOCUMENT_TEMPLATES.md
4. methodology/DIRECTIVES.md
5. roles/QA_BRIEF.md   ← single source of truth for this role
6. PROJECT_GUIDE.md
7. BUGS.md (only if present at the repo root)

QA does not read `DECISIONS.md` or `ROADMAP.md` at role level. The Task spec, design spec, DEV self-review, and task-unique references arrive via the init prompt's `read_first_task`.

## Single source of truth
`roles/QA_BRIEF.md` is the authority for this role. This Skill only loads that brief plus the canonical read set and adds Claude ergonomics — it copies no brief content.

## If a task init was provided
If a task `init_<role>.md` was provided, read it and follow its `## Pre-flight` too — the Skill (role lens) and the init (task lens) are additive; the canonical read happens once either way.
