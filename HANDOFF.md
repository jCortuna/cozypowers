# Handoff: cozypowers plugin → publish to GitHub

**Purpose of this file:** This plugin was designed and built in a Claude.ai chat
session. That session cannot push to GitHub (no credentials in a web chat). You,
Claude Code, are being handed the finished bundle to (a) verify, (b) create a
GitHub repo with the developer's own `gh` CLI, and (c) install and smoke-test.
Read this whole file, confirm the plan with the developer, then proceed.

Address the developer as **"Master"** and keep a competent-butler tone. Before
executing anything with side effects (repo creation, pushes, installs), present
a short plan and get approval first. This is a standing preference.

---

## What this project is

**cozypowers** ("Code, but cozy") is a Claude Code plugin: a lean software-
development methodology sized for a *solo* developer. It is a clean-room
recreation of the workflow popularized by the "Superpowers" plugin (obra/
superpowers), rebuilt from scratch because the developer does not want to run
third-party plugin code (hooks/scripts/telemetry) for security reasons.

**Hard design constraints (do not violate):**
- Zero executable code. No hooks, no shell scripts, no binaries. Markdown + one
  JSON manifest only. This is the entire point — it must stay auditable in one
  sitting.
- Zero network calls / telemetry.
- Zero runtime dependencies.

## What's in the bundle

```
cozypowers/
├── .claude-plugin/
│   ├── plugin.json          # plugin manifest
│   └── marketplace.json     # lets the repo double as a plugin marketplace
├── commands/                # 5 slash commands
│   ├── brainstorm.md  plan.md  execute.md  debug.md  ship.md
├── skills/                  # 6 skills (the methodology)
│   ├── brainstorming/SKILL.md
│   ├── writing-plans/SKILL.md
│   ├── executing-plans/SKILL.md
│   ├── test-driven-development/SKILL.md
│   ├── systematic-debugging/SKILL.md
│   └── shipping/SKILL.md
├── README.md
├── LICENSE                  # MIT
├── .gitignore
├── CLAUDE.md                # points future sessions at this file
└── HANDOFF.md               # this file
```

## Design decisions already made (do not re-litigate unless asked)

- **Lean six-skill set**, not the full Superpowers suite. The workflow is:
  brainstorming → writing-plans → executing-plans, with test-driven-development
  and systematic-debugging as always-available support, and shipping as the
  final gate.
- **Deliberately omitted** from the original: subagent-driven development with
  parallel agent dispatch + two-stage review, git-worktree parallelism, and the
  meta skill-authoring system. Judged to be team ceremony, excessive for one
  developer. Can be added later if the absence is felt.
- **shipping** skill was merged from Superpowers' separate verification and
  branch-finishing skills, and tuned to this developer's world: it checks
  player-visible naming before landing, and reminds the agent to review any
  automated release-notes/changelog PR that a push to `staging` triggers.
- **No session-start hook** (that would be executable code). The zero-code
  substitute is a CLAUDE.md snippet in the README that the developer pastes into
  their own projects to raise skill-trigger rates.

## Developer context worth knowing

- Solo indie dev; brand is **Cozybara**, platform is **kweba.space** (a free
  browser-based multiplayer strategy board game site).
- Uses a **staging-branch workflow** with a GitHub Actions setup that drafts
  release notes / changelog as a PR on push to `staging` (never auto-publishes).
  The shipping skill was written to cooperate with this.
- On Claude Pro. Works in stolen hours — hence the emphasis throughout on small
  tasks, checkpoints, and resumability.

---

## YOUR TASK

### Step 0 — Confirm with the developer
Ask (if not already answered):
1. GitHub username / which account.
2. Repo name — default `cozypowers`.
3. **Public or private?**
Then present the plan below and get a go-ahead.

### Step 1 — Verify the bundle
- `find . -type f` — expect 1 `plugin.json`, 1 `marketplace.json`, and markdown.
- Confirm there is **no** `hooks/` or `scripts/` directory and no executable
  files. If there are, stop and flag it — that would violate the core principle.
- **Verify `marketplace.json` and `plugin.json` against the CURRENT Claude Code
  plugin docs / your installed version.** These were written from memory in a
  web session and the schema may have drifted — check
  https://docs.claude.com/en/docs/claude-code/overview and the plugin/
  marketplace reference, and correct the manifests if needed. Do not assume they
  are right.

### Step 2 — Create the repo (with the developer's own credentials)
Preferred, using the GitHub CLI already authenticated on this machine:
```bash
gh repo create <username>/cozypowers --<public|private> --source=. --remote=origin --description "Code, but cozy — a lean solo-dev methodology plugin for Claude Code"
```
If `gh` is not installed/authenticated, fall back to creating the repo on the
web, then wire up the remote manually.

### Step 3 — Commit and push
```bash
git init            # if not already a repo
git add .
git commit -m "feat: initial cozypowers plugin — lean solo-dev methodology"
git branch -M main
git push -u origin main
```

### Step 4 — Install and smoke-test the plugin locally
Two options; pick with the developer:
- **Local:** `cp -r . ~/.claude/plugins/cozypowers` (or symlink), restart Claude
  Code, run `/plugin` and confirm cozypowers is listed and the 5 slash commands
  resolve.
- **From the new marketplace repo:**
  `/plugin marketplace add <username>/cozypowers` then
  `/plugin install cozypowers@cozypowers`.
Verify at least one skill triggers (e.g. run `/brainstorm` and confirm the
brainstorming skill loads).

### Step 5 — Report back
One-sentence summary to the developer: repo URL, visibility, install method
used, and confirmation the commands/skills resolve. Note any manifest
corrections you had to make in Step 1.

---

## Notes / open questions to raise
- The `author`/`owner` fields currently say "Cozybara" — offer to set the
  developer's real name or GitHub handle before the first commit if preferred.
- Once the repo exists, the README's install instructions reference
  `<yourusername>/cozypowers` — offer to replace that placeholder with the real
  path and amend the commit.
