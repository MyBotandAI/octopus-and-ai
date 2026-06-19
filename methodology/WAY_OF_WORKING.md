# Way of Working

**Owner:** PO
**Read by:** Every agent session — chat or coding-agent surface — at the start of every project, every session.
**Purpose:** Defines the roles, the workflow, the session protocol, and the framework-layer model that govern all PO work. The non-negotiable directives live in the companion `DIRECTIVES.md`. Project-agnostic — names capability tiers and surface kinds, not vendors. Per-project specifics live in each project's own documents.

---

## Framework layers

Octopus is structured in three layers. Every project that adopts it has all three; layers stay separate and are never merged.

**Layer 1 — Octopus core (`methodology/`):** `WAY_OF_WORKING.md`, `PO_INTERACTION_STYLE.md`, `DOCUMENT_TEMPLATES.md`, and `DIRECTIVES.md`. Project-agnostic. Defines how the team works, how roles communicate, what documents look like, and the non-negotiable directives. Updated only when the framework itself changes — never customised per project.

**Layer 2 — Octopus role briefs and templates (`roles/`, `templates/`):** Framework-shipped. Covers role briefs, procedural docs (`KICKOFF.md`, `PLAN.md`, `ONESHOT.md`), entry init prompts and per-role init skeletons (`INIT_*.md`, `INIT_*_SKELETON.md`), document seeds (`*_SKELETON.md` starters for `PROJECT_GUIDE`, `BACKLOG`, `ROADMAP`, `BUGS`, `CHANGELOG`, `CONTRIBUTING`, `AGENTS`, `OPS`, `PRELAUNCH_CHECKLIST`, `PARITY_LOG`, `CONTEXT_STUB`, `COLLAB_CONTEXT`, `TASK`), and both directory READMEs. Project-specific customization is additive: a new file alongside the framework defaults (e.g., `templates/TASK_PROJECT_SKELETON.md` for a project-specific spec shape, `roles/<NEW_ROLE>_BRIEF.md` for a new role), referenced from `PROJECT_GUIDE.md` § File index.

**Layer 3 — Project documents (project root):** `PROJECT_GUIDE.md`, `DECISIONS.md`, `ROADMAP.md`, `BACKLOG.md`, `BUGS.md`, technical context files (`AGENTS.md`, `web/README.md`), project-specific docs (`PARITY_LOG.md`, etc.), and per-TASK specs in `docs/`. Fully project-specific. Maintained by roles per the ownership matrix in this document.

### Bootstrapping a session

Each role brief contains a "Read at session start" list. That list is the session's reading order:

1. **Layer 1** — always first: `WAY_OF_WORKING.md`, `PO_INTERACTION_STYLE.md`, `DOCUMENT_TEMPLATES.md`, `DIRECTIVES.md`
2. **The project's `PROJECT_GUIDE.md`** — the Layer 3 entry point. Confirms the actual paths for all project documents.
3. **Remaining project docs** — as listed in the brief.

Role briefs and templates carry no project-specific placeholders — they reference canonical paths. Project-specific role notes live in `PROJECT_GUIDE.md` § Active roles.

### Layer 1 and Layer 2 are complementary, not redundant

`DOCUMENT_TEMPLATES.md` (Layer 1) defines document shapes; `DIRECTIVES.md` (Layer 1) defines the non-negotiables. The role briefs (Layer 2) define what a specific role does, what it reads, and what it produces. All are needed.

### Setting up a new project

Copy `methodology/`, `roles/`, and `templates/` into the project (or into a personal folder like `octopus-projects/<name>/` for the Detached topology below). Create `FRAMEWORK_VERSION` at the root. Then declare the project on **two orthogonal dials** in `PROJECT_GUIDE.md § Project mode` — they compose to produce the entry point, the loop, and the git rules.

