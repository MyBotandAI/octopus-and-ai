# Directives

**Owner:** PO
**Read by:** Every agent session — every project, every session. Always-loaded; part of the Layer 1 canonical set.
**Purpose:** The non-negotiables that govern all work. Numbered for shorthand reference — when a session is told "see D1," it means this document. Project-agnostic. A project may *add* to a directive (an additive override file referenced from `PROJECT_GUIDE.md`); it never edits this file.

---

**D1 — Git authority and branch policy.**
**The integration/default branch is PO-only.** Direct commits to the default branch, merges of review requests, release tags, and deploys are PO's sole authority. Agents work on task branches and may commit AND push on those branches; agents never touch the default branch. ("Default branch" is whatever the project's `CONTRIBUTING.md` names — `main`, `master`, `trunk`; "review request" is the project's mechanism — a pull request, merge request, etc.)

- **DEV implementing a Task** — creates a task branch per the project's `CONTRIBUTING.md` naming. Commits per logical change with Conventional Commits messages. **Pushes at session pause.** Stays on the branch until PO closes the session. Does not open the review request.
- **QA reviewing** — commits its review document on the same branch as the work being reviewed. May commit `BUGS.md` updates. **Pushes at session pause.** **When the review is 100% Pass, QA opens the review request**, writing its body from the AC review + spec summary. If anything is less than 100% Pass, QA does NOT open it — the review document is the handoff back to DEV.
- **Analyst / UX / Architect producing documents** — produces the updated document(s) as session output. Does not commit. Hands files to PO; PO commits.
- **Analyst at Task closure** — first action is to sync local state with the just-merged Task (checkout default branch + pull) and delete the merged local task branch (`git branch -d`, which fails safely if unmerged). **Halts and surfaces to PO if the working tree is dirty.** After sync, runs the closure responsibilities and **may suggest a release tag** with a one-line rationale; PO executes any tagging.
- **PO** — sole authority on the default branch: direct commits, merges of review requests that QA opens, release tags, deploys. Reviews and approves every review request before merging.

