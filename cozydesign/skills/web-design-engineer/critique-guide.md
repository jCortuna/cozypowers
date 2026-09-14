# Critique guide

Use for Step 7: when asked to review, rate, or score a design, or as a self-check before delivery. Be specific and actionable, in design language. Critique the work, never the person.

## Rubrics

### 1. Philosophy alignment - does every detail trace back to the chosen direction?

| Score | Standard |
| --- | --- |
| 9-10 | Every detail embodies the direction; nothing feels borrowed |
| 7-8 | Right direction, signature traits land, one or two drifts |
| 5-6 | Intent visible but diluted by foreign elements (a "minimal" page with six cards per row) |
| 3-4 | Surface mimicry without the underlying values |
| 1-2 | No relationship to any stated direction |

Look for: the direction's signature moves actually present; color, type, layout, and motion agreeing; self-contradictions (quiet minimalism crammed full).

### 2. Visual hierarchy - does the eye go where intended?

| Score | Standard |
| --- | --- |
| 9-10 | Effortless reading path |
| 7-8 | Clear primary/secondary; a couple of muddy spots |
| 5-6 | Title vs body clear, middle levels collapse |
| 3-4 | Flat; no entry point |
| 1-2 | Chaotic |

Look for: heading/body ratio of at least 2.5x (4-6x for heroes); 3-4 distinct levels via size, weight, color; whitespace steering attention; the **squint test** - blur your eyes and check the hierarchy survives.

### 3. Craft quality - pixel-level execution

| Score | Standard |
| --- | --- |
| 9-10 | Flawless alignment, spacing, color |
| 7-8 | Refined; one or two small slips |
| 5-6 | Roughly aligned; spacing inconsistent, color unsystematic |
| 3-4 | Obvious misalignment, chaotic spacing, too many colors |
| 1-2 | Reads as a draft |

Look for: a spacing scale (e.g. 8 / 16 / 24 / 32 / 48 / 64) applied consistently to like elements; about four colors (primary, accent, neutral scale, one emphasis); at most two families (display + body); precise edge alignment.

### 4. Functionality - does each element earn its place?

| Score | Standard |
| --- | --- |
| 9-10 | Everything serves a goal |
| 7-8 | Function-led with a little removable decoration |
| 5-6 | Usable, but decoration competes |
| 3-4 | Form over function; information is hard to find |
| 1-2 | Decoration drowns the message |

Look for: the deletion test; CTA and key information in the most prominent spot; things added "because they looked good"; density suited to the medium (slides sparse, documents denser, landing pages conversion-led).

### 5. Originality - fresh while coherent

| Score | Standard |
| --- | --- |
| 9-10 | A unique expression within the chosen philosophy |
| 7-8 | Has its own ideas |
| 5-6 | Template execution |
| 3-4 | Leans on clichés (gradient orbs for "AI", chat bubbles for "conversation") |
| 1-2 | Stock assembly |

Look for: absence of AI tells; at least one "unexpected but right" decision.

## Weighting by output type

| Output | Weight highest | Secondary | Can relax |
| --- | --- | --- | --- |
| Landing / marketing | Functionality, hierarchy | Originality | Nothing - must be all-round |
| Dashboard / data product | Functionality, craft | Hierarchy | Originality |
| Slide deck | Hierarchy, functionality | Craft | Originality |
| Mobile prototype | Functionality, craft | Hierarchy | Philosophy |
| Launch film / brand moment | Originality, hierarchy | Philosophy | Functionality |
| Editorial / portfolio | Originality, philosophy | Hierarchy | Functionality |
| Docs site | Functionality, hierarchy | Craft | Originality |
| User-testing prototype | Functionality, hierarchy | Craft | Originality |

## Top 10 issues

1. **AI-tech clichés** (orbs, digital rain, circuit boards, robot faces) → use abstract metaphors instead of literal symbols.
2. **Weak type scale** (heading < 2.5x body) → heading at least 3x body (16px body → 48-64px heading; ~6x for heroes).
3. **Too many colors** (5+ without structure) → one primary, one secondary, one accent, plus grays; everything else must justify itself.
4. **Ad-hoc spacing** → one scale, e.g. {8, 16, 24, 32, 48, 64, 96}.
5. **No breathing room** → roughly 40%+ whitespace (60%+ for minimal work).
6. **Too many fonts** (3+) → two families max; get variety from weight and size.
7. **Mixed alignment** → pick one (usually left); center only for heroes and pull-quotes.
8. **Decoration over content** → deletion test on every pattern, gradient, and shadow.
9. **Neon on navy-black** → a distinctive palette; if dark is required, a non-default base (warm deep gray, tinted near-black).
10. **Density wrong for the medium** → slides: one idea per page; covers: one focal point; infographics: overview then detail; documents: dense but navigable.

## Template

```markdown
## Design critique

**Overall: X.X / 10** - Excellent (8+) / Good (6-7.9) / Needs work (4-5.9) / Failing (<4)

**By dimension**
- Philosophy alignment: X/10 - reason
- Visual hierarchy: X/10 - reason
- Craft quality: X/10 - reason
- Functionality: X/10 - reason
- Originality: X/10 - reason

### Keep
- Specific strengths in design language ("muted terracotta on warm off-white reads confident and editorial", not "nice colors")

### Fix (most severe first)
**1. Issue** - Critical / Important / Polish
- Now: what it looks like
- Why: the principle it breaks
- Fix: a concrete change with values ("heading 32px → 56px", not "bigger headings")

### Quick wins (if there are only five minutes)
- [ ] ...
- [ ] ...
- [ ] ...
```

## Critique anti-patterns

- **Vague taste claims.** Not "the colors are off" but "the accent at oklch(0.65 0.25 25) competes with the primary; drop chroma to ~0.18 so it recedes."
- **Unspecific praise.** Say what works and why.
- **Mixed severities.** Order critical → important → polish.
- **More than seven fixes.** Group related ones ("five spacing inconsistencies").
- **Ungrounded fixes.** Each fix names the principle behind it.
- **Judging the designer.** "This element doesn't earn its place" - not "you didn't think this through."
