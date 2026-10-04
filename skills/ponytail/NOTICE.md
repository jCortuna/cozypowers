# Notice: ponytail

This skill is a clean-room rewrite, in cozypowers' own words, of the idea behind
the community **ponytail** skill by DietrichGebert:
[github.com/DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail).

It was written from public descriptions of that project - its seven-rung ladder
(needed? → codebase → stdlib → native → installed dependency → one line →
minimum), its never-cut list, its lite / full / ultra levels, and its practice of
marking shortcuts with `ponytail:` comments. No text or code from the upstream
repository was copied, and the upstream repository itself was not read.

Deliberately left out:

- **The SessionStart hook** that injects the ruleset into every session.
  cozypowers ships no executable code. The skill relies on its description, on
  `executing-plans` climbing the ladder before each implementation step, and on
  the README's CLAUDE.md snippet instead. An independent JetBrains test (80
  paired tasks, July 2026) found the copied skill never switched itself on
  without the hook, so expect weaker activation than upstream unless you use
  `/ponytail` or the snippet.
- **The separate `ponytail-debt` and help skills.** Shortcut tracking is folded
  into `shipping`, which lists every `ponytail:` comment on the branch before
  landing.

The same JetBrains test measured roughly 15% less code and 10% lower cost with no
significant quality change, concentrated on larger tasks (300+ lines). Expect
little difference on small changes.