**Dial 1 — Topology** (where Octopus's layers live; where output goes; drives the git/state rules in D1):

| Topology | Meaning |
|---|---|
| **In-repo** | Octopus layers copied into the project repo; output commits there. Covers greenfield *and* brownfield — new-vs-existing is a bootstrap detail, not a shape. |
| **Detached** | Octopus layers live in a separate personal folder; the *subject* of the work is a different repo the human may or may not have write access to. Octopus-side artifacts are disk saves only. |
| **No-repo** | No subject repo. State + output live in a folder; output is documents/artifacts. |

**Dial 2 — Scale** (how much loop; which entry point):

| Scale | Entry point | Loop |
|---|---|---|
| **Multi-feature** | **Kickoff** (`templates/INIT_ANALYST_KICKOFF.md`) → **Plan** per Feature | Full role loop; Epic/Feature/Task hierarchy. |
| **Single-feature** | **Plan** (`templates/INIT_ANALYST_PLAN.md`) | Role loop; one Feature = one release. |
| **Single-task** | a single Task spec | One DEV ⇄ QA loop. |
| **One-shot** | **Oneshot** (`templates/INIT_ONESHOT.md` + `templates/ONESHOT.md`) | **No loop** — agent makes design + copy + implementation calls in one session; PO reviews. A single creative deliverable. Avoids the Octopus loop where the loop cost exceeds the loop value. |

**Composition.** Entry point is a pure function of Scale; git/state rules are a pure function of Topology (D1 is Topology-conditional); the role loop applies for every Scale except One-shot. The two dials are independent — any Topology pairs with any Scale. Sensible default: **In-repo × the Scale matching the work size.** Show the common pairings as examples, don't enumerate all sixteen.

- **Multi-feature** projects run **Kickoff** first (produces `PROJECT_GUIDE.md`, `DECISIONS.md`, `ROADMAP.md`, `BACKLOG.md`, and the handoff init for Plan), then **Plan** per Feature.
- **Single-feature** / **Single-task** projects skip Kickoff — run **Plan** directly. Plan detects no `PROJECT_GUIDE.md` and runs a minimal Draft & Validate step inline before collecting context stubs.
- **Detached** topology: Plan's setup produces `COLLAB_CONTEXT.md` alongside the standard artifacts when PO confirms the subject is an external repo; Octopus state lives in a personal folder outside the subject repo.
- **One-shot** Scale: no Kickoff, no Plan, no per-Task spec files, no role loop — entry is `INIT_ONESHOT.md`.

After Kickoff (or after Plan's setup), reflect any project-specific role notes in `PROJECT_GUIDE.md` § Active roles. Inactive roles are marked `Deferred` with a one-line reason — brief files stay on disk.

`methodology/` and all of `roles/` + `templates/` are framework-controlled — re-sync wholesale on every upgrade. Project-specific rules and overrides go in `PROJECT_GUIDE.md` under "Project-specific rules." Project-specific Layer 2 additions are new files alongside framework defaults, referenced from `PROJECT_GUIDE.md` § File index.

---

## Directives

The non-negotiables live in **`methodology/DIRECTIVES.md`** (D1–D14), loaded as part of the Layer 1 canonical set at the start of every session. Referenced throughout the framework as `D1`, `D2`, … — when a session is told "see D1," it means that document. They are not selectively loaded: every session reads all directives. A project may *add* to a directive via an additive override file referenced from `PROJECT_GUIDE.md`; it never edits the framework file.

---

## Document maintenance

Sessions produce updates to the documents they own per the matrix below — not every session updates every document. The agent that knows the change owns the update. PO commits the updates; PO does not write them.

### Ownership matrix

| Document | Updated by | When |
|---|---|---|
| Project Context Card | PO + Analyst | At kickoff and at version boundaries |
| TASK spec (`docs/TASK_*.md`) | Analyst | At end of Analyst session — produces the file |
| Design spec | UX | At end of UX session |
| `DECISIONS.md` | Analyst, Architect, or any agent that surfaces a decision per D2 | When PO answers a decision-shaped OQ |
| `ROADMAP.md` | Analyst | After spec session (status changes) and after release |
| `BACKLOG.md` | Analyst | After spec session (new items, retiring items) |
| `BUGS.md` (open) | QA primary; DEV may create rows for bugs found incidentally during implementation | QA: when triaging a new bug. DEV: when running tests surfaces a bug unrelated to the current AC. |
| `BUGS.md` (fixed) | DEV | In the same commit as the fix |
| `CHANGELOG.md` | Analyst | At release-marking Task closure, together with the tag suggestion |
| `OPS.md` | DEV | When deploy commands or ops procedures change |
| `AGENTS.md` (technical context) | DEV | When architecture, gotchas, or key files change |
| `PRELAUNCH_CHECKLIST.md` | PO | PO maintains, others propose updates |
| `PARITY_LOG.md` (multi-surface projects only) | Analyst | When an audit surfaces a gap or when an item changes resolution state |
| One-shot deliverables (`docs/TASK_<id>/<output-file>`) | Single one-shot session, PO commits | Per one-shot session — see One-shot Scale below |

### PO's role in document maintenance

- **Review** the produced documents (quick scan, not a deep edit).
- **Commit and push.**
- **Confirm decisions** via Open Questions — the agent writes the row to `DECISIONS.md`. PO does not touch `DECISIONS.md` directly.
- **Periodic gardening** at version boundaries when documents drift.

PO is the committer, not the maintainer. If a session does not deliver the document updates alongside its work, PO sends it back.

---

## Roles

Seven roles total: PO (human, single owner of the project) + five specialist agent roles + one mode-role for non-loop work. The specialists are stable across projects; oneshot is invoked instead of the specialist rotation for One-shot-Scale Tasks (see § One-shot Scale below).

| Role | Kind | Brief |
|---|---|---|
| PO | Human — the human owner (you) | — (this document and `PO_INTERACTION_STYLE.md`) |
| Architect | Specialist agent | `roles/ARCHITECT_BRIEF.md` |
| Analyst | Specialist agent | `roles/ANALYST_BRIEF.md` |
| UX | Specialist agent | `roles/UX_BRIEF.md` |
| DEV | Specialist agent | `roles/DEV_BRIEF.md` |
| QA | Specialist agent | `roles/QA_BRIEF.md` |
| Oneshot | Mode-role agent | `roles/ONESHOT_BRIEF.md` (single-session creative work, no role loop) |

### Surface defaults

The **surface** is where a session runs: a **coding-agent surface** (a tool with repo + shell access) or a **chat surface** (conversational, visual paste).

| Role | Default surface | Switch to chat surface when |
|---|---|---|
| Architect | Coding-agent | Methodology evolution or strategic framing with no codebase context |
| Analyst | Coding-agent | Heavy visual reference required, or stakeholder-style discussion benefits from conversational format |
| UX | Coding-agent | Session is primarily rapid visual iteration with PO present |
| DEV | Coding-agent | Never |
| QA | Coding-agent | Never |

Surface is a deliberate per-session call by PO. The role's *function* is invariant; the surface follows the work.

### Model tiers

Roles declare a **capability tier**, not a vendor model version. Two tiers:

- **deep-reasoning** — strong reasoning model for structural, spec, and creative work.
- **fast-execution** — fast implementation model for code and review work.

The concrete tier → model mapping for a project lives in one place: `PROJECT_GUIDE.md § Tech stack`. Role briefs reference the tier by name; never hardcode a model version.

### PO — Product Owner / the human owner (you)

The connecting point. Decides what gets built, when, and at what quality bar. Coordinates the specialist sessions, holds the product vision, performs all git operations visible to remote, and accepts or rejects work at every gate. The PO is the only role that crosses between sessions.

PO is human (you). The other five roles are agent sessions.

### Architect

Structural decisions. Invoked at the start of a project, at major structural shifts, and at cross-cutting technical decision points. Most features do not go through Architect — they go directly to Analyst.

- **Surface:** Coding-agent by default.
- **Model:** deep-reasoning tier with extended thinking where available.
- **Inputs:** PO's framing of the structural question. Existing docs.
- **Outputs:** Architecture brief; writes `DECISIONS.md` rows after PO confirms via OQ.
- **Handoff:** Produces a Analyst init prompt referencing the brief and any decisions written.
- **What good looks like:** A brief that names the decision in one sentence, presents 2–3 options, states tradeoffs honestly, ends with a clear "this is what I'd do."

### Analyst — Specification (requirements analyst)

Requirements and specs. Defines what a feature must do, for whom, with which acceptance criteria and edge cases. Does not propose technical implementation. Does not produce visual designs.

Analyst is the most frequently invoked role.

- **Surface:** Coding-agent by default.
- **Model:** deep-reasoning tier.
- **Inputs:** PO's feature idea or backlog item. Existing specs from related features. Architecture briefs when relevant.
- **Outputs:** TASK spec; writes `DECISIONS.md` rows after PO confirms via OQ; updates `ROADMAP.md`.
- **Handoff:** Produces the init prompt for the next role. If UX is needed, produces a UX init prompt; Analyst reopens after UX delivers and produces the DEV init prompt incorporating both specs.
- **What good looks like:** Every AC can be answered yes/no. Every Edge Case names a specific weird condition. Open Questions flagged honestly. No technical implementation choices appear in the text.

### UX — UX/Design Specialist

Visual design and design system fidelity. Produces design specs that DEV implements against. Reviews shipped work against design intent. Owns design tokens and cross-platform parity story when more than one surface exists.

UX is invoked when a feature has a visual surface that needs design decisions.

- **Surface:** Coding-agent by default.
- **Two routes (PO-selected):** in-session UX (apply an existing design system) vs. an external **design surface** for net-new visual-identity decisions (typography, color, brand, layout, new screens). The design surface reads from disk but does not write to the repo — it generates options PO chooses from and emits code/assets DEV integrates. UX surfaces the route choice to PO when identity decisions are in play (`roles/UX_BRIEF.md` § Choosing the UX route).
- **Model:** deep-reasoning tier.
- **Inputs:** Analyst's TASK spec. Screenshots. Design tokens.
- **Outputs:** Design spec. Reviews of shipped work.
- **Handoff:** Returns to Analyst when the design is delivered. UX does not produce a DEV init prompt directly.
- **What good looks like:** Every state is named. Tokens referenced by name. Dark mode covered. Interaction details specified. Accessibility minimums stated.

### DEV — Developer

Implementation. Writes code. Reads existing code. Runs builds and tests. Commits per logical change on a task branch. Self-reviews against acceptance criteria.

Automated tests are part of DEV's deliverable. "DEV is done" includes "tests pass." DEV writes the tests, runs them, commits them.

DEV does not write specs and does not lock decisions. When ambiguity surfaces mid-implementation, DEV pauses and asks one focused question rather than guessing — or surfaces it as a spec issue that warrants reopening Analyst.

- **Surface:** Coding-agent.
- **Model:** fast-execution tier default. deep-reasoning tier only for genuinely hard architectural moves.
- **Inputs:** TASK spec from Analyst. Design spec from UX when relevant. Existing codebase. Project's `AGENTS.md`.
- **Outputs:** Code on a task branch with per-change commits, including automated tests. Updates to `AGENTS.md` and `OPS.md` when warranted. `BUGS.md` Fixed-row updates in the same commit as fixes. **May create `BUGS.md` Open rows for bugs found incidentally.** **May write `DECISIONS.md` rows per D2 for decision-shaped OQs PO answers during implementation.** Honest self-review against AC at the end.
- **Handoff:** Produces the QA init prompt referencing the branch, the spec(s), the design (when present), and what was implemented.
- **What good looks like:** AC walked one-by-one with a clear pass/flag/fail. Tests cover the AC. Surfaced ambiguities honestly.

### QA — Acceptance Review and Bug Triage

QA is invoked at the end of each TASK to verify shipped work meets its acceptance criteria, and reactively when bugs surface from PO's organic testing or from early users.

QA does **not** perform exhaustive exploratory testing. Automated tests are DEV's responsibility, not QA's.

- **Surface:** Coding-agent.
- **Model:** fast-execution tier default. deep-reasoning tier only when hunting a subtle bug class.
- **Inputs:** TASK spec with AC. The branch under review. Bug reports.
- **Outputs:** Acceptance review report. New `B-xxx` entries in `BUGS.md`. Triage of incoming bugs.
- **Handoff:** On approval, work returns to PO for merge. On Fail or Flags requiring fixes, the review document itself is the handoff back to DEV.
- **What good looks like:** Honest verdicts. Visual AC flagged when the surface cannot render or inspect the UI. Bugs triaged with severity, repro steps, suspected component. **Runtime bugs surfaced during testing:** diagnose root cause and log in `qa_review.md`; do not apply code changes (D3).

---

## Work hierarchy

Three levels — **Epic, Feature, Task**. Their interpretation as Releases depends on the project's **Project mode** (declared in `PROJECT_GUIDE.md § Project mode`):

| Project mode | Release maps to | Feature maps to |
|---|---|---|
| Epic-based (big project) | Epic (≥2 Features per Release) | Feature |
| Feature-based (small project) | Feature (one Feature = one Release) | (no separate level) |

The planning unit and the shipping unit are the same. Detail in `DOCUMENT_TEMPLATES.md § Work hierarchy`.

- **Epic** — strategic grouping. Opt-in outer level for ≥2 Features clustering under a shared thrust. Sized in months. Single-Feature "Epics" are not allowed.
- **Feature** — coherent piece of functionality and the default outer frame for Feature-based projects. Sized in weeks. Splits into Tasks at Analyst scoping.
- **Task** — the unit of delivery. One spec, 3–10 user stories, AC, edge cases. One branch. One DEV ⇄ QA loop.

Tasks can be standalone — a bug fix or small chore does not need to belong to a Feature.

---

## The loop

The loop is a graph. PO routes work through it. The common path is shown below; detours are normal, not exceptional. The entry point is a function of the project's **Scale** dial (see § Setting up a new project).

### Common path

```
[Kickoff phase — once per project, Multi-feature Scale only]
  PO → INIT_ANALYST_KICKOFF → Analyst Kickoff
    Phase 1 Discovery → Phase 2 Alignment (pitch locked)
    Phase 3: Architect needed?
      yes → init_architect_kickoff → Architect → init_analyst_kickoff_resume → Analyst Kickoff reopen
      no  → continue
    Phase 4 Draft & Validate — complete PROJECT_GUIDE draft inline; PO validates with one MCQ
    Phase 5 Features & Tasks elicitation (Epics → Features → Task names; no stubs)
    Phase 6 Artifact production → PROJECT_GUIDE, DECISIONS, ROADMAP, BACKLOG, init_analyst_plan for Feature 1

[Plan phase — once per Feature; also the entry point for Single-feature / Single-task Scale]
  PO → INIT_ANALYST_PLAN → Analyst Plan
    (small-project mode if no PROJECT_GUIDE: Draft & Validate first)
    Walk every Task in the Feature; collect 6-field context stubs
    Warn if Feature has >5 Tasks (soft limit)
    Write context.md per Task; write init_analyst for the first Task

[Spec phase — once per Task]
  Analyst → (needs UX? no)  → DEV init prompt → DEV
  Analyst → (needs UX? yes) → UX init prompt → UX → Analyst reopen → DEV init prompt → DEV

[Build phase — once per Task]
  DEV (persistent) ⇄ QA (persistent) → PO accepts → PO merges
         ↑                  ↑
         └── PO testing ────┘

[Closure phase — once per Task]
  PO syncs local default branch → Analyst reopens
  Analyst closure: ROADMAP / BACKLOG / archive
  Next-step routing
  PO closes sessions
```

Each role produces the init prompt for the next role in the common path. PO performs the mechanical action of opening the next session — until programmatic orchestration replaces the manual step.

### Detours (normal)

- **DEV → Analyst reopen.** DEV finds a spec ambiguity that's not an implementation choice. Analyst session reopens, PO ↔ Analyst resolves, spec updates, DEV resumes.
- **DEV → UX reopen.** Same pattern, design side.
- **PO testing → QA → DEV.** PO's organic testing finds bugs. QA logs them in `BUGS.md` (or DEV inline, if the bug surfaced during DEV's implementation), DEV fixes, QA verifies.
- **QA → DEV → QA.** Standard inner loop. 1–3 round trips before approval is normal.
- **Analyst → Architect reopen.** When Analyst surfaces a structural question mid-spec, Analyst produces a short **Architect reopen brief** (`docs/init_architect_reopen_<task-id>.md`) naming the question + relevant Phase 1/2 context + any new constraints surfaced since the prior Architect session. Architect returns either a brief addition to `ARCHITECTURE_BRIEF.md` or a new `DECISIONS.md` row per D2, plus a short reopen brief back to Analyst.

### When to skip steps

- **Skip Kickoff** for Single-feature / Single-task Scale. Enter directly via `INIT_ANALYST_PLAN.md` — Plan runs Draft & Validate inline in its small-project mode.
- **Skip the Phase 3 Architect handoff** when no structural question is open.
- **Skip Architect** at Task level for any Task that fits within existing structural decisions.
- **Skip Analyst** only for bug fixes where the spec is the bug report itself.
- **Skip DEV** for doc-only Tasks with no code surface (methodology-as-product projects, README / spec / doc edits): Analyst produces the doc changes as session output; QA or PO live-review gates.
- **Skip QA** only for documentation changes PO is reviewing in real time.
- **Skip the whole loop** for One-shot Scale (or per-Task `mode: one-shot` opt-out within an Octopus project) — a single creative deliverable (marketing copy, a landing page, a README rewrite, or content-fill of an already-built page-set). The agent makes design + copy + implementation calls in a single session; PO reviews the output. A multi-page presentational *build* is **not** a one-shot — it runs through the loop as a single batched Task (see § Multi-page presentational builds). See `DOCUMENT_TEMPLATES.md § One-shot variant` and `templates/ONESHOT.md`.

### Task closure (post-merge)

After PO merges the Task's branch, Analyst reopens briefly for **Task closure** — the bookkeeping that connects a shipped Task back to the project's planning artifacts.

**Analyst's first action at closure:** sync local state (checkout default branch + pull), then delete the merged local task branch (`git branch -d <task-branch>` — fails safely if it isn't fully merged).

