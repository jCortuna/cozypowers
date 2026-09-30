# Notice: unlazy

This skill is a clean-room rewrite, in cozypowers' own words, of the idea behind
the community **unlazy** skill:

- [Leonxlnx/unlazy](https://github.com/Leonxlnx/unlazy) (MIT)
- [CartyChris/unlazy-skill](https://github.com/CartyChris/unlazy-skill) (MIT)

Borrowed ideas: the `GATES.md` acceptance ledger with `CHECK` / `EXPECT` /
`EVIDENCE` lines, the depth tree with leaf and branch gates, the four-pass leaf
work, and the report audit (re-measure every number before reporting).

No text or code was copied. Deliberately left out:

- `gate-check.mjs`, `gate-lint.mjs`, `stop-hook.mjs`, `install-hooks.mjs` - Node
  scripts and a Claude Code Stop hook. cozypowers ships no executable code; the
  checks are run by the agent's own tools and the ledger is re-checked by the
  `shipping` skill instead.
- The orchestrated and parallel modes that dispatch sub-agents per leaf. Like
  the rest of cozypowers, this skill is sized for one developer in one session.
