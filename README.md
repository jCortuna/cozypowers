# cozypowers

*Code, but cozy.* A lean software-development methodology for Claude Code, sized for a solo developer. Inspired by the workflow popularized by the Superpowers plugin, but written from scratch as a clean-room recreation you can audit in one sitting.

## Why this exists

Third-party plugins can ship session hooks, shell scripts, and telemetry that execute on your machine. This plugin ships **none of that**:

- **Zero executable code.** No hooks, no scripts, no binaries. Every file is markdown, inert CSV data, or a small JSON manifest - nothing that can run.
- **Zero network calls.** Nothing phones home, ever.
- **Zero dependencies.** Nothing is downloaded at install or run time.
- **Auditable in minutes.** Eight skills, seven commands, two small manifests. Read it all before installing - please do.

## What's inside

The workflow, end to end:

| Stage | Skill | Slash command |
|---|---|---|
| 1. Refine the idea | `brainstorming` | `/brainstorm` |
| 2. Shape it into a spec | `shaping-specs` | `/spec` |
| 3. Break it into tasks | `writing-plans` | `/plan` |
| 4. Do the work | `executing-plans` | `/execute` |
| (while implementing) | `test-driven-development` | - |
| (when it has a UI) | `designing-interfaces` | `/design` |
| (when things break) | `systematic-debugging` | `/debug` |
| 5. Land it | `shipping` | `/ship` |

`shaping-specs` is optional - it earns its keep on features big enough that "what exactly are we building" deserves its own written answer. Small changes can go straight from `/brainstorm` to `/plan`.

`designing-interfaces` is the one skill that carries data rather than process: a
2,374-row design corpus - 192 colour palettes, 119 UX guidelines, 88 styles, 74
font pairings, 22 technology stacks and more - that Claude searches with its own
Grep tool. It is a zero-code port of [UI/UX Pro Max](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill)
(MIT, © 2024 Next Level Builder); see `skills/designing-interfaces/NOTICE.md`.

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

## Designing interfaces

For anything with a UI:

```
/design
```

This detects your stack rather than assuming it, searches the local design corpus,
and gives you one coherent design system - style, palette, type scale, spacing,
motion - instead of a pile of search results. It fixes things in priority order,
so accessibility and touch targets come before aesthetics.

Ask it to save the result and it writes `design-system/<project>/MASTER.md` into
your project, so the next session starts from your decisions instead of
re-litigating them. Page-specific overrides live in `pages/` beside it.

Three optional dials tune the output without changing the query: **variance**
(centred → bold), **motion** (subtle → complex), and **density** (spacious →
dashboard-dense), each 1-10.

## Recommended: the CLAUDE.md nudge

The original inspiration uses a session-start hook (executable code) to make the agent aware of its skills. We skip the hook on principle. The zero-code equivalent: paste this into your project's `CLAUDE.md`:

```markdown
## Development methodology

This project follows the cozypowers workflow. Before any feature work, bug fix,
or behavior change, check the cozypowers skills and use the one that fits:
brainstorming before new code, writing-plans before multi-file work,
test-driven-development for all logic, designing-interfaces for anything with
a UI, systematic-debugging for any bug, shipping before declaring anything
done. These are mandatory workflows, not suggestions.
```

Skills also trigger on their own descriptions, and the slash commands invoke them explicitly - the snippet just raises the hit rate at session start.

## Auditing this plugin

```bash
# 1. Nothing executable. This is the load-bearing check.
find cozypowers -type d \( -name hooks -o -name scripts \)     # expect: no output
find cozypowers -type f ! -name '*.md' ! -name '*.csv' ! -name '*.json'
                                                              # expect: LICENSE, .gitignore

# 2. Everything else is markdown, CSV data, or two small JSON manifests.
find cozypowers -type f -name '*.json'   # expect: plugin.json, marketplace.json,
                                         # and 2 inert data files under skills/designing-interfaces/data/
```

A note on URLs: the `designing-interfaces` corpus contains roughly 700 documentation
links in its CSV files - `fonts.google.com`, `tailwindcss.com`, `learn.microsoft.com`
and similar - so `grep -rn "http"` is no longer silent. They are inert strings in
data files. There is no code in this plugin, so there is nothing here that could
fetch them; they are there for you to click if you want the source.

That corpus was ported from [UI/UX Pro Max](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill).
Its upstream Python search engine was read and audited before being left out, and it
was clean - stdlib only, no subprocess, no `eval`, no network calls, and a single
opt-in write path with path-traversal and clobbering defences. It is omitted on
principle, not suspicion: this plugin ships no executable code, and that rule applies
to good code too. `skills/designing-interfaces/NOTICE.md` records the details.

If a future version of this plugin ever contains a `hooks/` or `scripts/` directory,
or any file that can execute, that version was not written under these principles -
read it before trusting it.

## License

MIT. Do as you please; a wave to the capybara is appreciated.

The `designing-interfaces` corpus is derived from
[UI/UX Pro Max](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill),
MIT © 2024 Next Level Builder. Full attribution, and a note on what was changed,
in `skills/designing-interfaces/NOTICE.md`.