**D1 is Topology-conditional** (per the project's `PROJECT_GUIDE.md § Project mode` Topology dial — see `WAY_OF_WORKING.md § Setting up a new project`):

- **In-repo** — Octopus layers and output live in the project repo. Standard D1 above applies in full.
- **Detached** — Octopus layers live in a separate personal folder; the *subject* of the work is a different repo the human may or may not have write access to. D1's git operations apply only to the subject repo *if* PO has write access there. PO's own Octopus artifacts persist as disk saves only — no branches, no commits, no review requests on PO's side. Agents do not write to the subject repository under any condition unless explicitly authorized.
- **No-repo** — no subject repo at all; state and output live in a folder. No git rules apply (optional local versioning only).

**D2 — Decision authority.**
Cross-cutting decisions (affecting more than the current Task) are surfaced by agents as Open Questions per D9. PO answers; the agent writes the decision row directly to `DECISIONS.md` — slug, value, rationale, date. PO does not write to `DECISIONS.md` directly. Decisions are immutable once written; to change a decision, supersede it with a new row referencing the old one and move the old row to `## Superseded Decisions` per `DOCUMENT_TEMPLATES.md § DECISIONS.md`.

**Who writes the row.** The **surfacing agent** writes the row, regardless of role. When DEV surfaces a decision-shaped OQ during implementation and PO answers, DEV writes the `DECISIONS.md` row inline — not via a Analyst reopen. When UX surfaces a structural design decision and PO answers, UX writes. The ownership matrix names Analyst / Architect as *typical* writers; any agent that surfaces and locks per D2 writes the row. This removes the mid-implementation Analyst reopen overhead for decision-shaped OQs surfaced by non-Analyst agents.

**D3 — Role boundaries.**
Each role stays in its lane. DEV does not write specs. Analyst does not make implementation choices. UX does not lock cross-cutting decisions. Architect does not implement. QA does not specify. When work crosses a boundary, the session surfaces the crossing and waits for PO to decide which role handles it.

**D4 — Source of truth is the documents.**
When session memory and a document conflict, the document wins. When two documents conflict, the session surfaces the conflict to PO and does not pick. The documents are the durable state; agent sessions are not.

**D5 — MVP over perfection.**
Flag quality issues; do not block on them unless correctness-critical. PO decides what gets gold-plated. Polish is a deliberate decision, not a default.

**D6 — One unit of work per session.**
A session works on one feature, one bug, one decision, one document — not five in parallel. Switch sessions to switch focus.

**D7 — Session lifecycle is PO's call.**
Sessions are opened, paused, resumed, and closed by PO — not by the agent. An agent that has produced its current output enters an implicit paused state and waits. It does not declare itself "done," "closed," or "ready to terminate." Closing a session prematurely breaks the loop's flexibility — most TASKs require an agent to be reopened at least once.

**D8 — Structure without rigidity.**
The loop is a graph, not a sequence. PO redirects mid-session, brings new context, surfaces screenshots, opens follow-up Open Questions. Agents preserve this flexibility — they do not push back on redirects or insist on the path they had before context updated.

**D9 — Discuss-Lock-Generate.**
When a session has Open Questions that materially affect the document it will produce, surface and resolve them with PO **before** generating the document. Sequence: **Discuss** OQs (as a menu) → wait for PO to lock → confirm understanding → **Generate** the document with locked decisions baked in.

**D10 — Tables are pointers, not narrative.**

Markdown table cells stay one physical line in the source and read as one line in any viewer. Longer context (rationale, history, multi-step semantics) lives in a body section the cell points to via slug or anchor.

**Cell allowances:**
- **Default:** ≤80-char trailing parenthetical allowed (e.g. `Done — 2026-05-14 (superseded by DOMAIN_REWORK)`). Anything longer promotes to a body section.
- **`DECISIONS.md` Summary cell:** ≤150 chars (one-sentence authoritative statement).
- **Traceability ledgers** (e.g. `PARITY_LOG.md` — docs whose primary purpose is linking IDs to resolution events): ≤200 chars — the prose IS the trace record. Strict body-section split doubles doc size for limited gain.

The body section may live **in the same document** — the table becomes an index; the cell's slug anchors a body section further down (`DECISIONS.md` is the textbook case). Or **in another document** — spec, design, `BACKLOG.md` entry, technical context file — appropriate when the rationale belongs to that other artifact's domain.

Multi-sentence rationale in a table cell breaks scannability and rendering, and duplicates content that lives better in a body. Cells stay short; bodies carry the depth.

**D11 — Documents are current state, not history.**
Live-state documents describe the project as it is *now*. Footers, Status sections, intro paragraphs, and any freeform block stay current-state — they do not accumulate per-update narrative. The footer stamp is one line: `*Last updated YYYY-MM-DD.*` — no per-cut gist, no "Prior 2026-MM-DD…" tail. When a session updates a live doc, it **rewrites** the affected sections and **overwrites** the footer stamp. History lives in version control and `CHANGELOG.md`. Live-state docs in scope: `PROJECT_GUIDE.md`, `DECISIONS.md`, `ROADMAP.md`, `BACKLOG.md`, `BUGS.md`, `OPS.md`, `AGENTS.md`, any project-specific log (e.g. `PARITY_LOG.md`). Exempt by definition: `CHANGELOG.md` and `docs/archive/**`.

**D12 — Inter-doc boundaries: one fact, one canonical home.**

Every technical fact has one canonical home, decided by which lens the fact represents:

| Lens | Doc | What lives here |
|---|---|---|
| **WHY** | `DECISIONS.md` | Cross-cutting choices + rationale. Kebab-case slug + ≤150-char summary + locked date. Body section for longer rationale. |
| **NOW** | `AGENTS.md` / `AGENTS_<component>.md` | Live architecture + rules + gotchas. One-line rules referencing `DECISIONS.md` slugs for the why. |
| **WHEN** | `CHANGELOG.md` | Per-release manifest. Cross-references `DECISIONS.md` slugs, `B-xxx` IDs, commits. |
| **HOW (per-Task)** | `docs/TASK_<id>/spec.md` (or archived) | Screen-level design calls, AC, EC, OQ. Cross-cutting calls promote to `DECISIONS.md`. |

**Cross-document references replace duplication.** Same fact in two places = D12 violation. Agents pick the doc by *which lens* the content represents, not by *which feels right*.

**Practical routing rules for agents:**
- A choice is locked → write `DECISIONS.md` row first; if it constrains future code, add a one-line gotcha in `AGENTS.md` with anchored reference.
- A live rule with no choice involved ("this is how the system works") → `AGENTS.md` only.
- A release shipped → `CHANGELOG.md` entry citing the slugs and bugs touched; no rationale (that's in `DECISIONS.md`).
- A screen-level design call → Task spec only; never promote to `DECISIONS.md` unless cross-cutting.

`OPS.md` is the canonical home for **ops config and procedures**; other docs reference here rather than duplicating. Project-specific docs (see `DOCUMENT_TEMPLATES.md § Project-specific documents`) follow the same rule — pick the lens, anchor by slug, don't duplicate.

**Migration:** Existing redundancy is not forced-cleaned. New content follows D12. Old content gets cleaned opportunistically when a Task touches the affected area.

**D13 — Stop-and-reopen on unexpected state.**

When executing a checklist or runbook — any procedure with expected results — if any step's expected result does not match what you see, **stop executing and reopen this session before continuing**.

Surface the divergence to PO. Do not barrel through unexpected state. Do not invent a recovery path that wasn't specified. Do not retry on the assumption the runbook is right and reality is wrong.

The runbook is authoritative for the *expected* path; reality is authoritative for what *is*. When they disagree, PO arbitrates. This is the difference between "I followed step 5, got an unexpected error, surfaced it" (correct) and "I followed step 5, got an unexpected error, then improvised steps 6-8 to work around it" (D13 violation).

Applies to: `OPS.md` runbooks, `PRELAUNCH_CHECKLIST.md` items, dev-machine setup, any procedure carrying *expected: …* annotations.

**D14 — BACKLOG estimation gate.**

Items entering `BACKLOG.md` default to the `## Needs estimation` section. **Promotion to any tier (1–4) requires a DEV effort estimate recorded on the row.**

Exception: items with obviously known effort — a parity backport, a single-file cleanup, a known one-liner — may bypass with a `(self-estimated)` tag in Notes.

Without an estimate, agents do not pick a tier. They leave the item in `## Needs estimation` for DEV to estimate at the next backlog review.

**Why:** intuition-based tier assignment produces Tier 4 dumping grounds and Tier 2 items with no effort signal. The gate keeps tier slots honest.

`When` (time-to-ship) is a separate column on backlog rows: `pre-release` (default) / `post-1.0` / `post-traction`. Tier remains pure impact × effort.

---

*Layer 1 — methodology baseline. Project-agnostic. Updated only when the directives themselves change.*
