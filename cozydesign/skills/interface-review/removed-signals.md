# Removed signals

What to look for on the `-` side of a hunk, and which skill judges it. A row is a **lead, never a finding**: route the removal to its owner and report only what that skill confirms got worse.

| Removed from the `-` side | Owner | Check |
| --- | --- | --- |
| `aria-label`, `aria-labelledby`, `aria-describedby`, `aria-live`, `role=` | better-accessibility | Lost accessible name, description, or announcement |
| `alt=`, `<label`, `for=`, `scope=` | better-accessibility | Image, field, or cell lost its programmatic association |
| `<button>`, `<a>`, `<nav>`, `<main>`, `<ul>` replaced by `div`/`span` | better-accessibility | Keyboard and assistive-tech behavior traded for styling |
| `:focus-visible`, `:focus`, `outline`, `tabindex` | better-accessibility | Focus indicator lost, or element left the tab order |
| `prefers-reduced-motion`, `prefers-contrast` | better-accessibility | Motion or contrast now ignores system preference |
| Logical properties swapped for `left`/`right` | better-layout | Direction-aware layout dropped |
| `lang=`, `dir=` | better-typography | Language or direction metadata dropped |
| `text-wrap`, `line-clamp`, `overflow-wrap`, `tabular-nums`, `font-feature-settings` | better-typography | Wrapping, rendering, or numeral alignment changed |
| Color token swapped for a literal, or for a lighter token | better-colors | Rendered contrast may now fail - measure it |
| User-facing string deleted or shortened | better-writing | Label, error, or empty state lost information |

## Equivalent replacements (clear the signal)

Check these before routing, or refactors fill the report as fake regressions:

- `aria-label` replaced by `aria-labelledby` pointing at visible text.
- An explicit role dropped because the element became its native equivalent (`div role="button"` → `<button>`).
- `outline` replaced by a `box-shadow` ring that still meets the focus-indicator rule.
- `tabindex="0"` dropped from an element that is now natively focusable.
- A color literal replaced by a token measuring the same rendered pair.
- A physical property replaced by its logical counterpart (that's the fix).
- A string moved into the translation catalog rather than deleted.

## Searching the removed side

Restrict to deleted lines so additions don't mask removals - e.g. a zero-context diff against the base, filtered to lines starting with a single `-`, then grepped for `aria-|role=|alt=|focus|tabindex|prefers-`. Then read the surrounding hunk before deciding: a removed attribute means nothing without the element it came from, and zero-context output deliberately hides that.
