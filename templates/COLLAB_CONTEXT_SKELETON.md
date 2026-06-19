# Collaboration Context — `<project-name>`

**Owner:** PO
**Updated:** `<YYYY-MM-DD>`

This document is present only for **Detached-topology** projects — declared in `PROJECT_GUIDE.md § Project mode` as `Topology: detached`, and triggered by the `Collaboration: see COLLAB_CONTEXT.md` line in `PROJECT_GUIDE.md § Identity`.

Sessions read this file at start to understand the collaboration framing before doing anything else. Plan produces it during setup when PO confirms the Detached topology (`templates/PLAN.md § Detached setup`).

---

## Subject

- **Project:** `<one-line description of what the external team is building or working on>`
- **Repository:** `<path or URL to the subject repo, or "TBD" / "none shared yet">`
- **My access:** `<none | read-only | read-write | other — describe>`

---

## External team

- **Methodology:** `<their framework / internal doctrine / unspecified — one line>`
- **My role:** `<advisory | reviewer | consultant | collaborator — one line>`
- **Collaboration mode:** `<sync chat in review requests | standalone audits | async deliverables | periodic check-ins — describe the cadence>`
- **Comms:** `<chat channel / email / shared workspace — name the channel>`

---

## What Octopus is doing here

`<One paragraph framing why Octopus is running on PO's side: tracking advisory workflow, producing handback artifacts, keeping a decision log for PO's reasoning, etc. Make the role of Octopus explicit — it is not authoring the primary deliverable of the subject project.>`

---

## Where my work lives

`octopus-projects/<project-name>/` — disk only, not a git repo.

**D1 in the Detached topology:** D1's git operations (push, review request, merge, tag, branch policy) apply only to the subject repo *if* PO has write access there. PO's own Octopus artifacts persist as disk saves only. Agents do not write to the subject repository under any condition — even when PO has write access, that's a separate explicit PO action.

---

## Inputs from the external team

Drop files received from the external team into `inbox/`. The canonical location for any reference doc, setup guide, requirement note, screenshot, or other input the team hands over.

Current contents:

- `<inbox/file-name.md>` — `<one-line description of what it contains and when it was received>`

*(Update this list when new inputs arrive — PO maintains; Analyst sessions may also add an entry when an input is referenced during a session.)*

---

## Outputs handed back

Track what's been delivered to the external team:

| Date | Artifact | Sent to | Notes |
|---|---|---|---|
| `<YYYY-MM-DD>` | `<docs/TASK_<id>/spec.md>` | `<channel/recipient>` | `<one-line summary>` |

*(Append as deliverables go out. PO maintains.)*

---

## Cross-references

- **`PROJECT_GUIDE.md § Identity`** — `Collaboration: see COLLAB_CONTEXT.md` line is the trigger that announces this doc's existence to fresh sessions.
- **`PROJECT_GUIDE.md § Project mode`** — `Topology: detached` records the topology choice.
- **`PROJECT_GUIDE.md § Active roles`** — Detached defaults are Analyst active, others Deferred unless engagement evolves.

---

*Layer 3 — per-project. Maintained by PO; updated when collab framing changes (new comms channel, scope shift, access change, methodology update on their side).*
