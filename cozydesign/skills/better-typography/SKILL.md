---
name: better-typography
description: Make typography feel right - font formats and loading, fewer faces and weights, a semantic type scale, heading hierarchy, line-height and letter-spacing by role, measure, deliberate wrapping, tabular numbers, truncation, smart punctuation, underlines, iOS input zoom, size floors, font smoothing, and bidi text. Use when setting or reviewing type, when text "looks off", wraps badly, shifts as numbers change, or zooms on iOS, and as the typography pass inside better-interface reviews.
---

# Better Typography

Typography is mostly restraint: a sensible scale, comfortable spacing, enough contrast. A label, a table cell, a marketing headline, and an article paragraph don't share one set of rules.

When reviewing, look at the **rendered** page - bad wrapping, widows, and truncation only appear at real content lengths.

Write fixes in the project's styling system using the exact values below. [css-cheat-sheet.md](css-cheat-sheet.md) maps each declaration to Tailwind.

The words belong to **better-writing**; heading semantics to **better-accessibility**; spatial RTL and logical properties to **better-layout**; contrast measurement to **better-colors**. This skill owns how text renders, wraps, and behaves in mixed-direction content.

## Principles

### Serve the right format

`.woff2` on the web (Brotli, broad support); `.woff` only as an ancient-browser fallback; `.ttf`/`.otf` are desktop formats. Loading strategy is the project's concern.

### Properties over raw tags

Use `font-weight: 650` not `font-variation-settings: "wght" 650`; `font-optical-sizing: auto` not `"opsz"`; `font-variant-numeric: tabular-nums` not `"tnum" 1`. Properties survive a non-variable fallback. Raw tags only for custom axes (`"GRAD" 80`) and niche features (`"ss01" 1`). → [fonts-and-features.md](fonts-and-features.md)

### Load the faces you use

Browsers synthesize missing weights and styles, distorting the face - load what the design uses. `font-synthesis: none` erases emphasis rather than reporting it; set it only after verifying every bold, italic, small-cap, and super/subscript form stays distinct across the fallback stack (or use the specific longhand).

### Fewer fonts, sizes, weights

Rarely more than three fonts. Pair for contrast (serif headline over sans body), not near-duplicates. Below 18px, weight 400 or heavier; weights under 300 are display-only at 28px+. Never introduce a new or paid typeface just to satisfy a review - use the product's type system unless a change is requested.

### A type scale with semantic names

A small set of sizes, deviated from rarely. Solo, `text-sm` is fine with clear usage rules; on a team, name by role (`text-body-sm`). → [scale-and-spacing.md](scale-and-spacing.md)

### Headings descend with level

Map heading levels to descending scale steps so a child never overpowers its parent. Deep levels may share a size if weight or spacing keeps them distinct. Choose the element for structure, then size it in CSS.

### Line-height by role

Headings ~1.1; body 1.5-1.6; unitless so it scales. Anything wrapping to 3+ lines needs at least 1.4, even in a tight row.

### Letter-spacing by size

Large headings: slightly negative (e.g. -0.02em). Small uppercase labels: slightly positive (e.g. 0.05em). Body text: neither.

### Cap the measure

Long-form text at ~60-75 characters per line. Any unit works (`65ch`, or roughly 560-680px at 16px body) as long as a cap exists.

### Wrap deliberately

- `text-wrap: balance` - headings.
- `text-wrap: pretty` - descriptions (no lone last word).
- `overflow-wrap: break-word` - long words, links, IDs that could escape.
- `white-space: nowrap` - labels and badges.

Skip balance/pretty on long-form text. Don't justify interface text.

### Tabular numbers on changing values

Timers, counters, prices: `font-variant-numeric: tabular-nums`, or the layout jitters as digits change.

### Truncate without losing content

One line: `text-overflow: ellipsis` + `overflow: hidden` + `white-space: nowrap`. Several: `line-clamp`. When the hidden text matters, keep it reachable (tooltip or expanded view).

### Natural copy, CSS presentation

Store text in natural case; use `text-transform`. Render smart punctuation: curly quotes in prose (straight in code), en dash for ranges (2010–2020), the single ellipsis character, `&nbsp;` to keep "16 px" together, `&shy;` for permitted breaks.

### Underlines from the font

`text-underline-position: from-font` and `text-decoration-thickness: from-font`, or tune `text-underline-offset`, thickness, and `text-decoration-skip-ink`. A dotted underline hints at extra information (abbreviations, defined terms). Only underline *color* animates reliably - build a separate element for anything else.

### 16px inputs on mobile

iOS Safari zooms the page for inputs under 16px. Two fixes that look different - ask which the design wants: size up on mobile (`text-base sm:text-sm`), or keep 16px and render smaller with `transform: scale()` plus compensating width and line-height. → [details.md](details.md)

### Size and contrast floors

Long-form body starts at 16px; deviate only for a nameable reason (small-running face, narrow measure, dense pro tool). UI text: ~14px for inputs and menus, 13px captions, rarely below 12px. Low contrast → better-colors measures, better-accessibility classifies; don't change colors unasked.

### Font smoothing once, at the root

`-webkit-font-smoothing: antialiased; -moz-osx-font-smoothing: grayscale;` on the root layout (Tailwind `antialiased`), never per component.

### Language and direction

Set `lang` (pronunciation, quotes, hyphenation) and `dir` where direction changes. Never reverse digits; isolate mixed-direction values with `<bdi>`. Paragraphs of three or more lines align to their own script even inside an opposite-direction UI.

### Keep text selectable

Selectable by default; `::selection` can carry brand if it stays legible. `user-select: none` only on drag or gesture surfaces where selection interferes.

## Before you finish

| Mistake | Fix |
| --- | --- |
| Synthesized face differs from design | Load the real face; disable only verified synthesis modes |
| Child heading overpowers its parent | Descending scale steps per section |
| Heading element chosen for default size | Semantics first, size in CSS |
| Orphan on a paragraph's last line | `text-wrap: pretty` |
| Lopsided two-line heading | `text-wrap: balance` |
| Justified interface text | `text-align: start` |
| Underline slicing descenders | `text-decoration-skip-ink: auto`, from-font metrics |
| Mixed-direction value misordered | Correct `lang`/`dir`; wrap in `<bdi>` |
| Selection disabled across the app | Restore; suppress only on drag/gesture conflicts |
| Extra-info term with no cue | Dotted underline |
| Thin weight on 14px UI text | 400+ below 18px |
| `leading-none` on a 3-line description | ≥1.4 |

## Reporting (standalone)

**Severity.** HIGH: unreadable text, or truncation with no way to recover the content. MEDIUM: breaks the type system or heading hierarchy. LOW: isolated polish.

**Verification.** Without a browser: computed size/weight per heading level (descending), declared line-height and measure, truncation against realistic string lengths. With one: resize to catch wrapping, widows, truncation at real lengths. Unrun checks are **Not verified**.

**Format.** Grouped by principle, severity-ordered, one row per root cause with all locations:

| Severity | Location | Before | After | Why |
| --- | --- | --- | --- | --- |

End with **Block** (any HIGH) or **Approve**. Nothing found → "No actionable typography findings", plus verification.