Halt and surface to PO if the working tree is dirty.

Analyst's closure responsibilities (after sync):

1. **`ROADMAP.md`** — Task status → Done with ship date; promote to Past section when appropriate.
2. **`BACKLOG.md`** — retire items the Task resolved; update notes; surface any new items.
3. **Task folder** — move `docs/TASK_<id>/` to `docs/archive/`.
4. **Archive-path sweep** — grep live docs for the old path and bump references.
5. **Promote earned files in `PROJECT_GUIDE.md` § File index** — scan for files that now exist but are still under "Documents earned later."
6. **Surface post-merge checklist** — read `docs/archive/TASK_<id>/qa_review.md` § Post-merge checklist when present and surface verbatim to PO.
7. **Release boundary (when warranted)** — when this Task closure marks a release boundary, write the new release entry to `CHANGELOG.md` (summary of shipped Task(s) since the previous tag; cross-refs `DECISIONS.md` slugs and `B-xxx` IDs per D12; no rationale) and surface a one-line tag suggestion. PO commits the CHANGELOG addition and executes the tag.
8. **Next-step routing** — examine the Feature this Task belonged to and either produce the next Task's init_analyst or surface "open Plan for Feature N+1."

#### Spec-less chore variant

For chore Tasks where Analyst was never invoked, PO produces the Analyst closure init directly per `DOCUMENT_TEMPLATES.md § Spec-less chore variant`.

