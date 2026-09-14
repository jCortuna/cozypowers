# Typography CSS cheat sheet

Declarations covered by this skill with Tailwind 4 equivalents (arbitrary-value form where no utility exists). Use the CSS column in plain CSS / CSS Modules / CSS-in-JS projects, the Tailwind column in Tailwind projects.

## Font

| Declaration | Does | Tailwind |
| --- | --- | --- |
| `font-family: sans-serif / serif / monospace` | Family | `font-sans` / `font-serif` / `font-mono` |
| `font-size` | Size from scale | `text-*` |
| `font-weight` | 1-1000 | `font-*` |
| `font-style: italic` | Italic | `italic` |
| `-webkit-font-smoothing` + `-moz-osx-font-smoothing` | macOS smoothing, root only | `antialiased` |
| `font-synthesis: none` | Disable synthesis (verify first) | `[font-synthesis:none]` |
| `font-feature-settings` | OpenType features | `[font-feature-settings:"ss01"]` |
| `font-variation-settings` | Custom axes | `[font-variation-settings:"GRAD"_80]` |
| `font-optical-sizing` | Per-size detail | `[font-optical-sizing:auto]` |
| `font-variant-caps` | Real small caps | `[font-variant-caps:small-caps]` |
| `font-variant-position` | Real super/subscript | `[font-variant-position:super]` |
| `font-variant-numeric: tabular-nums` | Equal-width digits | `tabular-nums` |
| `font-variant-numeric: slashed-zero` | 0 vs O | `slashed-zero` |

## Spacing and layout

| Declaration | Does | Tailwind |
| --- | --- | --- |
| `letter-spacing` | Tracking | `tracking-*` |
| `line-height` | Leading | `leading-*` |
| `font-kerning` | Kerning on/off | `[font-kerning:none]` |
| `text-box: trim-both` | Trim glyph box space | `[text-box:trim-both_cap_alphabetic]` |
| `max-width` on text | ~60-75 chars/line | `max-w-xl` / `max-w-2xl` / `max-w-[65ch]` |
| `text-align` | Line alignment | `text-start` / `text-center` |

## Wrapping and overflow

| Declaration | Does | Tailwind |
| --- | --- | --- |
| `text-wrap: balance` | Even heading lines | `text-balance` |
| `text-wrap: pretty` | Avoid orphans | `text-pretty` |
| `text-overflow: ellipsis` (+ hidden, nowrap) | Single-line truncation | `truncate` |
| `line-clamp` | Clamp to N lines | `line-clamp-*` |
| `overflow-wrap: break-word` | Break long strings | `break-words` |
| `white-space: nowrap` | No wrapping | `whitespace-nowrap` |
| `text-transform` | Casing | `uppercase` / `capitalize` |

## Decoration and interaction

| Declaration | Does | Tailwind |
| --- | --- | --- |
| `text-decoration-line: underline` | Underline | `underline` |
| `text-decoration-color` | Underline color | `decoration-*` |
| `text-decoration-thickness` | Thickness | `decoration-1` / `decoration-2` / `decoration-from-font` |
| `text-underline-offset` | Offset | `underline-offset-*` |
| `text-underline-position: from-font` | Font-defined position | `[text-underline-position:from-font]` |
| `text-decoration-style` | Dotted/dashed/wavy | `decoration-dotted` / `decoration-wavy` |
| `text-decoration-skip-ink` | Gaps at descenders | `[text-decoration-skip-ink:auto]` |
| `caret-color` | Cursor tint | `caret-*` |
| `user-select: none` | Only for drag/gesture conflicts | `select-none` |
| `text-shadow` | Glyph shadow | `text-shadow-*` |
| `-webkit-text-stroke` | Glyph outline | `[-webkit-text-stroke:1px_black]` |
| `background-clip: text` | Background clipped to glyphs | `bg-clip-text` |
| `initial-letter` | Drop cap size | `[initial-letter:3]` |
