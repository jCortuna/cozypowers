---
name: interface-review
disable-model-invocation: true
description: Review a change - uncommitted work, the current branch, a pull request, a ref, or a commit range - for interface quality across UI polish, typography, layout, color, writing, and accessibility. Resolves the change scope, expands changed files to the surfaces they affect, reads both sides of the diff, classifies each finding as Introduced, Regression, or Pre-existing, and hands the review to better-interface. Invoke as /interface-review [working | staged | branch | pr <n> | <ref> | <a>..<b>].
---

# Interface Review

Reviews a **change**, not a screen. This skill owns the scope: resolve it, expand changed files to affected surfaces, read both sides of the diff, classify every finding. Domain rules belong to the **better-\*** skills; severity, consolidation, coverage, cap, and verdict belong to **better-interface**.

Correctness, tests, security, and performance belong to the project's general code review - name such a concern once and move on.

## The change, not the codebase

The author is asking "did I make this worse?" Report what the change caused and stay mostly quiet about what it merely touched - three pre-existing findings is a courtesy; thirty is a different, unrequested review.

Read the change fully before judging it. The stated intent decides what counts as incomplete, and a skimmed diff produces findings the next hunk already fixed.

## Principles

### 1. Resolve the change scope first

The whole invocation is the target: `/interface-review pr 482` reviews PR 482. Accepted targets and resolution rules: [scope-resolution.md](scope-resolution.md).

With no target, stop at the first match:

1. **HEAD is ahead of the merge base** with the default branch → that range **plus** any uncommitted changes, stating commit count and uncommitted file count separately.
2. **Working tree is dirty** → the uncommitted changes.
3. **Neither** → there's no change; ask (principle 2).

Order matters: check the working tree first and one stray formatting edit hides a twelve-commit branch while the report claims full coverage.

Exclude lockfiles, snapshots, generated output, vendored code, and binaries, and name what you excluded.

### 2. With no change, ask - don't invent one

A clean tree with nothing ahead of the merge base means the requested change doesn't exist. **Never silently fall back to the last commit** - it may be a merge or someone else's work. State the repository facts, check for an open PR on the current branch (offer it first - a branch whose commits already landed still has the PR the developer meant), then offer:

- **The last commit**, named by short SHA and subject.
- **A target they name** - PR, branch, ref, or range.
- **A whole-repository interface audit** - a different review; hand it to better-interface directly, without scope block, statuses, or pre-existing section.

If exclusions emptied the scope, list what was excluded and ask the same way. Never Approve a review of nothing.

### 3. A diff is not a surface

A changed file is evidence; its **blast radius** - the surfaces it renders in - is the review subject. Expand one hop (direct importers and callers) by default; two hops only for design tokens, theme values, and shared primitives. Review **at most five consumers**, ordered per [scope-resolution.md](scope-resolution.md#expanding-to-consumers), and state how many you didn't expand.

### 4. Read the removed lines

Regressions are invisible in the post-change state. Read the `-` side of every hunk against [removed-signals.md](removed-signals.md). A signal is a lead, not a finding: it's a regression only if nothing in the change replaces it, and the owning domain skill decides. Report only what that skill confirms, with status `Regression`, so the author knows something that worked now doesn't.

### 5. Classify every finding

- **Introduced** - the change created it.
- **Regression** - the change weakened something previously correct.
- **Pre-existing** - in touched code but not caused by the change.

Status by what the diff touched, not by file: an untouched line three lines from a hunk is Pre-existing. When it matters, confirm with `git blame` against the base ref.

### 6. Hold the change to its stated intent

Read the PR title and body, linked issue, and commit messages, then check the interface delivers what they claim. This catches the **incomplete** change - the states that are absent:

- A new variant, size, or theme applied to some states but not all (hover, focus, active, disabled, loading, selected).
- A new user-facing string missing from the project's translation catalog.
- A new component without empty, loading, error, disabled, or narrow-width states.
- A control added to one surface but not to siblings that carry its peers.

Don't report scope creep - that's a process question.

### 7. Hand off to better-interface

Pass the scope block, affected surfaces, and a status on every finding. better-interface routes to the domains, applies severity, consolidates, enforces the cap, and issues the verdict. If it's unavailable, report the resolved scope and file inventory, name the missing skill, and stop - don't invent a severity scale, cap, or verdict.

### 8. Never mutate the working tree

Read-only, including the checkout. Fetching refs is fine (`git fetch` writes only inside `.git`). **Never** `git checkout`, `git switch`, `git stash`, or `gh pr checkout` - they rewrite files the author has open. Rendered verification is opt-in: mark visual and runtime claims **Not verified** unless there's a cheap preview or the developer asks; then use an isolated `git worktree` on the fetched ref and remove it afterwards.

## Before you finish

| Mistake | Fix |
| --- | --- |
| One stray edit reviewed instead of the branch | Check merge base before working tree; report both counts |
| Last commit reviewed because nothing changed | State facts; offer last commit, a named target, or a repo audit |
| Hunks reviewed without consumers | Expand one hop (two for tokens/primitives); name what was skipped |
| Only the `+` side read | Search the `-` side for removed a11y, focus, motion, text signals |
| Equivalent replacement reported as regression | Route the removal to its owner; report only confirmed regressions |
| Removal reported as a new mistake | Status it Regression |
| Nearby untouched line statused Introduced | Status by what the diff touched; confirm with blame on the base ref |
| PR checked out to review it | Fetch the ref and read it in place |
| Line numbers that don't exist on the reviewed ref | Cite against the head ref named in the scope block |
| Severity scale or cap restated here | Defer to better-interface |
| Correctness/test/security findings | Name once, point to code review, drop |

## Output

Open with the scope block:

| Field | Value |
| --- | --- |
| Target | `branch`, `working`, `staged`, `pr 482`, or the range as entered |
| Base ref | `origin/main` at `a1b2c3d` |
| Head ref | `refs/remotes/pr/482` at `e4f5g6h` |
| Commits | 7 committed, 2 files uncommitted |
| Files in scope | 12 after exclusions |
| Excluded | `pnpm-lock.yaml`, `src/__snapshots__/` - lockfile and snapshots |
| Surfaces expanded | `CheckoutPage`, `SettingsPanel`; 3 further `Button` consumers not expanded |

Then better-interface's coverage table unchanged (a domain with no evidence in the change is "Not reviewed: no evidence in the change scope" - a coverage statement, not a gap).

Then findings with a **Status** column:

| Severity | Domain | Status | Location | Before | After | Why |
| --- | --- | --- | --- | --- | --- | --- |
| HIGH | Accessibility | Regression | `src/Dialog.tsx:42` | `aria-label="Close"` removed | Restore `aria-label="Close"` on the icon-only control | The close control had an accessible name before this change |

No Introduced or Regression findings → omit the table: "No actionable interface findings in this change."

Then **Pre-existing** findings - at most three, highest severity first, plainly marked as not this change's responsibility (omit if none):

| Severity | Domain | Location | Issue |
| --- | --- | --- | --- |
| MEDIUM | Typography | `src/Toolbar.tsx:7` | Numeric badges use proportional figures; predates this change |

The cap and verdict cover Introduced and Regression only - pre-existing findings sit outside both, so touching a legacy file can't become a full audit, and a change whose only findings are pre-existing is an **Approve**. End with **Block** if any HIGH remains, otherwise **Approve**.
