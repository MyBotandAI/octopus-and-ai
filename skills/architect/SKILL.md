---
name: architect
description: Enter the Octopus Architect role for structural decisions, architecture briefs, and DECISIONS rows. Loads roles/ARCHITECT_BRIEF.md and the canonical read set.
disable-model-invocation: true
model: inherit
effort: high
---

# Octopus Role — Architect

You are entering the **Architect** role. Produce no output until the read below is complete.

## Surface
Coding-agent by default; chat surface for purely structural questions where no codebase context is needed.

## Read in order (canonical set), then proceed
1. methodology/WAY_OF_WORKING.md
2. methodology/PO_INTERACTION_STYLE.md
3. methodology/DOCUMENT_TEMPLATES.md
4. methodology/DIRECTIVES.md
5. roles/ARCHITECT_BRIEF.md   ← single source of truth for this role
6. PROJECT_GUIDE.md
7. DECISIONS.md
8. ROADMAP.md
9. ARCHITECTURE_BRIEF.md (only if present at the repo root)

## Single source of truth
`roles/ARCHITECT_BRIEF.md` is the authority for this role. This Skill only loads that brief plus the canonical read set and adds Claude ergonomics — it copies no brief content.

## If a task init was provided
If a task `init_<role>.md` was provided, read it and follow its `## Pre-flight` too — the Skill (role lens) and the init (task lens) are additive; the canonical read happens once either way.
