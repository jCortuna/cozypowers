# Taste memory

Tastemaker remembers through plain local files the agent reads and writes - no backend, no scripts. Read in this order; write to the smallest layer that fits.

| Layer | File | Holds |
| --- | --- | --- |
| Project style lock | `.tastemaker/style-lock.md` | This project's rules: palette + color contract, type, shape, spacing, structure, assets, motion, avoid list |
| Project decision log | `.tastemaker/decisions.log` | Append-only keep / reject / pending-review evidence |
| Project build log | `.tastemaker/log.json` | Structural picks per build, newest first (for rotation) |
| Personal profile | `~/.tastemaker/profile.md` | Durable cross-project preferences |
| Cross-project history | `~/.tastemaker/history.json` | Recent builds' structure picks and hero copy across all projects, with outcomes |

**Precedence:** the current request > style lock > resolved decisions > profile. Pending-review entries guide review but never count as approval. The two `~/.tastemaker/` files live in the developer's home directory; mention the first time you create them, and respect the project's `.gitignore` for `.tastemaker/`.

## Decision log (`.tastemaker/decisions.log`)

One JSON object per line, append only - never rewrite history; append the newer decision.

```json
{"ts":"2026-09-14T12:40:00Z","surface":"homepage hero","status":"kept","axis":"structure","decision":"one promise, one short explanation, two actions, one product preview","reason":"developer preferred a clean first impression over a feature-dense hero","source":"user","promote":true}
{"ts":"2026-09-14T12:46:00Z","surface":"dashboard empty state","status":"pending-review","axis":"assets","decision":"quiet line illustration in the locked accent","reason":"keeps the shell calm without an asset-empty state","source":"agent-pending","promote":false}
```

- `status`: kept | rejected | pending-review. `axis`: palette | type | density | structure | motion | assets | copy | interaction | other. `source`: user | agent-pending.
- After each meaningful pass, ask **one concrete keep/reject question** ("keep this hero density, or try a quieter variant?"), and log the real answer.
- With nobody to answer (autonomous run), log `pending-review` - never fabricate approval.
- When a pending decision is later reviewed, append a new entry referencing it.
- Record at a useful grain ("compact table rows at 36px", not "looks nice").
- If a project already has a plain-text log, keep its style.
- When a `structure` or `copy` decision resolves, update the matching entry's `outcome` in `~/.tastemaker/history.json`.

## Profile (`~/.tastemaker/profile.md`)

Promote a decision only when it's resolved **and** durable: the developer says to carry it forward, it recurs in two or more resolved decisions, or it describes a reusable axis (density, motion feel, type taste, asset style, shape language, hierarchy, common rejects).

Never promote: pending decisions, one-off brand constraints, choices forced by a client or platform, fallbacks caused by missing assets or time pressure, or hesitant approvals.

```markdown
# Tastemaker profile
Updated: <date>

## Strong priors
- Density: <preference> (evidence: <project>, <date>, <decision>)

## Things to avoid
- <rejected pattern> (evidence: <project>, <date>)

## Open questions
- <preference needing one more resolved decision>
```

Use priors to avoid known rejects and start warm - not to narrow the creative range. On a fresh project, state the 1-3 priors you're applying. Remove an entry only when a newer resolved decision contradicts it.

## Build log (`.tastemaker/log.json`)

JSON array, newest first, trimmed to ~20 entries:

```json
[
  {"date":"2026-09-14","page":"landing","macrostructure":"Feature Stack","nav":"N2","hero":"H2","footer":"Ft1","knobs":"hero=split/left-bias/mockup; features=F1/irregular","brief":"observability SaaS"}
]
```

If built CSS carries a stamp but there's no log, infer an entry from the stamp.

## Cross-project history (`~/.tastemaker/history.json`)

The project log stops one project repeating itself; this stops *different* projects converging on the same "safe" shape and the same headline template. JSON array, newest first, trimmed to ~40:

