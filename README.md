# Octopus

**A methodology framework for orchestrating specialist AI agent sessions across solo-founder projects.**

Octopus turns "one human + AI coding agents" into a small, disciplined team. You — the Product Owner — coordinate a rotation of specialist agent sessions (Analyst, Architect, UX, DEV, QA, plus a one-shot mode) through a defined loop, with **durable documents instead of chat history** as the source of truth. It is model-agnostic in shape; Claude is the reference implementation.

> Part of the **mybotandai** house — *My Octopus and AI*: you and your octopus of agents, working together.

## What it is (and isn't)

Octopus is **prose and process**, not a tool you install. There is no runtime to run and no dependency to add — you copy a set of Markdown documents into your project and follow them. The value is in the discipline: clear roles, explicit handoffs, one decision at a time, and a paper trail that survives between sessions.

## The three-layer model

Octopus is structured in three layers that stay separate and are never merged:

- **Layer 1 — core (`methodology/`)** — *project-agnostic.* How the team works, how roles communicate, what documents look like, and the non-negotiable directives. Four files: `WAY_OF_WORKING.md`, `PO_INTERACTION_STYLE.md`, `DOCUMENT_TEMPLATES.md`, `DIRECTIVES.md`. Re-synced wholesale on upgrade; never customized per project.
- **Layer 2 — roles & templates (`roles/`, `templates/`)** — *framework-shipped.* Six role briefs plus a library of document seeds (`*_SKELETON.md`) and init-prompt templates. Customization is **additive** — a new file alongside the defaults, never an edit to a shipped one.
- **Layer 3 — your project (your repo)** — *fully yours.* The documents you produce by following the framework: `PROJECT_GUIDE.md`, `DECISIONS.md`, `ROADMAP.md`, per-task specs, and so on. Octopus ships the **seeds**; the filled-in instances live in your project.

An optional **Claude layer (`skills/`)** packages the six roles as Claude Skills. It is opt-in and vendor-isolated — copy it if you use Claude, ignore it otherwise. Nothing in Layers 1–2 depends on it.

## How to adopt

1. **Copy the framework into your project:** `methodology/`, `roles/`, `templates/` (and `skills/` if you use Claude).
2. **Pin the version:** copy `FRAMEWORK_VERSION` to your repo root so you know which framework cut you are tracking.
3. **Declare your project mode:** Octopus composes on two dials — **Topology** (in-repo / detached / no-repo) × **Scale** (multi-feature / single-feature / single-task / one-shot). Pick the pairing that matches your work; the sensible default is *in-repo × the Scale matching the work size*.
4. **Pick your entry point** (a function of Scale):
   - **Multi-feature** → start with **Kickoff** (`templates/INIT_ANALYST_KICKOFF.md`).
   - **Single-feature / single-task** → start with **Plan** (`templates/INIT_ANALYST_PLAN.md`).
   - **One-shot** → a single creative session (`templates/INIT_ONESHOT.md`).
5. **Run the loop:** Analyst specs → (UX if visual) → DEV builds → QA reviews → you merge. Handoffs are documents, decisions are locked in `DECISIONS.md`, and the documents — not the conversation — are the durable state.

Start with [`methodology/WAY_OF_WORKING.md`](methodology/WAY_OF_WORKING.md) — it explains the roles, the loop, and the session protocol end to end.

## License

Apache-2.0 — see [`LICENSE`](LICENSE) and [`NOTICE`](NOTICE). The license grants the framework freely (attribution + patent grant) but conveys **no rights in the names or marks**: "Octopus" and "mybotandai" are trademarks of mybotandai. You are free to copy, adapt, and build on the methodology; you may not pass your product off as Octopus.

---

*Octopus is published by **mybotandai** — "My Octopus and AI."*
