# Fonts and features

## Typeface categories

| Category | Traits | Use for |
| --- | --- | --- |
| Serif | Stroke endings guide the eye along a line | Long passages, editorial |
| Sans-serif | Even shapes, crisp at small sizes | Default for most interfaces |
| Monospace | Equal-width glyphs; columns align | Code, tables, tabular data |
| Display | Drawn for large sizes | Headlines, hero text |
| Script | Handwriting | Rare decorative moments |

A family's "Display" variant (e.g. SF Pro Display vs SF Pro Text) is tuned for large sizes - use the variant that matches the size you're setting.

## Choosing and changing faces

- Fewer is better; rarely more than three. Marketing can be more expressive than apps.
- Pair for contrast, never near-identical sans-serifs.
- Thin weights (100-300) only at 28px+ display sizes, checked against the background.
- Reviews never require a new typeface. If a change is requested: a system stack gives a native Apple feel; a commercial face is a brand decision and still needs fallbacks.

```css
html { font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif; }
html { font-family: "Helvetica Now", "Helvetica Neue", Arial, sans-serif; }
```

## Formats

| Format | Notes |
| --- | --- |
| `.woff2` | Brotli-compressed, broadly supported - use on the web |
| `.woff` | Older compression; very old browsers only |
| `.ttf` / `.otf` | Uncompressed desktop formats |

## Anatomy

x-height (lowercase x), cap height, baseline, ascender, descender. Differences in these are why two fonts at the same `font-size` look different sizes - a larger x-height reads bigger.

## Static vs variable

- **Static:** one weight/style per file.
- **Variable:** a continuous range in one file (`font-weight: 589` works).

Not automatically better: at one or two weights static files can be smaller; with several weights, optical sizes, or custom axes, variable usually wins.

## Synthesis

Requesting a weight or style the family lacks makes the browser fake it. `font-synthesis: none` disables all synthesized forms at once and can erase distinctions if the real face fails to load - verify the whole fallback stack first, or use a longhand (`font-synthesis-weight`, `font-synthesis-style`) to disable only the unwanted mode. Keep synthesis on for body and UI text unless a verified setup supplies every form.

## Axes

| Axis | Tag | Controls |
| --- | --- | --- |
| Weight | `wght` | Stroke thickness |
| Optical size | `opsz` | Detail and spacing tuned to size |
| Width | `wdth` | Glyph width |
| Slant | `slnt` | Slant angle |
| Custom | e.g. `GRAD` | Whatever the designer built |

A font supports only its designed axes (Inter's variable file: `wght` and `opsz`). Many families still ship optical sizes as separate files (a "Text" cut sturdier for reading, a "Display" cut finer).

```css
/* Good */
.heading { font-weight: 650; font-optical-sizing: auto; }
.heading-grade { font-variation-settings: "GRAD" 80; } /* no property exists */

/* Bad: silently ignored by a non-variable fallback */
.heading { font-variation-settings: "wght" 650; }
```

## OpenType features

Work on static and variable fonts alike, if the font includes them.

| Tag | Feature |
| --- | --- |
| `tnum` | Tabular (equal-width) digits |
| `zero` | Slashed zero |
| `liga` | Ligatures |
| `ss01`-`ss20` | Stylistic sets |
| `cv01`-`cv99` | Character variants |

```css
.price { font-variant-numeric: tabular-nums; }
.id { font-variant-numeric: slashed-zero; }
.logo { font-feature-settings: "ss01" 1; } /* no property exists */
```

- Real small caps: `font-variant-caps: small-caps`. Real super/subscripts: `font-variant-position`. Both need the glyphs in the font.
- Stylistic set and character variant slots mean different things per font - check its documentation (in Inter, `ss01` gives open digits and `cv11` a single-story a).