```json
[
  {"id":"tracejam-2026-09-14","date":"2026-09-14","project":"tracejam","page":"landing","macrostructure":"Feature Stack","nav":"N2","hero":"H2","footer":"Ft1","headline":"Every failed retry, traced to the deploy that caused it","cta":"Trace your first incident","angle":"mechanism","outcome":"pending"}
]
```

Write the entry in the same pass as the project log and the CSS stamp, with `outcome: "pending"`; patch it to kept/rejected when the decision resolves.

**Reading it (by hand):**
- **Over-represented pick:** if a macrostructure, nav, hero, or footer appears in 3+ of the last 5 entries (60%+), flag it as a hot default. Keep it only if the brief genuinely calls for it, and say so.
- **Outcome tie-break:** once rotation leaves several legal candidates, prefer the one with a better kept/rejected record - but treat fewer than 4 resolved entries as no data. A high reject rate is a prompt to check *why* in the decision logs (bad fit, or poor execution), not a blacklist. Never use outcomes to justify repeating the last build's pick.
- **Copy:** compare the new headline and CTA to recent ones; a near-duplicate phrasing or the same sentence template across projects is a flag.

## Style lock (`.tastemaker/style-lock.md`)

The single source of truth once a style exists. Every later screen reads tokens from here instead of re-deriving them. Include only values actually derived - every line should be something another project might plausibly do differently.

```markdown
# Style lock - <project>
Established: <date>. Source: <reference images (list) | generated from mood | developer-specified>

## Palette
- Background / Surface / Primary / Accent / Border: #hex (role)
- Text primary: #hex - contrast vs background X.XX
- Text muted: #hex
- On-primary (button label): #hex - contrast vs Primary X.XX (never assume white)
- Dark mode: <single mode only | companion palette (author-time) | runtime toggle - both verified>

## Color contract
Floors: body/muted text on bg or surface 4.5 · label on any solid fill 4.5 · accent as text 4.5 · fill vs page 3.0 · accent as icon/highlight 3.0 · state-carrying border 3.0 (decorative hairlines exempt)
- Text-safe (≥4.5): <pairings>
- UI-safe (3.0-4.5): <pairings - large text, icons, state borders>
- Decorative (<3.0): <pairings that never carry text or sole state>
- Adjustments: <e.g. "Accent nudged #xxxxxx → #yyyyyy to clear UI-safe on Surface">

## Typography
- Display: <font> - <why> · Body: <font> · Scale: <ratio, base>
- (Non-Latin projects: one family across weights; record letter-spacing and word-break choices)

## Shape language
- Radius: <values and where> · Shadow: <flat | soft | hard> · Borders: <usage>

## Density & spacing
- Section padding tiers: <connective / standard / pivotal tokens> · Content card padding: <≥24px token> · Compact padding: <token> · Showcase card: <token>
- Overall density: <...> · Section separation: <tint | hairline | padding only - same at every boundary>

## Structure
- Macrostructure per page · Arc per page (beats → archetypes) · Shared chrome (nav + footer) · Body archetypes

## Reference intelligence
- Board: `.tastemaker/reference-board.md` (<viewed | inferred, not viewed>)
- Design read + dials · Foundation (design system / repo stack / custom lane) · Quality bar · Direction contract · Anti-references

## Taste memory
- Profile priors used · Last resolved decisions · Pending review · Promotions

## Navigation chrome (app shells only)
- Sidebar vs content background · Active item · Hover · Breadcrumbs · Row height and type size

## Mood descriptors
2-4 words for gut-checks, e.g. "quiet, confident, technical"

## Assets
- Anchor asset · Asset style · Illustration vs photography split · Illustration source · Logo (path, how produced)

## Motion
- Feel · Curves · Durations · Entrance distance · Screen tracks · Frequency rules · Reduced motion · Verified (date/method or pending)

## Do not
- <project-specific rejects, e.g. "no gradients - rejected twice">
```

## Handoff

At the end of every design task, say plainly whether the decision log, style lock, build log, history, and profile changed - and why the profile did, if it did.
