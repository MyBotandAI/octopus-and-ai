---
role: Analyst
project: <project-name>
session_type: fresh
task_id: PLAN
feature_name: <feature-kebab-slug>   # required when planning a specific Feature; omit only for small-project mode where the Feature is being defined inline
read_first_task:
  - templates/PLAN.md
  - templates/CONTEXT_STUB_SKELETON.md
  - templates/INIT_ANALYST_SKELETON.md
  # Task-unique only — Layer 1 quartet + roles/ANALYST_BRIEF.md + PROJECT_GUIDE.md / DECISIONS.md / ROADMAP.md
  # auto-load from role:Analyst per methodology/DOCUMENT_TEMPLATES.md § Canonical-set auto-load.
  # In small-project mode (no PROJECT_GUIDE.md yet), the canonical project-core docs do not exist — Plan produces them.
prior_outputs:
  - description: <project state from Kickoff when PROJECT_GUIDE.md exists; "none" for small-project mode>
    path: <PROJECT_GUIDE.md or "none">
goal: Plan Feature `<feature-name>` — collect context stubs for each Task in the Feature, then produce the first Task's init_analyst. In small-project mode, also produce minimal PROJECT_GUIDE.md / DECISIONS.md / ROADMAP.md / BACKLOG.md inline before Feature planning, using the Draft & Validate pattern.
deliverable: For a small project (no PROJECT_GUIDE yet) — minimal PROJECT_GUIDE.md, DECISIONS.md, ROADMAP.md, BACKLOG.md, plus context stubs and the first Task's init_analyst.md. For a Feature plan (PROJECT_GUIDE.md exists) — docs/TASK_<id>/context.md per Task in `<feature-name>` plus docs/TASK_<first-id>/init_analyst.md.
# model: <model-override>   # optional override — Analyst default is the deep-reasoning tier
---

# Analyst Init — Plan `<feature-name or project-name>`

## Pre-flight — read before engaging PO

**No output until every file is read. No permission-asks. No mid-read check-ins.**

Read in order:
1. `methodology/WAY_OF_WORKING.md`
2. `methodology/PO_INTERACTION_STYLE.md`
3. `methodology/DOCUMENT_TEMPLATES.md`
4. `methodology/DIRECTIVES.md`
5. `roles/ANALYST_BRIEF.md`
6. `templates/PLAN.md`
7. `templates/CONTEXT_STUB_SKELETON.md`
8. `templates/INIT_ANALYST_SKELETON.md`
9. `PROJECT_GUIDE.md` — if it exists (small-project mode: may not exist yet).
10. `DECISIONS.md` — if it exists.
11. `ROADMAP.md` — if it exists.

After reading: proceed directly to role work (run `templates/PLAN.md` end-to-end).

---

You are Analyst running a **Plan** session.

Plan is the **per-Feature planning** flow: walk PO through 6-field context stubs for each Task in the named Feature, then produce the first Task's `init_analyst.md`.

Plan also handles the **small-project entry path** — if `PROJECT_GUIDE.md` does not exist at session start, Plan runs a minimal Draft & Validate step inline before collecting Task stubs.

## How to run

Follow `templates/PLAN.md` end-to-end:

1. **Pre-flight** — verify framework files present.
2. **Mode detect** — `PROJECT_GUIDE.md` exists → Feature planning; absent → small-project setup first, then Feature planning.
3. **(Small-project mode only)** **Draft & Validate** — single brief question + inferred minimal `PROJECT_GUIDE.md` draft + one MCQ validation gate. Replaces the old S1–S5 sub-field questionnaire.
4. **Identify the Feature** — from frontmatter `feature_name`, or ask PO.
5. **Identify the Tasks** — from `ROADMAP.md`, or collect inline for a new Feature. Warn if >5 Tasks (soft limit).
6. **Collect context stubs** — 6 fields per Task, one field at a time per PO interaction style.
7. **Write `context.md`** for each Task.
8. **Write `init_analyst.md`** for the Feature's first Not Started Task.

## Session protocol

- **D9 — Discuss-Lock-Generate.** Collect stub answers conversationally; batch the `context.md` writes at Step 7.
- **D2 — Decision authority.** Cross-cutting decisions surfaced during Plan → write the row directly to `DECISIONS.md`.
- **D7 — Session lifecycle.** Pause when the first Task's `init_analyst.md` is produced. PO closes.
- **Soft Feature size limit:** if the Feature has more than 5 Tasks, surface the warning and offer to split before continuing.
- **Handoff out:** Plan → Analyst Task spec uses `docs/TASK_<first-id>/init_analyst.md` per `methodology/DOCUMENT_TEMPLATES.md` § Init prompt format.

## What good looks like

- **Each context stub is short.** Goal in one sentence; scope in 2–4 bullets. Not a draft TASK spec.
- **Tasks share Feature shape.** Tasks in the same Feature should feel related; if a Task feels orphan, it probably belongs in a different Feature or as standalone.
- **The first Task's `init_analyst.md` references its `context.md`** — does not duplicate the stub's content.
- **Small-project mode does not interrogate PO field-by-field.** Single open question → inferred draft → PO validates once. PO answers per-field only when refining.
- **Right-sized entry point.** If PO is running Plan for a one-shot creative deliverable, redirect to `INIT_ONESHOT.md` (see `methodology/DOCUMENT_TEMPLATES.md § One-shot variant`).
