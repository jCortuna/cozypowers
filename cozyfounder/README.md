# cozyfounder

*Business, but cozy.* Eleven skills that test a business before you launch it. A
companion plugin to [cozypowers](../README.md), living in the same marketplace and
built to the same rules:

- **Zero executable code.** No hooks, no scripts. Markdown, two inert example data
  files and two small manifests. Every calculation the original pack did in Python
  is now a written procedure the agent follows by hand, showing its working.
- **Zero network calls from the plugin.** Research steps *ask* the agent to look
  things up during your session, and every fetched page is treated as data, never
  as instructions.
- **No broad permissions.** Buyer sub-agents get no tools; they reply with JSON and
  the moderator validates and files each answer.

A clean-room recreation of [The Founder skill](https://github.com/Jakeschincariol/founder-skill)
by Jake Schincariol (MIT). See [CREDITS.md](CREDITS.md) for what changed and why.

## What's inside

| Skill | Role | What it does |
| --- | --- | --- |
| `cozy-founder-board` | Board of directors | Three lenses (Offers, Monopoly, Product) score the idea, name what would kill it and vote |
| `cozy-founder-competitors` | Competitor scout | Direct, indirect and substitute competitors with prices, positioning and complaints, every fact linked |
| `cozy-founder-consumer` | Consumer panel | 20 simulated buyers by default (100 on request), each an isolated sub-agent; tallies who buys and why |
| `cozy-founder-pricing` | Pricing strategist | Van Westendorp range by hand, against competitors and margin; a price, a ladder and what to test |
| `cozy-founder-offer` | Offer architect | Bonuses, an affordable guarantee, true urgency and a name, re-tested on the same buyers |
| `cozy-founder-cfo` | CFO | Contribution, margin at plan, break-even, year 1 by month, cash needed, payback, what-ifs |
| `cozy-founder-marketing` | Marketing director | Positioning, channels, a dated 30-day campaign, ten hooks, the most a customer may cost |
| `cozy-founder-brand` | Brand designer | Names with trademark, domain and handle checks; voice, promise and a look brief |
| `cozy-founder-ops` | Operations manager | Suppliers, rota, SOPs, tools, permits to confirm and a risk register |
| `cozy-founder-launch` | Launch lead | A cheap real test first, then a dated countdown, run sheet and 30-day review |
| `cozy-founder-plan` | Business planner | The plan, a summary and a one-pager, with a verdict decided by fixed checks |

Run them in order; each reads what the others wrote in a `founder/` folder in your
project. Any one can also run alone.

```
board → competitors → consumer → pricing → offer → cfo → marketing → brand → ops → launch → plan
```

## Install

**Claude Code** (from the cozypowers marketplace):

```
/plugin marketplace add jCortuna/cozypowers
/plugin install cozyfounder@cozypowers
```

Skills appear as `/cozyfounder:cozy-founder-board` and so on.

**Antigravity**: this folder is also an Antigravity plugin (`plugin.json` at the
root, skills in `skills/`). Copy the `cozyfounder/` folder to
`.agents/plugins/cozyfounder/` in a workspace, or to `~/.gemini/config/plugins/`
for every workspace. To use the skills without the plugin wrapper, copy the
`skills/cozy-founder-*` folders into the workspace's `.agents/skills/`.
Where sub-agents are not available, the board and the panel switch to a
one-at-a-time fallback and label their results as less independent.

## Honest limits

- **The panel is simulated buyers, not customers.** Good for objections, segments
  and wording; bad at predicting conversion. Read the buy rate as an upper bound
  and confirm with real people; `cozy-founder-launch` starts with exactly that.
- **Hand arithmetic can slip.** The CFO procedure carries a worked example the
  agent must reproduce first and three cross-checks it must pass, and every line
  of working is written out for you to check.
- **The numbers are only as good as the inputs.** Check costs with suppliers and
  structure, payroll and tax with an accountant.
- **Not financial, legal or tax advice.**

## Files

```
cozyfounder/
├── .claude-plugin/plugin.json      # Claude Code manifest
├── plugin.json                     # Antigravity manifest
├── README.md  CREDITS.md
└── skills/
    ├── cozy-founder-board/         SKILL.md, lenses.md
    ├── cozy-founder-competitors/   SKILL.md
    ├── cozy-founder-consumer/      SKILL.md, dealing.md, brief-template.md,
    │                               example-customer.json, example-pitch.md
    ├── cozy-founder-pricing/       SKILL.md, van-westendorp.md
    ├── cozy-founder-offer/         SKILL.md
    ├── cozy-founder-cfo/           SKILL.md, formulas.md, example-numbers.json
    ├── cozy-founder-marketing/     SKILL.md
    ├── cozy-founder-brand/         SKILL.md
    ├── cozy-founder-ops/           SKILL.md
    ├── cozy-founder-launch/        SKILL.md
    └── cozy-founder-plan/          SKILL.md
```
