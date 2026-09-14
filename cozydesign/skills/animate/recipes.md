# Animation recipes

Starting points for the cases that come up most. Adapt; don't rebuild. Curves refer to the `--ease-out`, `--ease-in-out`, and `--ease-drawer` tokens in SKILL.md.

---

## Button press

```css
.button { transition: transform 160ms var(--ease-out); }
.button:active { transform: scale(0.97); }
```

Children scale with it, which is what reads as a physical press. `:active` works on touch, so no hover gate is needed here - gate any `:hover` styles separately.

---

## Dropdown, popover, menu, select

```css
.popover {
  transform-origin: var(--transform-origin); /* supplied by Base UI and similar */
  transition: opacity 200ms var(--ease-out), transform 200ms var(--ease-out);
}
.popover[data-starting-style],
.popover[data-ending-style] {
  opacity: 0;
  transform: scale(0.95);
}
```

The origin is the point: the panel should appear to come out of what was clicked.

---

## Tooltip

```css
.tooltip {
  transform-origin: var(--transform-origin);
  transition: transform 125ms var(--ease-out), opacity 125ms var(--ease-out);
}
.tooltip[data-starting-style],
.tooltip[data-ending-style] {
  opacity: 0;
  transform: scale(0.97);
}
.tooltip[data-instant] { transition-duration: 0ms; } /* neighbours open instantly */
```

Delay only the first tooltip; once one is open, skip delay and animation for the rest.

---

## Modal

```css
.modal {
  transform-origin: center; /* not anchored to a trigger */
  transition: opacity 250ms var(--ease-out), transform 250ms var(--ease-out);
}
.modal[data-starting-style],
.modal[data-ending-style] {
  opacity: 0;
  transform: scale(0.96);
}
.backdrop { transition: opacity 250ms var(--ease-out); }
```

Fade the backdrop in step so both read as one surface.

---

## Drawer / sheet

```css
.drawer {
  transform: translateY(0);
  transition: transform 500ms var(--ease-drawer);
}
.drawer[data-closed] { transform: translateY(100%); }
```

Adding drag turns this into a gesture problem - see *Drag to dismiss*.

---

## Toast

```css
.toast {
  opacity: 1;
  transform: translateY(0);
  transition: opacity 400ms ease, transform 400ms ease;
  @starting-style {
    opacity: 0;
    transform: translateY(100%);
  }
}
```

Plain `ease`, a little slower than typical UI, suits a toast's personality. Without `@starting-style`, set a `data-mounted` flag after first render. When stacked toasts reflow, balancing the opacity change against the height change is trial and error - tune it, then recheck tomorrow.

---

## Accordion / collapse

```css
.content {
  overflow: hidden;
  transition: height 200ms var(--ease-out), opacity 200ms var(--ease-out);
}
```

Keep it short - height costs layout every frame. Measure the content height (or use a primitive that exposes it) instead of animating to `auto`.

---

## Staggered group entrance

For something seen occasionally, not a list scrolled past all day.

```css
.item {
  opacity: 0;
  transform: translateY(8px);
  animation: fade-in 300ms var(--ease-out) forwards;
}
.item:nth-child(2) { animation-delay: 50ms; }
.item:nth-child(3) { animation-delay: 100ms; }
.item:nth-child(4) { animation-delay: 150ms; }
@keyframes fade-in { to { opacity: 1; transform: translateY(0); } }
```

Never block interaction while a stagger plays.

---

## Hold to confirm

For destructive actions that a single click makes too easy.

```css
.overlay {
  clip-path: inset(0 100% 0 0);
  transition: clip-path 200ms var(--ease-out); /* release: snappy */
}
.button:active .overlay {
  clip-path: inset(0 0 0 0);
  transition: clip-path 2s linear; /* press: deliberate */
}
.button:active { transform: scale(0.97); }
```

`linear` is right here: the fill is a progress indicator, and progress shouldn't ease.

---

## Tab indicator with color change

Duplicate the tab list, style the copy as active, and clip it to the active tab:

```css
.tabs-active-copy {
  clip-path: inset(0 60% 0 20%); /* computed from the active tab's position */
  transition: clip-path 250ms var(--ease-in-out);
}
```

Text and background change in perfect sync because a single element is being revealed.

---

## Scroll reveal

Marketing surfaces only.

```css
.reveal {
  clip-path: inset(0 0 100% 0);
  transition: clip-path 600ms var(--ease-in-out);
}
.reveal[data-visible] { clip-path: inset(0 0 0 0); }
```

Trigger once via IntersectionObserver (or `useInView` with `{ once: true, margin: "-100px" }`). Re-animating on every pass fights the reader.

---

## Drag to dismiss

```js
const elapsed = Date.now() - dragStart.current;
const velocity = Math.abs(swipeAmount) / elapsed;
if (Math.abs(swipeAmount) >= SWIPE_THRESHOLD || velocity > 0.11) dismiss();

// Move the dragged element directly - not through a parent CSS variable.
element.style.transform = `translateY(${distance}px)`;
```

- Capture the pointer when the drag starts.
- Ignore new touch points while dragging (`if (isDragging) return`).
- Damp movement past natural boundaries; allow over-drag with rising friction instead of a hard stop.
- Settle with a spring (`{ type: "spring", duration: 0.5, bounce: 0.2 }`) so interrupted drags keep their velocity.

---

## Masking a crossfade that won't settle

```css
.content { transition: filter 200ms ease, opacity 200ms ease; }
.content.transitioning { filter: blur(2px); opacity: 0.7; }
```

Blur fuses two overlapping states into one perceived change. Stay under 20px.

---

## Programmatic motion without a library

```js
element.animate(
  [{ clipPath: "inset(0 0 100% 0)" }, { clipPath: "inset(0 0 0 0)" }],
  { duration: 1000, fill: "forwards", easing: "cubic-bezier(0.77, 0, 0.175, 1)" }
);
```

Hardware-accelerated, interruptible, zero bundle cost.
