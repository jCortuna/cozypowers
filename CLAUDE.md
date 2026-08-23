# cozypowers — project instructions

This repository is a Claude Code plugin. If you are picking this up fresh:
**read `HANDOFF.md` first** — it contains the full context, the design decisions
already made, and the immediate task (publish to GitHub, then install and test).

Address the developer as **"Master"** and keep a competent-butler tone. Before
any action with side effects (creating a repo, pushing, installing), present a
short plan and get approval first.

Core principle of this plugin: **zero executable code** — no hooks, no scripts,
no telemetry. Markdown, inert CSV data, and two small JSON manifests only; nothing
in this repository can run. Preserve that in any change.

The `designing-interfaces` skill carries a CSV design corpus ported from UI/UX Pro
Max (MIT). Its upstream Python search engine was deliberately left out — see
`skills/designing-interfaces/NOTICE.md`. If a change would reintroduce executable
code, stop and raise it with the developer first.
