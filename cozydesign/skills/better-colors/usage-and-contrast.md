# Color usage, formats, and contrast

## Notation

| Notation | Good for | Weakness |
| --- | --- | --- |
| Hex | Universal, compact, what design tools export | Opaque channels |
| `rgb()` | Same reach, readable alpha | Channels don't map to design intent |
| `hsl()` | Looks like design controls | Non-perceptual lightness, drifting hue |
| `oklch()` | Perceptual lightness, stable hue, predictable ramps | Baseline 2023; very old targets need fallbacks |

Notation isn't a defect - match the project. For a new system, `oklch(L C H)` (lightness 0-1, chroma 0-~0.4, hue 0-360; alpha after a slash: `oklch(L C H / a)`).

**Converting** only when asked, when a migration is in scope, or when the value is a straggler in a standardizing project. Change values only: leave keywords (`currentColor`, `inherit`, `transparent`), leave gradient interpolation methods (convert the stops), leave third-party configs, keep comments and formatting. Bulk conversion is a migration (every color shifts by rounding), never incidental cleanup.

```css
color: #3b82f6;                          →  color: oklch(0.623 0.188 259.815);
border: 1px solid rgba(0, 0, 0, 0.1);    →  border: 1px solid oklch(0 0 0 / 0.1);
```

## Gamut

Display P3 contains all of sRGB plus ~50% more, relevant only for the most vivid colors. Colors beyond a display's gamut are **clipped**, flattening neighboring ramp steps into one. Maximum vividness varies by hue and lightness (cyans far lower than reds and purples). Fix by reducing vividness while holding hue and lightness. Generate ramps against sRGB and layer P3 on top:

```css
.accent { background: #3b82f6; }
@media (color-gamut: p3) {
  .accent { background: oklch(0.62 0.24 259); }
}
```

sRGB first, P3 override second. A P3 color with no fallback doesn't degrade - it fails (HIGH). For browser matrices older than `oklch()`, layer with `@supports (color: oklch(0 0 0))` instead - but on a modern baseline that's dead weight.

## Modern CSS

- `color-mix(in oklab, var(--color-accent-solid) 15%, white)` - derived tints for states; keep generated values out of the token layer.
- Relative color syntax - `oklch(from var(--color-accent-solid) calc(l - 0.1) c h)`; powerful but unreadable when chained.
- `light-dark()` - both appearances in one declaration.

All resolve at render time, so measure the rendered result.

## One color, one meaning

```css
/* Bad: accent means both "link" and "decorative heading" */
a { color: #3b82f6; }
.section-title { color: #4f8ef7; }

/* Good */
a { color: var(--color-accent-text); }
.section-title { color: var(--color-text-primary); }
```

Near-miss hues read as the same color. And the rule runs both ways: a meaning must not appear without its color.

## Tokens in their role

```css
.caption { color: var(--color-border); }         /* bad: border token as text */
.tag { background: var(--color-text-secondary); } /* bad: text token as background */
```

## One filled action

```html
<!-- Good -->
<button class="bg-accent-solid text-white">Save</button>
<button class="text-neutral-700">Cancel</button>
<!-- Bad: everything colored, nothing primary -->
```

Selected states (active tab, checked segment) may use accent on glyph and label - that's state, not emphasis.

## Gradients

```css
background: linear-gradient(#3b82f6, #ec4899);            /* sRGB: muted, darker midpoint */
background: linear-gradient(in oklab, #3b82f6, #ec4899);  /* even brightness - best default */
background: linear-gradient(in oklch, #3b82f6, #ec4899);  /* vivid, arcs through intermediate hues */
```

- oklab and sRGB are rectangular (straight line through the space); oklch is polar (travels the hue angle), which keeps saturation but can introduce hues nobody asked for (blue→pink routes through purple).
- **Gray dead zone:** opposite hues in a rectangular space pass near neutral. Use a polar space or add a middle stop.
- Direction in polar spaces: `in oklch shorter hue` (usual) or `longer hue` (sweeps the spectrum).
- **Banding** on large low-contrast gradients: widen contrast, shrink the area, or add subtle noise.
- Keep text off gradients; if unavoidable, measure the worst region or add a scrim.

## Culture

| Color | Common Western reading | Elsewhere |
| --- | --- | --- |
| Red | Danger, loss | Luck, prosperity; gains in Chinese financial UIs |
| Green | Success, gains | Losses in Chinese financial UIs |
| White | Purity | Mourning in parts of East Asia |
| Gold | Premium | Religious significance in some regions |

Where color is load-bearing (finance, status, alerts) in multiple markets, make meanings like gain/loss per-locale tokens.

## Light, dark, increased contrast

```css
:root { --color-accent-solid: #3b82f6; }
@media (prefers-color-scheme: dark) { :root { --color-accent-solid: #60a5fa; } }
@media (prefers-contrast: more)     { :root { --color-accent-solid: #1d4ed8; } }
```

Increased contrast should widen the foreground/background gap by at least ~15 points of perceived lightness, then be re-verified (APCA preferred: Lc 90 body, Lc 75 non-body).

## Contrast

Measure foreground (text, icon, UI element) against the background it **actually renders on** - usually the nearest ancestor that paints. **Report, don't repaint**: give the pair, the measured value, the missed threshold; fix only on request.

### APCA (recommended for design decisions)

| Content | Minimum | Preferred |
| --- | --- | --- |
| Body text | Lc 75 | Lc 90 |
| Non-body text (labels, headlines) | Lc 60 | Lc 75 |
| Large text (≥36px) | Lc 45 | Lc 60 |
| UI components | Lc 30 | - |

Lc 30 is also the minimum for disabled and placeholder text; Lc 15 is the floor for a non-text element to be discernible. Lc is signed (positive = dark on light); compare absolute values.

### WCAG 2 (legal conformance)

| Content | AA | AAA |
| --- | --- | --- |
| Normal text (<24px, or <18.5px bold) | 4.5:1 | 7:1 |
| Large text (≥24px, or ≥18.5px bold) | 3:1 | 4.5:1 |
| UI components and graphics | 3:1 | - |

When WCAG conformance must be claimed, WCAG is the gate and APCA the tiebreaker above it.

### Fixing a failing pair (on request)

Change **lightness** - the channel contrast responds to; hue changes barely move it. Move the foreground away from the background in perceived lightness, hold hue and saturation, remeasure.

```css
color: #7d93b0; background: #eef2f7;  /* ≈ Lc 50 - fails */
color: #2b3a4f; background: #eef2f7;  /* ≈ Lc 90 - same hue, darker */
```

- Mid-lightness backgrounds cap what's achievable: near 75% perceived lightness even black text reaches only ~Lc 60. Body text needs a background near an extreme - change the background.
- Pushing lightness can exit the gamut; reduce saturation to stay renderable.

### Approximations (then measure)

- Body text at |Lc| ≥ 75: on a light background (>~90% perceived lightness) use foreground below ~35%; on a dark background (<~25%) use foreground above ~90%. Asymmetric because APCA is polarity-aware - a pair passing in light can fail mirrored.
- Light or dark text? The crossover is ~73% perceived lightness. Between ~60% and 73% the background *looks* light, yet white text still measures better.

### What to check

- Every pair in every appearance.
- Translucent surfaces (backdrop-filter headers, overlays) against the lightest and darkest content beneath - or make them opaque enough.
- Computed colors (`color-mix()`, relative syntax, opacity modifiers) as rendered.
- Text over images: worst region, or a guaranteed scrim.
