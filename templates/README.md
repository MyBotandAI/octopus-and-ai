# templates/

Layer 2 templates and procedural docs for Octopus framework consumers. **Framework-shipped — paste-replace wholesale on every framework upgrade.** No per-project edits to these files. Project-specific customization is additive: add a new file alongside (e.g., `TASK_PROJECT_SKELETON.md`) and reference it from `PROJECT_GUIDE.md` § File index.

---

## File index

| File | Category | Description |
|---|---|---|
| `KICKOFF.md` | Procedural doc | Kickoff procedural doc — Discovery, Alignment, Architect handoff, Structured questions, Artifact production |
| `PLAN.md` | Procedural doc | Plan procedural doc — per-Feature context collection; small-project entry path |
| `INIT_ANALYST_KICKOFF.md` | Entry init prompt | Entry init prompt for a fresh Analyst session running Kickoff |
| `INIT_ANALYST_PLAN.md` | Entry init prompt | Entry init prompt for a fresh Analyst session running Plan |
| `INIT_ARCHITECT_SKELETON.md` | Init prompt skeleton | Init prompt skeleton for Architect sessions |
| `INIT_ANALYST_SKELETON.md` | Init prompt skeleton | Init prompt skeleton for Analyst sessions |
| `INIT_UX_SKELETON.md` | Init prompt skeleton | Init prompt skeleton for UX sessions |
| `INIT_DEV_SKELETON.md` | Init prompt skeleton | Init prompt skeleton for DEV sessions |
| `INIT_QA_SKELETON.md` | Init prompt skeleton | Init prompt skeleton for QA sessions |
| `TASK_SKELETON.md` | Document seed | Canonical TASK spec — copy at TASK creation, fill, transform into Layer 3 |
| `PROJECT_GUIDE_SKELETON.md` | Document seed | Project Context Card — copy once at Kickoff Phase 5 |
| `DECISIONS_SKELETON.md` | Document seed | Cross-cutting decisions log — canonical index + body shape per D10 |
| `BUGS_SKELETON.md` | Document seed | Bug log starter |
| `BACKLOG_SKELETON.md` | Document seed | Backlog starter — five-tier structure |
| `ROADMAP_SKELETON.md` | Document seed | Roadmap starter — Status, Future, Past |
| `CHANGELOG_SKELETON.md` | Document seed | Changelog starter |
| `OPS_SKELETON.md` | Document seed | Ops starter |
| `CONTRIBUTING_SKELETON.md` | Document seed | Contributing guide starter |
| `AGENTS_SKELETON.md` | Document seed | Technical context starter |
| `CANVAS_SKELETON.md` | Document seed (earned) | Business-hypothesis canvas — nine boxes, one state each; earned when Identity Intent is `prospective` or `commercial` |
| `CONTEXT_STUB_SKELETON.md` | Document seed | Per-Task context stub — 6-field format, produced by Plan |
| `COLLAB_CONTEXT_SKELETON.md` | Document seed (Detached only) | Collaboration framing for Detached-topology projects |

---

## How each category is used

**Procedural docs and Init prompts** are read by agents at session start (procedural docs frame a multi-phase flow; init prompts brief a fresh role). Their internal `<PLACEHOLDER>` fields are fill-at-use parameters — agents fill them when producing a concrete artifact (e.g., a Task-specific `init_dev.md` in `docs/TASK_<id>/`). They are not project customization points.

**Document seeds** are copied at the point of need (project setup for `PROJECT_GUIDE_SKELETON.md`, `BACKLOG_SKELETON.md`, etc.; Task creation for `TASK_SKELETON.md`; on-demand for `CONTEXT_STUB_SKELETON.md`). The copy lands in Layer 3 (`PROJECT_GUIDE.md`, `BACKLOG.md`, `docs/TASK_<id>/spec.md`, …) and evolves with project state from there. The seed in `templates/` stays untouched and gets paste-replaced like the rest of Layer 2 on framework upgrade — re-pasting has no effect on Layer 3 because agents never re-read the seed after the first copy.

---

## Placeholder convention

All fill-in fields use `<PLACEHOLDER>` syntax (e.g., `<project-name>`, `<task-id>`, `<YYYY-MM-DD>`).
