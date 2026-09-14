# Details

## Underlines

```css
/* Metrics from the font */
a { text-underline-position: from-font; text-decoration-thickness: from-font; }

/* Hint at extra information */
abbr { text-decoration: underline dotted; }

/* Manual tuning */
a {
  text-decoration-thickness: 1px;
  text-underline-offset: 3px;
  text-decoration-skip-ink: auto;
  text-decoration-color: var(--link-underline);
  transition: text-decoration-color 200ms ease-out;
}
a:hover { text-decoration-color: var(--link-underline-hover); }
```

Only the color of a real underline animates reliably; for any other underline animation build a separate element.

## Selection and editing

- `::selection` can carry brand if the pair stays legible.
- `::target-text` styles the phrase a shared text-fragment link scrolls to.
- The Custom Highlight API styles arbitrary ranges (search matches) without extra markup.
- `::placeholder` styles empty-field hints; `caret-color` tints the insertion bar - that's about as far as caret styling should go.

## iOS input zoom

Safari zooms the page when an input's text is under 16px (an accessibility behavior - 16px is the web default). Both fixes are correct; they differ in appearance.

**Size up on mobile** - 16px on small screens, design size from `sm` up. Simple, but mobile and desktop inputs differ:

```tsx
<input className="text-base sm:text-sm" type="email" />
```

**Scale down** - keep `font-size: 16px`, render smaller via transform. Identical at every viewport, but needs compensation: widen by the inverse scale so it still fills its container, divide line-height by the same factor, set the transform origin to the start edge (right edge under RTL), and drop the transform above the breakpoint.

```tsx
// 13px rendered from 16px: 13 / 16 = 0.8125
<div className="flex h-10 items-center rounded-[10px] bg-gray-300 px-2.5">
  <input
    type="email"
    className="h-full w-[calc(100%/0.8125)] origin-left scale-[0.8125] bg-transparent text-base leading-[calc(1.125/0.8125)] outline-none sm:w-full sm:scale-100 sm:text-[13px]"
  />
</div>
```

The transform shrinks the whole box, so a wrapper draws the field's surface and the input stays transparent - a border or ring on the scaled element would shrink and miss the intended hit area.

## Decorative text

| Property | Effect |
| --- | --- |
| `::first-letter` | Drop cap (widely supported) |
| `::first-line` | Style only the first line |
| `initial-letter` | Size a drop cap (limited support; no Firefox yet) |
| `background-clip: text` | Clip a background or gradient to glyphs |
| `-webkit-text-stroke` | Outline glyphs (works across modern browsers) |
| `text-shadow` | Shadow that follows glyph shapes |

Stray lines *inside* stroked letters come from variable fonts keeping overlapping contours unmerged; static fonts don't show it.

## Size floors

| Text | Size |
| --- | --- |
| Long-form body | ~16px, verified in the actual face and measure |
| Inputs and menus | ~14px |
| Captions | 13px |
| Floor | Rarely below 12px |

Type must survive the reader changing it - zoom, larger default font size, overridden line height or letter spacing.

## Font smoothing

```css
html { -webkit-font-smoothing: antialiased; -moz-osx-font-smoothing: grayscale; }
```

Tailwind: `antialiased` on `<body>`, once.
