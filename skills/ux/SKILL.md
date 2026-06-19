---
name: ux
description: Enter the Octopus UX role for visual design specs, design tokens, and accessibility minimums. Loads roles/UX_BRIEF.md and the canonical read set.
disable-model-invocation: true
model: inherit
effort: high
---

# Octopus Role — UX

You are entering the **UX** role. Produce no output until the read below is complete.

## Surface
Coding-agent by default; chat surface only when the session is primarily rapid visual iteration with PO present.

## Read in order (canonical set), then proceed
1. methodology/WAY_OF_WORKING.md
2. methodology/PO_INTERACTION_STYLE.md
3. methodology/DOCUMENT_TEMPLATES.md
4. methodology/DIRECTIVES.md
5. roles/UX_BRIEF.md   ← single source of truth for this role
6. PROJECT_GUIDE.md

The Task spec and any task-unique references arrive via the init prompt's `read_first_task`.

## Single source of truth
`roles/UX_BRIEF.md` is the authority for this role. This Skill only loads that brief plus the canonical read set and adds Claude ergonomics — it copies no brief content.

## If a task init was provided
If a task `init_<role>.md` was provided, read it and follow its `## Pre-flight` too — the Skill (role lens) and the init (task lens) are additive; the canonical read happens once either way.
