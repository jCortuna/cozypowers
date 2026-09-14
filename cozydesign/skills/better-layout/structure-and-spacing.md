# Structure and spacing

## Grouping

Three tools, in order of preference:

1. **Negative space** - the default. Related close, unrelated far.
2. **Background shapes** - when a group must read as a unit (a selectable row, a draggable card).
3. **Separator lines** - last resort for dense data (tables, long settings lists).

Rule: inter-group gap ≥ 2x intra-group gap.

```css
/* Good: spacing alone communicates grouping */
.field-group { display: flex; flex-direction: column; gap: 8px; }
.form { display: flex; flex-direction: column; gap: 24px; }

/* Bad: uniform spacing plus lines to compensate */
.form > * { margin-bottom: 12px; border-bottom: 1px solid var(--separator); }
```

If a separator is genuinely needed, keep it quiet: hairline, low contrast, and never paired with a large gap that already did the job.

## Controls vs content

```html
<!-- Bad: the action is indistinguishable from the sentence -->
<p class="text-zinc-600">Your trial ends soon. Upgrade now</p>

<!-- Good -->
<p class="text-zinc-600">Your trial ends soon.</p>
<button class="font-medium text-blue-600">Upgrade now</button>
```

## Shared edges

- An icon 2px off the text edge or a card padded differently from its neighbor is noise even if nobody can name it.
- Repeat one indent step for each nesting level.
- In tables, numbers align to the trailing edge, text to the leading edge.

```css
/* Good: one leading edge, one indent step */
.section { padding-inline: 24px; }
.section .child { margin-inline-start: 16px; }

/* Bad: three unrelated leading edges in one column */
.header { padding-inline-start: 20px; }
.list-item { padding-inline-start: 14px; }
.footer { padding-inline-start: 24px; }
```

## Logical properties

| Physical (avoid) | Logical (use) |
| --- | --- |
| `margin-left` | `margin-inline-start` |
| `padding-right` | `padding-inline-end` |
| `left: 0` | `inset-inline-start: 0` |
| `text-align: left` | `text-align: start` |
| `border-right` | `border-inline-end` |

Tailwind: `ms-4 pe-6 text-start` rather than `ml-4 pr-6 text-left`.

Physical properties remain right for truly physical sides (a device notch, a gesture direction). Sequences that encode progression - star ratings, steppers, progress bars - mirror in RTL (stars fill from the trailing side). Flex and grid with logical properties mirror automatically; hand-positioned elements don't. Digit order within numbers never reverses (a typography concern).

## Importance ordering

- Most important information near the top and leading edge.
- Don't bury the one number the user came for under secondary detail; move detail into collapsed sections, tabs, or detail views.
- Within a row, identifying content leads; metadata and actions trail.

```html
<!-- Good -->
<p class="text-2xl font-semibold">$4,320.00</p>
<p class="text-sm text-zinc-500">Available balance</p>

<!-- Bad: the key fact is the last line -->
<p class="text-sm">Account 4402 · Opened 2019 · Standard tier</p>
<p class="text-sm">Last statement: June 30</p>
<p class="text-sm">Balance: $4,320.00</p>
```

The first screen is a table of contents, not the whole book - if everything is prominent, nothing is.

## Spacing between targets

| Between | Starting point |
| --- | --- |
| Adjacent bordered/filled controls | 12px |
| Around borderless controls (text, icon buttons) | 24px |
| Unrelated control groups | 24px+ (2x intra-group) |

Borderless controls need more room because the space *is* the boundary. Preserve an established usable density rather than inflating it. These clearances are in addition to accessibility hit areas, so expanded areas never overlap.

## Edge insets and safe areas

```css
/* Good: inset action bar */
.action-bar {
  padding-inline: 16px;
  padding-bottom: calc(16px + env(safe-area-inset-bottom));
}
.action-bar button { width: 100%; border-radius: 12px; }

/* Bad: glued to three edges */
.action-bar button { width: 100vw; border-radius: 0; position: fixed; bottom: 0; }
```

## Disclosure affordances

Keep the product's existing scroll/disclosure cues; where none exist:

- **Peeking scrollers:** size items so the next peeks 16-32px past the edge. A row ending exactly at the edge looks complete and nobody scrolls.
- **Disclosure controls:** chevron or "Show more", labelled with what's hidden ("Show 12 more results").
- **Truncation:** ellipsis plus a way to expand.

```css
.scroller {
  display: flex; gap: 12px; overflow-x: auto;
  padding-inline: 24px; scroll-padding-inline: 24px;
  scroll-snap-type: x mandatory;
}
.scroller > * {
  flex: 0 0 calc(100% - 48px - 24px); /* container − margins − peek */
  scroll-snap-align: start;
}
```

## Bleed vs float

```css
/* Full-bleed media inside a constrained article */
.article { display: grid; grid-template-columns: 1fr min(65ch, calc(100% - 48px)) 1fr; }
.article > * { grid-column: 2; }
.article > .full-bleed { grid-column: 1 / -1; }

/* Floating action respects safe areas */
.fab {
  position: fixed;
  inset-inline-end: calc(16px + env(safe-area-inset-right));
  bottom: calc(16px + env(safe-area-inset-bottom));
}
```

## Breakpoints

- Break where the layout stops fitting (a sidebar squeezing content below its minimum measure, a grid dropping below a usable column width) - not at 768px because a preset says so.
- Collapse late; premature collapse wastes space the user has.
- Components adapt to their container:

```css
.card-list { container-type: inline-size; }
@container (max-width: 400px) { .card { grid-template-columns: 1fr; } }
```

A viewport media query here would break the card inside a narrow sidebar.

## Growth and clipping

- No fixed widths sized to English; `max-width` plus wrapping.
- No fixed heights on text containers; `min-height` for floors.
- Buttons size from their label (`padding-inline: 16px; white-space: nowrap`), never a hardcoded width that German will overflow.
- Test with pseudo-localization or a long-string locale.
- Never place a critical action where it can be cut off: bottom of a resizable pane, below the fold of a fixed-height modal, behind the on-screen keyboard. When a modal's content scrolls, its action row doesn't.
