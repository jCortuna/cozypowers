# Scale and spacing

## Units

`px` fixed; `em` scales with the current font size; `rem` with the root; `%` on `font-size` behaves like `em`.

## Type scale

```css
:root {
  --text-sm: 0.875rem;
  --text-base: 1rem;
  --text-lg: 1.125rem;
  --text-xl: 1.5rem;
  --text-2xl: 2rem;
}
```

Adopt an existing scale (Tailwind's `text-xs`...`text-9xl`, which pairs sizes with line heights) or define one. A **role-based** scale makes each role one decision instead of three. Starting point for product UI:

| Role | Size | Line-height | Weight |
| --- | --- | --- | --- |
| Display | 2.25rem (36px) | 1.1 | 600 |
| Title | 1.5rem (24px) | 1.2 | 600 |
| Heading | 1.125rem (18px) | 1.3 | 600 |
| Body | 1rem (16px) | 1.5 | 400 |
| Caption | 0.8125rem (13px) | 1.4 | 400 |

Emphasis inside a role is one weight step (400 → 500), not a size change.

## Heading hierarchy

```css
h1 { font-size: var(--text-2xl); }
h2 { font-size: var(--text-xl); }
h3 { font-size: var(--text-lg); }
```

In Tailwind, centralize the mapping in a component or `@layer base` rather than repeating it inline. When reviewing, compare computed heading sizes within each section - a child more prominent than its parent breaks hierarchy. A heading is never smaller than body text unless it's a deliberate overline label.

## Kerning and letter-spacing

Kerning adjusts specific pairs (AV, Ye) and is automatic - disable only deliberately (`font-kerning: none`). `letter-spacing` adds uniform space:

```css
.display-heading { letter-spacing: -0.02em; }
.uppercase-label { text-transform: uppercase; letter-spacing: 0.05em; }
```

## Line-height

| Text | Value |
| --- | --- |
| Headings | ~1.1 |
| Body | 1.5-1.6 |

Tailwind's `leading-snug`, `leading-normal`, `leading-relaxed` rarely need overriding. A cramped paragraph costs more than a taller row.

```css
.card-description { line-height: 1.1; } /* bad: wraps to 3 lines at heading leading */
.card-description { line-height: 1.4; } /* good */
```

## Measure

Aim for 60-75 characters per line in long-form text. `65ch` measures directly; at 16px body this is roughly 560-680px, so Tailwind `max-w-xl` (576px) or `max-w-2xl` (672px) fit. Recheck if the body size changes.

## Trimming with text-box

Fonts reserve space above and below glyphs, which is why text sits low in buttons and badges. `text-box` trims it:

| Keyword | Trims at |
| --- | --- |
| `cap` | Cap height (top) |
| `alphabetic` | Baseline (bottom) |
| `text` | The font's text edge, keeping descender room |

```css
.badge { text-box: trim-both cap alphabetic; }
.heading { text-box: trim-start cap; }
.label { text-box: trim-end alphabetic; }
```

Chromium 133+ and Safari 18.2+, not yet Firefox - progressive enhancement only.

## Wrapping, truncation, alignment

| Property | Use |
| --- | --- |
| `text-wrap: balance` | Even lines - headings |
| `text-wrap: pretty` | No lone last word - descriptions |
| `overflow-wrap: break-word` | Long words, links, IDs |
| `white-space: nowrap` | Labels and badges |

Skip balance/pretty on long-form text (browsers ignore balance past a few lines, and evening paragraphs wastes space). `justify` belongs only in specific editorial layouts.

Truncate: single line with ellipsis + hidden overflow + nowrap; multi-line with `line-clamp`. Keep the full value reachable when it matters.

## Punctuation

| Instead of | Use |
| --- | --- |
| Straight quotes in prose | Curly quotes (straight stays in code) |
| Hyphen in ranges | En dash (2010–2020) |
| Double hyphen for an aside | Em dash character |
| Three periods | Ellipsis character (…) |
| Space in "16 px" | `&nbsp;` |
| Uncontrolled breaks in long words | `&shy;` |

## Mixed direction

- Short snippets (one or two lines) follow the UI's direction; paragraphs of three or more lines align to their own script (`text-align: start` with correct `lang`/`dir` on the element).
- Digits never reverse; let the Unicode bidi algorithm work and isolate mixed values with `<bdi>`.
