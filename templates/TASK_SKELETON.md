# `<project-name>` — `<task-name>`
## TASK `<task-id>`: `<short-description>`

**Status:** `<Draft | Specced | In Progress | Shipped>`
**Parent feature:** `<feature-kebab-name, or "standalone">`
**Target release:** `<version>`
**Depends on:** `<other-task-IDs, or "none">`
**Last updated:** `<YYYY-MM-DD>`

---

## Context

`<One to three paragraphs. What this Task delivers, why now, what's bundled, what carry-over fixes are included.>`

---

## Entry points / scope (if applicable)

`<When and how the user encounters this functionality. Where it appears in the existing surface. What triggers it.>`

---

## Functional spec sections

`<The body of the spec. Organized by sub-feature or by screen. Tables for fields and behaviors when scannable. Prose for flows and rationale.>`

---

## User Stories

**US-01 — `<short-title>`**
As a `<user>`, I want to `<action>`, so that `<benefit>`.

---

## Acceptance Criteria

**AC-01** — `<testable-assertion>`.

**AC-02** — `<testable-assertion>`. *[Verify after merge — `<one-line reason: what PO checks, what live state lags>`]*

Tag an AC inline with *[Verify after merge — …]* when the live verification target is a post-merge state (domain resolution, CDN rebuild, third-party deploy hook). Untagged ACs are verifiable on the task branch. See `methodology/DOCUMENT_TEMPLATES.md` § canonical TASK spec format §6.

---

## Edge Cases

**EC-01** — `<condition>`: `<expected-behavior>`.

---

## Open Questions

**OQ-01** — `<question>`. `<Notes on who can answer, whether it blocks DEV>`.

---

## Backlog Items Added

`<I-XX IDs and short descriptions of any backlog items surfaced during this spec session, or "(none)".>`

---

## DECISIONS.md updates required

`<Decision rows written to DECISIONS.md during this session. Listed here so PO has them in one place when reviewing. Or "(none)".>`
