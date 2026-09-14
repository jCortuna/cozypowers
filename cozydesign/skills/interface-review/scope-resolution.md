# Scope resolution

Turning a review target into a file list. The git is ordinary; what follows are the non-obvious parts and the traps that fail silently and leave the scope block claiming coverage it never delivered.

## Default branch

Try `refs/remotes/origin/HEAD`, then `gh repo view --json defaultBranchRef`, then `init.defaultBranch`. If the remote HEAD ref is missing, `git remote set-head origin --auto` asks the remote (network; writes only under `.git` - permitted; note it in Verification). With no remote at all, fall back to local `main` or `master` and state which base you assumed.

## Targets

Accepted: `working`, `staged`, `branch`, `pr <n>`, a bare `<ref>`, and explicit `<a>..<b>` or `<a>...<b>` ranges. Anything else is treated as a `<ref>`.

- Diff a **branch** against the merge base (three dots). Two dots would count every upstream commit that landed on the base as part of the change.
- For an **explicit range**, use the dots the developer wrote: `a..b` compares endpoints; `a...b` compares `merge-base(a, b)` with `b`. Rewriting `release..feature` to three dots silently drops exactly what was asked for. State the resolved range.
- `git diff HEAD` covers tracked files only. Any target including uncommitted work must also include untracked files (`git ls-files --others --exclude-standard`), or a newly added component vanishes from a scope reported as complete. For `branch` with uncommitted work, report the two counts separately.

## Pull requests

- Fetch the head into a remote-tracking ref - `git fetch origin "pull/<n>/head:refs/remotes/pr/<n>"` - and review in place. Works for forks, unlike `origin/<branch>`.
- Read files at that ref (`git show refs/remotes/pr/<n>:path`), never the working-tree copy - on a fork PR it's a different file.
- `gh pr diff <n>` gives patch text but no unchanged context or consumers; fetch the ref as well.
- **Citations:** line numbers from the fetched ref may not match the working tree - cite against the head ref and declare it (with SHA) in the scope block.
- **Intent:** the PR title and body from `gh pr view`; add commit subjects when the body is empty.

## Awkward repository states

Most failures are loud at merge-base (no remote, unrelated histories, empty repo, moved submodule pointer) - say the base is unresolvable and stop. Never review a range you can't name. Three need handling:

- **Detached HEAD** - use the merge base against the default branch; name the SHA, not a branch.
- **Shallow clone** (CI default; merge-base returns nothing) - `git fetch --deepen=50`, retry, then `--deepen=200`, then report unresolvable. Deepening writes only to `.git`; note it in Verification.
- **Mid-rebase or mid-merge** - the silent one: `git diff` succeeds but isn't the change. Detect via `git rev-parse --git-path` for `rebase-merge`, `rebase-apply`, `MERGE_HEAD`, `CHERRY_PICK_HEAD` (don't test `.git/` paths directly - they aren't directories in linked worktrees). Stop and say the tree is mid-operation.

## Nothing to review

Gather facts before asking: current branch, clean or dirty, count ahead of base, last commit SHA and subject, and any open PR from `gh pr status`. That command succeeds with an empty result when no PR exists; it fails without `gh`, without auth, or without a GitHub remote - treat any failure as "no pull request found", say so, and offer the remaining routes. Put the last commit's SHA and subject inside the offer so the developer can recognize "a1b2c3d Merge pull request #482" as not what they meant.

## Renames

`--name-status` reports renames (`R100 old new`) by default. When a file was moved and edited, widen detection with `--find-renames=40% --find-copies-harder`. Review a rename as a move: only genuine edits are in scope.

## Exclusions

Exclude and name in the scope block - they're machine-authored and carry no interface rules:

| Category | Patterns |
| --- | --- |
| Lockfiles | `package-lock.json`, `pnpm-lock.yaml`, `yarn.lock`, `bun.lock`, `bun.lockb`, `Cargo.lock`, `composer.lock`, `Gemfile.lock`, `poetry.lock`, `uv.lock` |
| Snapshots, fixtures | `__snapshots__/`, `*.snap`, `*.approved.*`, `test-results/`, `playwright-report/` |
| Generated output | `dist/`, `build/`, `out/`, `.next/`, `.turbo/`, `.svelte-kit/`, `coverage/`, `storybook-static/`, `*.min.js`, `*.min.css`, `*.map` |
| Generated sources | `*.gen.ts`, `*.generated.*`, build-emitted `*.d.ts`, GraphQL/Prisma client output |
| Vendored | `vendor/`, `third_party/`, `node_modules/` |
| Binaries, media | `*.png`, `*.jpg`, `*.webp`, `*.avif`, `*.woff2`, `*.mp4`, `*.pdf` |

Two stay in scope through the code that references them: an added or swapped **font file** (typography) and an **image** added to a component (UI and accessibility, via alt text and outline).

Apply exclusions as pathspecs so the reported count is the reviewed count. Two silent under-exclusion traps: `*.lock` misses `package-lock.json` and `pnpm-lock.yaml` (cover every name in the table), and `**` needs glob magic - without it `**/dist/**` misses a root-level `dist/`. Compare counts with and without the pathspecs; the difference should equal the files you named.

## Expanding to consumers

One hop by default; two for tokens and shared primitives. Use the project's resolver if it has one, otherwise import paths.

- `git grep` searches the working tree unless you pass the reviewed ref after the pattern - on a PR you'd miss importers the change added. Read results with `git show <rev>:path`. Use `-e` when a pattern starts with a dash (e.g. `--color-*`).
- For a changed token or theme value, search the **token name**; consumers reference names, not files.

Order consumers by a reproducible rule:

1. **Route and layout entry points first** - whatever the framework renders as a surface (`app/**/page.*`, `app/**/layout.*`, `pages/**`, `routes/**`, `src/views/**`, `*.astro` pages).
2. **Then by importer count** - a component used by twenty files carries more of the change.
3. **Ties by proximity** - same package or feature directory first.

Review the first five, state how many were skipped, and say plainly if ordering became arbitrary past some point.
