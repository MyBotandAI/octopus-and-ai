# roles/

Layer 2 role briefs for Octopus framework consumers. **Framework defaults — paste-replace on every framework upgrade.** No project-specific edits in these files. Project-specific role notes (active vs. deferred, project-flavored guidance) live in `PROJECT_GUIDE.md` § Active roles.

---

## File index

| File | Role kind | Description |
|---|---|---|
| `ARCHITECT_BRIEF.md` | Specialist | Structural decisions |
| `ANALYST_BRIEF.md` | Specialist | Requirements and specs |
| `UX_BRIEF.md` | Specialist | Visual design |
| `DEV_BRIEF.md` | Specialist | Implementation |
| `QA_BRIEF.md` | Specialist | Acceptance review and bug triage |
| `ONESHOT_BRIEF.md` | Mode-role | Single-session creative work — no role loop |

The five specialist roles + oneshot = six agent roles. The five specialists run the Octopus role rotation (Analyst → UX → DEV → QA, with Architect as needed). Oneshot is invoked **instead of** the rotation, for projects or Tasks where the loop cost exceeds the loop value (marketing copy, landing pages, README rewrites, single-section content).

---

## Lifecycle

**At project setup:** copy the entire `roles/` directory from the framework into your project repo. No edits.

**On framework upgrade:** paste-replace the entire `roles/` directory. No diff-and-merge required because there are no project-specific edits to preserve.

**Project-specific role notes** live in `PROJECT_GUIDE.md` § Active roles — one short line per role in the Notes column (e.g., "Reviews each Task after DEV"; "Deferred until Feature `gui-platform`"). Richer project-specific narrative goes in `PROJECT_GUIDE.md` § Project-specific rules.

**Thinning roles per project:** if a project does not use a role (e.g., backend-only project skips UX), reflect that in `PROJECT_GUIDE.md` § Active roles by marking the role `Deferred` with a one-line reason. The brief file stays on disk — it's a framework default and may be needed later. Do not delete brief files.

**Role selection follows the Scale dial.** A project declares **Topology + Scale** in `PROJECT_GUIDE.md § Project mode` (see `methodology/WAY_OF_WORKING.md § Setting up a new project`):
- Scale ∈ {`multi-feature`, `single-feature`, `single-task`} → uses the five specialist roles per the standard loop (any Topology).
- Scale = `one-shot` → uses ONESHOT_BRIEF only; no role rotation, no Analyst/UX/DEV/QA invocations.

A single project may mix modes per-Task — most Tasks run through the specialist loop; a specific Task may declare `mode: one-shot` in its planning stub and route through ONESHOT_BRIEF instead.

---

## Customization escape hatch (rare)

If a project has genuinely unique role responsibilities that cannot be captured in `PROJECT_GUIDE.md` § Active roles, the supported pattern is **additive**: add a new role brief alongside the framework defaults (e.g., `roles/<NEW_ROLE>_BRIEF.md`) and reference it from `PROJECT_GUIDE.md` § File index and § Active roles. Framework-shipped briefs are never edited per project — modifying an existing brief's behavior is a fork situation, not a customization. Surface to PO before adding a new brief.
