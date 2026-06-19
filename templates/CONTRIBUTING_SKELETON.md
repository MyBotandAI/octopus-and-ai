# Contributing to `<project-name>`

---

## Branch naming

Format: `<type>/<scope>/<short-description>`

**One branch per Task.** See D1 in `methodology/DIRECTIVES.md`.

### Branch types

| Type | Used for |
|---|---|
| `feat` | New functionality |
| `fix` | Bug fixes |
| `refactor` | Code restructure with no behaviour change |
| `build` | Build system, dependencies, deploy config, infra files |
| `ci` | Continuous integration configuration |
| `docs` | Documentation-only changes that need a branch |
| `hotfix` | Emergency fix branched off a release tag (see § Hotfix policy) |
| `spike` | Throwaway exploration — never merged |

`hotfix` and `spike` are branch-only markers — they describe workflow, not commit semantics. Commits inside those branches still use one of the commit types below.

### Scopes

Project-specific. Define them per project:

| Scope | Used for |
|---|---|
| `<scope>` | `<description>` |

---

## Commit messages

Conventional Commits format: `<type>(<scope>): <imperative subject ≤72 chars>`

Optional body explaining *why*, not *what*. Optional footer for refs or breaking changes.

### Commit types

Curated subset of [Conventional Commits 1.0](https://www.conventionalcommits.org). Use the most specific type that fits.

| Type | Used for | Example |
|---|---|---|
| `feat` | New functionality | `feat(web): scaffold app shell` |
| `fix` | Bug fix | `fix(api): correct date timezone offset` |
| `docs` | Documentation only | `docs(repo): add CONTRIBUTING.md` |
| `refactor` | Code restructure with no behaviour change | `refactor(api): extract state machine` |
| `build` | Build system, dependencies, deploy/infra config | `build(deps): bump <dependency> to <version>` |
| `ci` | Continuous integration config | `ci(repo): run the test suite on the review request` |
| `revert` | Reverting a previous commit | `revert(web): drop offline shell strategy` |

**No `chore` type.** What used to land under `chore` now resolves to one of the more specific types above — most commonly `build` (deps, config, deploy files) or `refactor` (behaviour-neutral cleanups). If a commit genuinely doesn't fit any of the seven types above, the change is probably too mixed and should be split.

---

## Direct-to-default-branch commits

The default branch (`<main | master | …>`) is always green. Most work goes through a branch (see § Branch naming).

**Exceptions allowed direct to the default branch:**

| Type | Constraint |
|---|---|
| `docs(<scope>):` | Any documentation-only commit — ROADMAP updates, DECISIONS rows, README typos, etc. |
| `fix(<scope>):` | Single-purpose `B-xxx` one-liner fixes where the diff is obviously safe and would not benefit from a review request. |

All other work — `feat`, `refactor`, multi-file `fix`, `build`, `ci`, `revert` — goes through a branch and a review request.

---

## Hotfix policy

Branch off a release tag *only* when the default branch contains unfinished work you do not want to ship.

| Default-branch state | Action |
|---|---|
| Clean and deployable | Fix on the default branch via `fix/<scope>/<desc>` branch (or direct-to-default-branch per § above if it qualifies), tag a new patch version, ship. |
| Has unfinished work | Branch `hotfix/<scope>/<version>-<desc>` off the latest release tag, fix, tag, merge back to the default branch. |

Commits inside a `hotfix/...` branch use commit type `fix:`, not `hotfix:`.

Do not pre-emptively create release branches.

---

## Release tags

Format: `<component>-v<semver>`. Components match branch scopes that are independently versioned.

Tag the merge commit on the default branch after merging the release work. Tags are immutable — if you mistag, create a new tag, do not move existing ones.

---

## Review-request and merge policy

- **Task branches:** agents commit and push (DEV implements; QA reviews). Push cadence: at session pause (one push per pause; no intermediate pushes).
- **Opening the review request:** QA opens it when its review is 100% Pass — all AC Pass, zero Flags, no unresolved OQs, tests pass. QA writes the body from the AC review + spec summary.
- **Approval and merge:** PO only.
- **Release tags:** PO only. Analyst may suggest a tag at Task closure with a one-line rationale; PO executes.
- **Default branch:** PO only — direct commits, merges, tags, deploys.

See D1 in `methodology/DIRECTIVES.md`.