### Multi-page presentational builds

A multi-page **presentational** build — a vitrine / brochure site where every page shares **one locked design system** — runs through the normal loop as a **single batched Task**, not as a one-shot and not as one Task per page. One Analyst scope covers the whole page-set; one UX design pass covers *every* page's layout and IA; one DEV build implements all pages on one branch with **placeholder copy**; one QA gate; one closure.

- **One batched Task, not N.** Scoping the whole page-set as one Task avoids re-running the loop per page over the same locked system (loop cost exceeds loop value) while still giving the build a real design gate — the gate a one-shot build leaves open, because a locked design system locks tokens and components, **not** page-level layouts/IA.
- **Size the design pass by the design-route choice.** A page that is genuine composition of existing patterns takes the in-session design route; a page whose layout/IA is net-new takes the external design surface. Trivial pages don't pay a heavy pass; net-new layouts get a real one (`roles/UX_BRIEF.md § Choosing the UX route`).
- **Build-then-content is the sequencing.** This batched Task builds the *structure* with placeholder copy; a later **content-fill** Task drops in the real copy — content edits, not redesign. Content-fill is a one-shot (copy is one-shot's native lane) or a spec-less content Task.
- **Precondition — a locked design system.** The build *applies* a system (tokens, type scale, component primitives, a reference page that sets the quality bar); it does not invent one. Net-new visual identity is a real design call — lock it first (full loop or design surface), then run the build Task.
- **Build-brief shape.** The build Task's brief carries: per-page scope inputs (route, purpose, key sections); hard constraints — **no new design tokens**, **reuse components** by composition, **locked routes / nav**; a **reuses list** (design-token source, component directory, the reference page, any content/collection schemas, design-intent docs); an **"elevate the existing page"** framing for flat/stub pages; **placeholder-copy discipline** (realistic in rhythm and length but obviously swappable, structured so content-fill can fill it mechanically); and a **build-passes-clean gate** (not done until the build command runs clean).
- **Hybrid rule.** Within one release, routing is per-Task: presentational pages take this batched build path; any route carrying a spec or a visible API surface (contact form, auth, payments, SEO infra, deploy) keeps its own full Analyst → UX → DEV → QA Task. If such a route would otherwise break navigation, add only a minimal placeholder page so the nav resolves — do not build its logic in the presentational Task.

The build-brief shape and the multi-page scoping note also live in `DOCUMENT_TEMPLATES.md § Multi-page build scoping`.

### One-shot Scale

One-shot-Scale Tasks (Scale = One-shot in `PROJECT_GUIDE.md § Project mode`) run **outside** the role-rotation loop. No Analyst → UX → DEV → QA. PO provides a brief; one session produces the deliverable.

- **Entry point:** `templates/INIT_ONESHOT.md` + `templates/ONESHOT.md`. No Kickoff, no Plan, no per-role init prompts.
- **Scale compresses the role loop, not git.** One-shot removes `spec.md`, the UX/DEV/QA rotation, and `qa_review.md` — nothing more. **Git and closure follow Topology (D1), not Scale:** an **in-repo** one-shot works on a task branch, commits per change, pushes at pause, and gets a ROADMAP/closure beat like any other Task; only a **no-repo / standalone** one-shot uses the "PO commits, closure straight to PO, disk-save only" shape (D1 is Topology-conditional — see `DIRECTIVES.md`).
- **Decision discipline retained.** One-shot sessions may write `DECISIONS.md` rows per D2 when PO confirms a cross-cutting choice surfaced during the session. The session is outside the loop for role rotation but inside Octopus's decision-locking discipline.
- **D12 applies.** Cross-cutting facts surfaced during a one-shot anchor in `DECISIONS.md` like any other. Don't duplicate the deliverable's content into other docs.
- **Single review gate.** Output presented to PO with explicit "Choices I made (worth flagging)" and "Decisions worth locking" sections. No QA review document.
- **Task folder for traceability:** minimal contents (`init.md` brief, the output, optional PO review notes). No `spec.md`, no `init_<role>.md` — this reflects the compressed role loop and stays regardless of Topology.

Fits: marketing copy, landing pages, README rewrites, single-section content, brand voice work, and content-fill of an already-built page-set (the content phase of a multi-page build — see § Multi-page presentational builds). Does not fit anything that needs a spec, a visible API surface, or net-new page layout/IA design — those are normal Octopus Tasks.

### Loop principles

- **Unit of decision is the Task, not the Feature or Epic.** PO does not approve a multi-task plan in advance.
- **Handoffs are documents, not chat history.** Handoff artifacts must be self-contained.
- **Every role change produces a named handoff.** Inside Kickoff and across the loop.
- **Sessions stay open through their need.** A session that has delivered its output enters a paused state and waits. PO closes after the Task is accepted (D7).
- **Agents do not auto-advance through `ROADMAP.md`.** A role that has produced its output and the next role's init prompt pauses. Advancing to the next Task is PO's call.

---

## Session protocol

### PO's standard session-open prompt

The init file (`init_<role>.md`) is **self-sufficient** by design — frontmatter declares `role:` (triggers canonical-set auto-load: Layer 1 quartet + role brief + project core docs), `read_first_task:` lists task-unique paths, body carries the goal, deliverable, and how-to-run. PO does not need to re-list what the init file already covers.

**Standard session-open prompt by surface:**

- **Coding-agent surface (most common):** one line pointing at the file path.
  > `Read docs/TASK_<id>/init_<role>.md and proceed.`

  Agent reads the file, follows canonical-set auto-load, then `read_first_task`, then proceeds per the body.

- **Chat surface (rare — visual-generation sub-tool, occasional Analyst conversation):** paste the full content of the init file. Layer 1 docs live in the chat's project knowledge / system prompt; do not re-paste them per session.

**Optional belt-and-braces checkpoint:** for less-rigorous chat surfaces or when PO wants verification, append *"Before doing anything else, confirm you've loaded the Layer 1 quartet + your role brief + the project core docs."* Agent responds with a one-line confirmation of what was read, then proceeds. Not needed in steady-state coding-agent sessions.

**Antipatterns to avoid:**
- Re-listing what the init file already says ("Read X and Y and Z, then do this...") — means the init file isn't doing its job; fix the init file.
- Skipping the init file and hand-rolling the briefing — agent loses canonical-set context, spec context, durable record.
- Asking the agent to "read methodology first" — redundant with canonical-set auto-load.

### At session start

**Read everything first — produce no output until reading is complete.** When an init prompt is provided, read the full canonical set and every `read_first_task` entry in one uninterrupted pass before writing anything to PO. No mid-read check-ins. No permission-asks. No narration of intent. The init file is the permission; reading is the first act of the session. The pre-flight block in every init skeleton lists the files in order.

1. **Read the canonical set.** Layer 1 quartet (`WAY_OF_WORKING.md`, `PO_INTERACTION_STYLE.md`, `DOCUMENT_TEMPLATES.md`, `DIRECTIVES.md`) → role brief (`roles/<ROLE>_BRIEF.md`) → project core docs per the brief's "Read at session start."
2. **Read all `read_first_task` entries.** Every path listed in the init prompt, in order.
3. **Then engage PO.** Three cases:
   - **Init prompt provided** (most common) — proceed directly to role work. Do not confirm reads; do not summarise what you read. Just work.
   - **Reopen** (PO returns to a paused session) — ask: *"What changed since I paused?"* Re-read anything that changed.
   - **Fresh session, no init prompt** (rare) — ask: *"What's the goal today, and which colleague's output am I picking up from?"*
4. **Proceed in role.** Stay in lane (D3). Surface crossings, do not handle them silently.

### Mid-session

- **Surface Open Questions explicitly.** Do not guess; do not silently proceed past ambiguity.
- **Present Open Questions as a menu, not prose.** When the interactive elicitation tool is available, use it. Otherwise fall back to the markdown menu format.
- **Adapt to PO redirects.** New context, new screenshots, scope shifts. Do not insist on the path before the redirect (D8).
- **Produce intermediate artifacts as you go.**

### At pause (output delivered, awaiting next PO action)

- Produce the artifacts in full, ready for PO to commit.
- **Produce the next role's init prompt** per your role's Handoff section. Detour cases replace the init prompt with the document that triggered the detour.
- Surface anything that crossed a boundary.
- **Do not declare the session "complete."** PO closes sessions, not agents (D7).
- **Do not summarize the conversation.** PO read it.

### At reopen (PO returns with new input)

- Re-read the documents that have changed since pause.
- Treat reopen as a mini-session-start.

### At close (PO declares session no longer needed)

- Final document updates per the ownership matrix.
- No farewell summary.

---

## What this document does NOT cover

- **Project-specific structure.** Tech stack, file layout, branch naming scopes, deploy commands — these live in each project's own documents.
- **The directives.** The non-negotiables (D1–D14) live in `DIRECTIVES.md`.
- **Document content.** The shape of TASK specs, the format of `DECISIONS.md`, the conventions for `B-xxx` and `I-xxx` IDs — see `DOCUMENT_TEMPLATES.md`.
- **Communication style.** How sessions talk to PO, what tone to use — see `PO_INTERACTION_STYLE.md`.

These four Layer 1 documents are read together.

### Out-of-scope review work — PO's gate at merge time

Octopus's role lineup intentionally does not include separate Code Review, Security Review, or Performance Review roles. For solo founder operation these are **PO's gate when merging a review request** — PO reviews the change before merging, surfaces any code-quality / security / performance concerns inline, and routes back to DEV if needed.

Projects that earn scale to need dedicated review roles can add them via the customization escape hatch in `roles/README.md` (additive new brief). Until then, the absence is deliberate, not a gap.

---

*Layer 1 — methodology baseline. Project-agnostic. Updated only when the way of working itself changes.*
