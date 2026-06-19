---
name: oneshot
description: Enter the Octopus oneshot mode-role for single-session creative work — no role loop. Loads roles/ONESHOT_BRIEF.md and the canonical read set.
disable-model-invocation: true
model: inherit
effort: high
---

# Octopus Role — oneshot

You are entering the **oneshot** mode-role — single-session creative work, no Analyst → UX → DEV → QA loop. Produce no output until the read below is complete.

## Surface
Coding-agent (single-session creative work); chat surface acceptable when the deliverable is conversational copy iteration with PO present.

## Read in order (canonical set), then proceed
1. methodology/WAY_OF_WORKING.md
2. methodology/DOCUMENT_TEMPLATES.md
3. methodology/DIRECTIVES.md
4. roles/ONESHOT_BRIEF.md   ← single source of truth for this role
5. templates/ONESHOT.md
6. PROJECT_GUIDE.md (only if it exists — oneshot may run inside or outside an Octopus project)
7. Any reuse paths named in the brief (existing logo, design tokens, brand voice notes, prior copy)

`methodology/PO_INTERACTION_STYLE.md` is deliberately not in the oneshot read set — PO is not available for incremental questions during a one-shot session.

## Single source of truth
`roles/ONESHOT_BRIEF.md` is the authority for this role. This Skill only loads that brief plus the canonical read set and adds Claude ergonomics — it copies no brief content.

## If you were opened via a oneshot brief
If you were opened via an Octopus oneshot brief, read it and follow `templates/INIT_ONESHOT.md`'s flow — the Skill (role lens) and the brief (task lens) are additive. oneshot runs no role loop and hands off to no other role; the deliverable goes back to PO.
