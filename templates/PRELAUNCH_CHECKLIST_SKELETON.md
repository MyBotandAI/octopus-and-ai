# `<project-name>` — Pre-Launch Checklist

**Owner:** PO  
**Targets:** `<launch-target-A>` · `<launch-target-B>`  
**Updated:** `<YYYY-MM-DD>`

Earned when launch is in sight (per `DOCUMENT_TEMPLATES.md § Incremental adoption`). Lists everything that must be true before public release. Reviewed at the end of each release cycle; items completed are checked off, items earned during the cycle are added.

---

## How this skeleton adapts to Project mode

- **Multi-surface = No** → drop the `## Shared` / `## <Surface>` split; use a flat checklist.
- **Multi-surface = Yes** → use the per-surface structure below (Shared section + one section per surface).
- **Versioning = date-keyed** → `Targets:` line carries date milestones instead of version tags.

---

## Shared (both surfaces inherit)

`<For single-surface projects, this whole "## Shared / ## <Surface>" split disappears — use flat sections below directly.>`

### 1. `<area — e.g. Domain & Infrastructure>` `<✅ when complete>`

- [ ] `<concrete blocking item>`
- [ ] `<concrete blocking item>`

#### Pending pre-launch
- [ ] `<item still open at this stage>`

#### Known issues (non-blocking)
- [ ] `<item that exists but does not block launch — track here so it's visible but not gated on>`

### 2. `<area — e.g. Email Setup>`
...

### N. `<area — e.g. Legal & Compliance>`
...

### Pending decisions

Decisions surfaced by launch prep that are **not yet locked**. Each item carries a one-line description and the role responsible for surfacing the OQ. Lock via the OQ → PO answer → `DECISIONS.md` row flow (per D2 in `methodology/DIRECTIVES.md`); then check off here.

- [ ] `<decision-name>` — `<one-line summary; Analyst / DEV / UX / Architect to surface OQ to PO>`

---

## `<Surface A — e.g. Mobile>` (`<launch target>` submission)

### A1. `<area>`

- [ ] `<item>`

### A2. `<area>`

- [ ] `<item>`

### A3. `<area>` — `<status emoji if useful, e.g. 🟡 In Progress>`

- [ ] `<item>`

### A`<n>`. Pre-Launch Sign-Off (`<Surface A version>`)

All items below must be confirmed before submitting `<launch-target-A>`:

- [ ] `<gating item — usually a cross-reference up to a Shared or per-surface checkbox above>`
- [ ] `<gating item>`

---

## `<Surface B — e.g. Web>` (`<launch target>` launch)

`<Same shape as Surface A. Items unique to this surface; shared items live in the Shared section above.>`

### B1. `<area>`

- [ ] `<item>`

### B`<n>`. Pre-Launch Sign-Off (`<Surface B version>`)

- [ ] `<gating item>`

---

## Priority for the current cycle

Snapshot view of what matters most right now. **Source of truth is the checkboxes above — this section is a derived snapshot, not authoritative.** Update or delete when the cycle's focus shifts.

**🔴 Critical for launch:**
1. `<item, with surface tag>`
2. `<item, with surface tag>`

**🟡 Important before launch:**
3. `<item>`

**🟢 Nice to have:**
4. `<item>`

---

*Last updated `<YYYY-MM-DD>`. Source of truth is the checkbox state above; priority section is a derived snapshot for triage.*
