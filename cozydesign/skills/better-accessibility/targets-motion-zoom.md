# Targets, motion, and zoom

## Target sizes

| Standard | Minimum |
| --- | --- |
| WCAG 2.5.8 (AA) | 24x24 px - the hard floor |
| WCAG 2.5.5 (AAA) | 44x44 px |
| Apple HIG | 44x44 pt |
| Material | 48x48 dp |

Recommend 44px for primary touch controls and 40px on desktop where density allows. Smaller isn't automatically a failure - check the spacing, equivalent-control, inline, user-agent, and essential exceptions first. **Spacing exception:** an undersized target passes if a 24px circle centered on it overlaps no other target or other undersized target's circle (simple case: 20px targets need 4px gaps).

The visual can be small; the hit area must be big, and anything that looks clickable is clickable across its whole visual extent.

**Grow the hit area with a pseudo-element** on the wrapping `<label>` or `<button>` - never on the `<input>` (replaced elements don't render pseudo-elements reliably):

```css
.checkbox-label { position: relative; width: 20px; height: 20px; }
.checkbox-label::after {
  content: "";
  position: absolute;
  top: 50%; left: 50%;
  transform: translate(-50%, -50%);
  width: 44px; height: 44px;
}
```

Tailwind: `relative size-5 after:absolute after:top-1/2 after:left-1/2 after:size-11 after:-translate-1/2`.

When the element can afford real size, skip the pseudo-element: `min-width: 44px; min-height: 44px; display: inline-grid; place-items: center;` gives the browser real geometry.

**Collisions:** where an extended area would overlap another control, shrink it to the largest non-colliding size. Hit areas never overlap.

**Decorative layers** (scrims, glows, sheens, full-bleed `::after`) swallow every click in their box. Give them `pointer-events: none` and `aria-hidden="true"`. A scrim that dismisses on click is a control - leave its events on.

## Touch

- `touch-action: manipulation` on interactive elements removes double-tap-zoom delay.
- `touch-action: none` only on a surface implementing its own pan/zoom/drag - scoped there, never page-wide.
- Set `-webkit-tap-highlight-color` to suit the design.
- Gate hover-only styles behind `@media (hover: hover)`; on touch, `:hover` sticks after a tap and looks like a stuck selection. (Tailwind 4's `hover:` already compiles under this query.)
- Prefer generous targets over finicky drag handles and precise hover zones.

## Reduced motion

Make motion opt-in:

```css
.card { /* static styles */ }
@media (prefers-reduced-motion: no-preference) {
  .card { transition: transform 200ms ease-out; }
}
```

Tailwind: `motion-safe:` / `motion-reduce:` variants.

Fallback kill switch for existing codebases where opt-in isn't feasible:

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}
```

Use `0.01ms`, not `none`, so `animationend`/`transitionend` still fire and waiting code doesn't hang.

Reduced means reduced, not eliminated - it targets vestibular triggers, not feedback:

| Disable | Replace | Keep |
| --- | --- | --- |
| Parallax | Slide/scale/zoom → opacity crossfade | Spinners and progress |
| Autoplaying video, GIFs, looping decoration | Smooth scroll → instant jump | Instant state changes (hover color, focus ring) |
| Spinning, large movement across the screen | Auto-rotating carousels → start paused | Brief functional feedback (press) |

## Autoplay and timed UI

- Anything moving, blinking, or auto-updating for over 5 seconds needs a visible pause/stop (WCAG 2.2.2) - muted hero loops included.
- Prefer explicit dismissal. Auto-dismiss suits only low-stakes confirmations. Toasts with an action, error, or needed information stay until dismissed; if one must time out, 5 seconds minimum and hover/focus pauses it.
- Never put critical information only in a timed element - an undo link in a vanished toast is scheduled data loss.

## Zoom and reflow

- **200% text zoom** (WCAG 1.4.4): all content and functions survive; the viewport never blocks zoom.
- **Reflow at 320px** (WCAG 1.4.10): works with vertical scrolling alone. Genuinely 2D content (tables, maps, code) may scroll inside its own container.
- Fixed heights break under zoom - use `min-height` for anything holding text.

**rem vs px.** Follow the codebase; never mix units into an established px or Tailwind system. Where you choose:

| `rem` | `px` |
| --- | --- |
| `font-size` | Borders, hairlines |
| `max-width` of text containers | Focus outline width/offset |
| Media-query breakpoints (`48rem`) | Shadow details |
| Spacing that should scale with text | Fixed decorations |

Breakpoints matter most: at a larger base font size a `rem` query switches to the narrow layout when the text needs it; a `px` query doesn't.
