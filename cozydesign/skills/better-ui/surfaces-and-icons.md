# Surfaces and icons

## Concentric radius

`outerRadius = innerRadius + padding`

```css
/* Good */
.card { border-radius: 20px; padding: 8px; }   /* 12 + 8 */
.card-inner { border-radius: 12px; }

/* Bad: same radius on both */
.card { border-radius: 12px; padding: 8px; }
.card-inner { border-radius: 12px; }
```

Tailwind: `rounded-2xl p-2` (16px, 8px padding) around `rounded-lg` (8px). Matters most for closely nested surfaces with an even visible inset. Beyond ~24px padding, treat layers as separate surfaces with independent radii. Keep an established token where layers are independent or padding is deliberately asymmetric.

## Optical alignment

**Text + icon buttons.** Symmetric padding makes the icon side look heavy. Start with icon-side padding = text-side padding − 2px:

```css
.button-with-icon { padding-inline-start: 16px; padding-inline-end: 14px; } /* trailing icon */
```

Tailwind: `ps-4 pe-3.5`.

**Play triangles.** The geometric center isn't the visual center - shift the glyph right (e.g. `translateX(2px)`; a physical correction to the glyph).

**Asymmetric glyphs** (stars, arrows, carets). Best: fix the SVG's viewBox or path so components need no compensation. Fallback: a 1px translate on a wrapper.

## Shadows instead of depth borders

For buttons, cards, and containers whose border only suggests depth. Transparent shadows adapt to any background (images, mixed surfaces) where a fixed border color can't. **Never** for dividers (`border-t`, `border-b`, side borders) or layout separation.

Light mode - a 1px ring, a lift, an ambient layer:

```css
:root {
  --shadow-border:
    0 0 0 1px oklch(0 0 0 / 0.06),
    0 1px 2px -1px oklch(0 0 0 / 0.06),
    0 2px 4px 0 oklch(0 0 0 / 0.04);
  --shadow-border-hover:
    0 0 0 1px oklch(0 0 0 / 0.08),
    0 1px 2px -1px oklch(0 0 0 / 0.08),
    0 2px 4px 0 oklch(0 0 0 / 0.06);
}
```

Dark mode - depth shadows vanish on dark grounds, so a single white ring (via whatever theme mechanism the project uses):

```css
--shadow-border: 0 0 0 1px oklch(1 0 0 / 0.08);
--shadow-border-hover: 0 0 0 1px oklch(1 0 0 / 0.13);
```

```css
.card {
  box-shadow: var(--shadow-border);
  transition-property: box-shadow;
  transition-duration: 150ms;
  transition-timing-function: ease-out;
}
.card:hover { box-shadow: var(--shadow-border-hover); }
```

| Shadows | Borders |
| --- | --- |
| Cards and containers with depth | Dividers between list items |
| Bordered-style buttons | Table cell boundaries |
| Elevated elements (dropdowns, modals) | Form input outlines |
| Elements over varied backgrounds | Hairline separators in dense UI |
| Hover/focus lift | |

## Image outlines

```css
img { outline: 1px solid oklch(0 0 0 / 0.1); outline-offset: -1px; }          /* light */
img { outline: 1px solid oklch(1 0 0 / 0.1); outline-offset: -1px; }          /* dark */
```

Tailwind: `outline outline-1 -outline-offset-1 outline-black/10 dark:outline-white/10` - specifically black/white, never `outline-slate-*`, `zinc-*`, `neutral-*`, a palette near-black like `#111827`, or the accent/ink color. Outline (not border) adds no layout size, and the -1px offset hugs the corner radius.

## Icon stroke vs text weight

| Adjacent text | Stroke (24px grid) |
| --- | --- |
| Regular 400, 14-16px | 1.5px |
| Medium/semibold 500-600 | 2px |
| Bold 700, or emphasized standalone | 2.5px |

```html
<button class="flex items-center gap-2 font-semibold">
  <PlusIcon stroke-width="2" class="size-4" /> New project
</button>
```

- One optical strategy per surface - don't mix libraries with incompatible stroke conventions on one toolbar. If a set has no stroke variants, keep its native stroke and use size or color for emphasis.
- Size inline icons relative to cap height, typically `1em`-`1.25em`, so icon and text scale together.

## One SVG, CSS states

```html
<svg fill="none" stroke="currentColor" stroke-width="2">...</svg>
```

```css
.icon-button { color: oklch(0.552 0.016 285.938); }
.icon-button:hover { color: oklch(0.21 0.006 285.885); }
.icon-button[aria-pressed="true"] { color: oklch(0.623 0.188 259.815); }
.icon-button:disabled { opacity: 0.4; }
```

Tailwind: `text-zinc-500 hover:text-zinc-900 aria-pressed:text-blue-600 disabled:opacity-40`. Strip hardcoded fills (`fill="#666"`) to `currentColor` on import.

## Outline default, fill active

| Variant | For |
| --- | --- |
| Outline | Default: toolbars, rows, inline with text |
| Fill | Selected/active: current tab, toggled bookmark, liked heart |

Filled icons everywhere erase the active-state signal. The swap between variants uses the contextual icon cross-fade (motion.md).

## Design at render size

- Test every icon at its smallest render size (often 16px); it must stay recognizable.
- Use simplified glyphs for small contexts rather than shrinking detailed art.
- Stay on the set's native grid sizes (16, 20, 24) - fractional scaling renders soft.
- SVG, never raster.

## Icons in RTL

| Flip | Don't flip |
| --- | --- |
| Back/forward arrows, navigation chevrons | Logos, brand marks |
| Text-block glyphs (alignment, lists, indent) | Checkmarks |
| Volume waves | Physical objects (clocks, cups, pencils) |
| Directional "send" glyphs | Media playback controls (convention keeps them LTR) |

```css
[dir="rtl"] .icon-directional { scale: -1 1; }
```

Tailwind: `rtl:-scale-x-100`. Analyze composites part by part - a badge overlay may stay put while the base glyph flips.
