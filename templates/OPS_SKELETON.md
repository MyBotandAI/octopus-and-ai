# `<project-name>` — Operations

**Owner:** DEV
**Updated:** `<YYYY-MM-DD>`

Operational truth for deploys, infrastructure, secrets, and procedures that need to be repeatable. The **canonical home** for ops config (per D12 inter-doc boundaries) — other docs (`AGENTS.md`, `PROJECT_GUIDE.md`) reference here rather than duplicating.

---

## Global rules

**Stop-and-reopen on unexpected state (per `methodology/DIRECTIVES.md` § D13).** If any step's expected result does not match what you see — stop executing and reopen this DEV session before continuing. Surface the divergence to PO; do not barrel through.

**Only PO runs deploys (per D1 in `methodology/DIRECTIVES.md`).** Agents prepare commands and verification steps; PO executes.

---

## Deploy commands

Exact commands a fresh operator can copy and run. Group by surface or by deploy target.

```bash
# <Surface or target>
<exact command>            # <one-line purpose>
```

**`<post-deploy verification note when relevant — e.g. "verify in incognito after hosting deploys to bypass the CDN cache" or "watch <provider> deploy list for Published status">`**

---

## Infrastructure

Resource names, regions, service tiers — the facts you'd need to re-create the system or audit it. Where a step is a **one-time dashboard action** that can't be scripted (CDN site creation, hosting-provider console registration, email-provider SMTP key generation, domain registrar config), use the **UI-only callout**:

> *(No runbook — `<operation>` is a one-time dashboard action. Resulting state captured below / in §`<reference>`.)*

The callout legitimizes UI-only setup work and points the reader at the resulting state.

### `<infrastructure-area>`

`<Reference data — service names, URLs, regions, ports, account IDs, build settings, DNS records, etc.>`

`<Where a one-time UI action set this state, include the UI-only callout describing what was done and pointing here.>`

---

## Secrets

**Names and locations only — never values.** Per `methodology/DIRECTIVES.md` directive on secrets handling.

| Secret | Where it lives | Used by |
|---|---|---|
| `<NAME>` | `<env var | secret manager path | dashboard location>` | `<consumer>` |

`<Procedural notes for adding / rotating secrets, where to download credentials from, what file path they land in locally. Reference but do not include the values.>`

---

## Procedures

Repeatable operational procedures that aren't deploy commands — new-machine setup, tester portal updates, beta access flow, post-release tasks, anything with concrete steps.

### `<procedure-name>`

`<Numbered steps. Each step has a single concrete action. Mark expected results so the stop-and-reopen rule can fire on mismatch.>`

1. `<step>` — *expected: `<observable outcome>`*
2. `<step>` — *expected: `<observable outcome>`*

`<For procedures where some steps require role coordination (e.g. QA prepares, PO deploys), name the role on each step.>`

---

## File stewardship

For project files that mix human-editable content with auto-generated or rendering logic, declare what is and is not safe to touch:

### `<filename>` — what NOT to touch

- `<constant-name or section>` — `<reason / consequence of touching>`

---

*Last updated `<YYYY-MM-DD>`.*
