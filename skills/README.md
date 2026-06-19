# skills/

The **optional Claude layer** for Octopus — the first *vendor* layer over the provider-neutral core. Six role-Skills wrap (not copy) the canonical `roles/<ROLE>_BRIEF.md`, adding Claude-only ergonomics: a `/role` command entry and an `effort` hint. Each `SKILL.md` is a thin pointer — it enumerates the role's canonical read order, declares the brief the single source of truth, and copies no brief content.

**One-way dependency:** Skills read briefs; **nothing in Layer 1/2 references the Skills layer.** Removing `skills/` changes nothing in the core loop. Claude-specifics live only here; the briefs they load stay vendor-agnostic.

---

## File index

| Command | Role | `effort` | Brief (SSOT) |
|---|---|---|---|
| `/architect` | Architect — structural decisions | `high` | `roles/ARCHITECT_BRIEF.md` |
| `/analyst` | Analyst — requirements and specs | `high` | `roles/ANALYST_BRIEF.md` |
| `/ux` | UX — visual design | `high` | `roles/UX_BRIEF.md` |
| `/dev` | DEV — implementation | `medium` | `roles/DEV_BRIEF.md` |
| `/qa` | QA — acceptance review and bug triage | `medium` | `roles/QA_BRIEF.md` |
| `/oneshot` | oneshot — single-session creative work | `high` | `roles/ONESHOT_BRIEF.md` |

`effort` expresses the role's capability tier version-free (`high` = deep-reasoning, `medium` = fast-execution). Every Skill also sets `model: inherit` — no pinned model, so the Claude layer carries no version-staleness. A consumer who wants a role to force a specific model sets `model:` locally (additive, off the published default).

---

## Install

Copy `skills/*` into the consumer's `.claude/skills/` directory. The **directory name is the invocation command** — `skills/architect/` ⇒ `/architect`.

**Opt-in = don't copy.** A consumer that copies nothing gets zero Skills and runs the loop unchanged via init prompts. The core never depends on this layer.

Invocation is **explicit `/role` only** (`disable-model-invocation: true`) — no chat phrase auto-loads a Skill. The role-Skill (role lens — identity + canonical read + Claude hints) and a task `init_<role>.md` (task lens — goal, deliverable, `read_first_task`) are orthogonal and additive; the canonical read is idempotent, so it happens once either way.

---

## Lifecycle / upgrade

Paste-replace the entire `skills/` directory on every framework upgrade and bump `FRAMEWORK_VERSION` — the same lifecycle as Layer 1/2 (`layer2-single-lifecycle`, `layer1-distribution`). No per-project edits to shipped Skills. Consumer customization is **additive only**: a local `model:` pin, or a new skill folder alongside the framework defaults.

---

## Dependency note

The Skills require `roles/` and `methodology/` present at the repo root — they Read those briefs by repo-root-relative path. Installing `skills/` without the framework layers leaves the Skills pointing at missing files: the Read fails visibly and the session reports the missing file (it does not silently proceed without the brief). Keep `skills/` and `roles/` in lockstep via the paste-replace lifecycle.

---

## Command-name fallback

The six commands are the bare lowercase role names. If a consumer already has a skill or command of the same name, the consumer renames their own or namespaces it — **Octopus does not pre-namespace.** (The six names were verified at build to not collide with any Claude Code built-in command.)
