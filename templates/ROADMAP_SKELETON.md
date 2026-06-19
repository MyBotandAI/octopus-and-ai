# `<project-name>` — Roadmap

**Owner:** Analyst
**Updated:** `<YYYY-MM-DD>`

---

## How this skeleton adapts to Project mode

Read `PROJECT_GUIDE.md § Project mode` to know which variant of this file your project uses:

- **Release model = Epic-based** → each Release in this file is an Epic containing Features; the active Feature(s) under Current Release expand to per-Task drill-down.
- **Release model = Feature-based** → each Release in this file is a Feature directly; the active Feature drills down to Tasks.
- **Versioning = semver-tagged** → Past Releases use version-keyed rows (`<component>-vX.Y.Z`).
- **Versioning = date-keyed** → Past Releases use date-keyed rows (no version numbers).
- **Multi-surface = Yes** → Current / Future / Past each split into one block per surface (`### Surface A`, `### Surface B`, etc.).
- **Multi-surface = No** → single block per section, no surface split.

The structure below assumes Feature-based, semver-tagged, single-surface defaults. Bracketed alternatives flag what to adjust for other modes.

---

## Current Release

`<For multi-surface projects, replace this section with one `### <Surface>` block per active surface, each shaped as below.>`

`<For projects between releases: replace the table below with a one-line "Now" status, e.g. *"Between releases — next: open Plan for Feature `<feature-slug>`. No active Release."*>`

**Release:** `<release-name>` `<(release-slug — Epic for Epic-based projects; Feature for Feature-based)>`
**Target:** `<version-tag | date>`
**Demo bar:** `<one-line statement of what this Release proves when shipped>`

`<For Epic-based projects: this Features-in-Release table lists the Features under this Epic.>`

| Feature | Size | Status |
|---|---|---|
| `<feature-slug>` | `<S | M | L>` | `<Done | In Progress | Not Started>` |

`<Active Feature(s) expand inline below — Tasks listed with per-Task status. Inactive Features in this Release show no Task drill-down yet.>`

### `<active-feature-slug>` — Tasks

| Task | Status |
|---|---|
| `<task-name>` (`<task-id>`) | `<Done | In Progress | Not Started>` |

---

## Future Releases

`<For multi-surface projects, same per-surface split as Current.>`

| Release | Target | Demo bar |
|---|---|---|
| `<release-slug>` | `<version | date>` | `<one-line demo statement>` |

### `<release-slug>` — Features

| Feature | Size | Scope |
|---|---|---|
| `<feature-slug>` | `<S | M | L>` | `<≤80-char scope summary; longer scope promotes to body section below>` |

`<Future Releases carry Features but no Task drill-down — Tasks split at Analyst scoping time per DOCUMENT_TEMPLATES.md.>`

`<Optional body sections for Features whose scope exceeds the 80-char cell allowance:>`

#### `<feature-slug>`

`<Multi-sentence scope description. References to DECISIONS.md anchors, BACKLOG items, or parity items.>`

---

## Past Releases

`<For multi-surface projects, same per-surface split.>`

### Semver mode

| Version | Date | Demo bar |
|---|---|---|
| `<component>-v<semver>` | `<YYYY-MM-DD>` | `<one-line demo statement>` |

#### `<component>-v<semver>`

**Shipped:** `<YYYY-MM-DD>`
**Merge:** `<commit-SHA or review-request-#>`
**Contents:**

- `<Feature or Task slug>` — `<one-line shipped description, ≤80 chars; longer promotes to its own subsection>`
- `<Bug>` `<B-xxx>` — `<one-line fix description>`

### Date-keyed mode

For deploy-continuous projects (consulting sites, content sites — `Versioning = date-keyed` in `PROJECT_GUIDE.md § Project mode`). Replace the Version column with a Feature column; date is the key.

| Feature | Shipped | Demo bar |
|---|---|---|
| `<feature-slug>` | `<YYYY-MM-DD>` | `<one-line demo statement>` |

#### `<feature-slug>`

**Shipped:** `<YYYY-MM-DD>`
**Contents:**

- `<Task slug>` — `<one-line shipped description>`

---

*Last updated `<YYYY-MM-DD>`.*
