# cozypowers

*Code, but cozy.* A lean software-development methodology for Claude Code, sized for a solo developer. Inspired by the workflow popularized by the Superpowers plugin, but written from scratch as a clean-room recreation you can audit in one sitting.

## Why this exists

Third-party plugins can ship session hooks, shell scripts, and telemetry that execute on your machine. This plugin ships **none of that**:

- **Zero executable code.** No hooks, no scripts, no binaries. Every file is markdown or a small JSON manifest.
- **Zero network calls.** Nothing phones home, ever.
- **Zero dependencies.** Nothing is downloaded at install or run time.
- **Auditable in minutes.** Seven skills, six commands, two small manifests. Read it all before installing - please do.

## What's inside

The workflow, end to end:

| Stage | Skill | Slash command |
|---|---|---|
| 1. Refine the idea | `brainstorming` | `/brainstorm` |
| 2. Shape it into a spec | `shaping-specs` | `/spec` |
| 3. Break it into tasks | `writing-plans` | `/plan` |
| 4. Do the work | `executing-plans` | `/execute` |
| (while implementing) | `test-driven-development` | - |
| (when things break) | `systematic-debugging` | `/debug` |
| 5. Land it | `shipping` | `/ship` |

`shaping-specs` is optional - it earns its keep on features big enough that "what exactly are we building" deserves its own written answer. Small changes can go straight from `/brainstorm` to `/plan`.

Design principles baked in: designs approved before code, plans in 2-15 minute tasks that each end green and committed, RED-GREEN-REFACTOR with the watch-it-fail rule, root cause before fixes, evidence before completion claims, and checkpoints so work is resumable across short solo-dev sessions.

Deliberately **not** included from the original inspiration: subagent-driven development with parallel agent dispatch and two-stage review, git-worktree parallelism, and the meta skill-authoring system. Those earn their keep on teams running long autonomous sessions; for one developer they are mostly ceremony. Add them later if you feel the absence.

## Installation

### Option A - skills-directory plugin (simplest, fully offline)

Copy this folder into your personal skills directory:

```bash
cp -r cozypowers ~/.claude/skills/cozypowers
```

It loads automatically on your next Claude Code session as `cozypowers@skills-dir` - no marketplace, no install step. Verify with `/plugin` or `claude plugin list`.

### Option B - your own marketplace (survives machine moves, easy updates)

This repo doubles as its own marketplace ([`jCortuna/cozypowers`](https://github.com/jCortuna/cozypowers)):

```
/plugin marketplace add jCortuna/cozypowers
/plugin install cozypowers@cozypowers
```

or non-interactively:

```bash
claude plugin marketplace add jCortuna/cozypowers
claude plugin install cozypowers@cozypowers
```

Because you own the repo, updates only happen when *you* push them.

## Shaping specs

Before planning a feature, shape it first:

```
/spec
```

This reads any `standards/` and `product/` context in the current project, asks a few scoping questions, and drafts a spec folder under `specs/` for your review. Once approved, hand it to `/plan` - writing-plans will pick up the spec automatically if one exists.

Neither `standards/` nor `product/` is required. Without them, `/spec` and `/plan` behave exactly as before.

## Recommended: the CLAUDE.md nudge

The original inspiration uses a session-start hook (executable code) to make the agent aware of its skills. We skip the hook on principle. The zero-code equivalent: paste this into your project's `CLAUDE.md`:

```markdown
## Development methodology

This project follows the cozypowers workflow. Before any feature work, bug fix,
or behavior change, check the cozypowers skills and use the one that fits:
brainstorming before new code, writing-plans before multi-file work,
test-driven-development for all logic, systematic-debugging for any bug,
shipping before declaring anything done. These are mandatory workflows,
not suggestions.
```

Skills also trigger on their own descriptions, and the slash commands invoke them explicitly - the snippet just raises the hit rate at session start.

## Auditing this plugin

```bash
find cozypowers -type f            # expect: 2 json manifests, markdown, LICENSE - nothing else
grep -rn "http" cozypowers          # expect: nothing executable, no URLs fetched
```

If a future version of this plugin ever contains a `hooks/` or `scripts/` directory, that version was not written under these principles - read it before trusting it.

## License

MIT. Do as you please; a wave to the capybara is appreciated.
