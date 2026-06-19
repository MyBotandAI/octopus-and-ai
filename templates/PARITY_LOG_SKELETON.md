# `<project-name>` — Parity Log

**Owner:** Analyst `<+ PO if project convention>`
**Updated:** `<YYYY-MM-DD>`

Tracks gaps surfaced by parity audits between surfaces. **Opt-in for multi-surface projects** (declared in `PROJECT_GUIDE.md § Project mode` as `Parity tracking: PARITY_LOG.md active`). Single-surface projects do not need this file.

This is a **traceability ledger** — rows point at where each item resolves rather than carrying the resolution itself. Resolution detail lives in `DECISIONS.md` (locked divergences), `BACKLOG.md` (backports), TASK specs (absorbed work), or commit / review-request refs (shipped).

---

## Purpose

Surfaces visual / behavioural / structural gaps between surfaces of the same product (e.g. Web ↔ Mobile, Surface A ↔ Surface B). Each item starts as a surfaced gap and resolves to one of six states:

| State | Meaning | Where the resolution lives |
|---|---|---|
| **Mirror** | Fix the lagging surface to match the leading one. | Remediation TASK; row moves to **Resolved** when it ships. |
| **Locked divergence** | PO accepts the difference between surfaces. | New row in `DECISIONS.md`; this entry references the slug. |
| **Backport** | The lagging surface has the better behaviour; promote it to the other. | New row in `BACKLOG.md` (`I-xxx`); this entry references the ID. |
| **Defer** | Revisit at a later milestone. | Notes the milestone trigger in the entry. |
| **Absorbed into TASK** | A forward-looking TASK now owns the resolution work. | TASK spec; row moves to **Resolved** when the absorbing TASK ships. |
| **Resolved** | Fixed in an audit session OR shipped via a remediation / absorbing TASK. | Commit, review-request, or branch reference in the entry. |

Single-surface behaviours (no other-surface equivalent) and surface-first decisions already locked in `DECISIONS.md` are not tracked here — they stay in audit reports as historical context.

---

## Open

Items pending decision. Flat list — do not split into category subsections until ≥2 open items share a category.

| ID | Source | Surfaces | Summary |
|---|---|---|---|
| `<P-xxx>` | `<TASK_X spec | audit session | DEV implementation>` | `<surface-A vs surface-B>` | `<≤200-char gap description>` |

---

## Absorbed into TASK

Folded into a forward-looking TASK that owns their resolution. Moves to **Resolved** when the absorbing TASK ships.

| ID | Source | Summary | Absorbing TASK |
|---|---|---|---|
| `<P-xxx>` | `<source>` | `<≤200-char gap description>` | `<TASK_<id> (release-slug)>` |

---

## Deferred

Re-evaluated at a later milestone. Trigger named.

| ID | Source | Summary | Re-evaluate when |
|---|---|---|---|
| `<P-xxx>` | `<source>` | `<≤200-char gap description>` | `<concrete milestone trigger>` |

---

## Locked as divergence

PO has accepted the gap. Each row anchors a `DECISIONS.md` slug carrying the rationale (per D12 inter-doc boundaries).

| ID | Source | Summary | `DECISIONS.md` slug |
|---|---|---|---|
| `<P-xxx>` | `<source>` | `<≤200-char gap description>` | [`<kebab-slug>`](DECISIONS.md#kebab-slug) |

---

## Backported

The behaviour of the lagging surface is preferred; pulled into the other surface's `BACKLOG.md`.

| ID | Source | Summary | `BACKLOG.md` entry |
|---|---|---|---|
| `<P-xxx>` | `<source>` | `<≤200-char gap description>` | `<I-xxx (tier, when)>` |

---

## Resolved

Shipped. Commit / review-request / branch reference in the Resolution cell.

| ID | Source | Resolution |
|---|---|---|
| `<P-xxx>` | `<source>` | `<≤200-char outcome + commit-SHA or review-request-#>` |

---

*Last updated `<YYYY-MM-DD>`. P-xxx IDs sequential, never reused, even after resolution.*
