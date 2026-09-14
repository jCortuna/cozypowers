---
name: animate
description: Build a UI animation from scratch by making decisions in the order that determines whether it feels right - whether it should animate at all, its purpose, the tool, the properties, the curve and duration, interruption, exit, and reduced motion - then write the implementation. Use when asked to animate something, add motion or a transition, or make a component "feel alive". For critiquing existing motion, use design-engineering; for a broad interface polish pass, use better-ui.
---

# Animate

A construction skill: turn a request for motion into code that would pass a strict design-engineering review on the first try. It builds; it does not audit.

## Posture

Build it yourself, decisively. Two ways to fail, and the first is worse:

1. **Animating something that shouldn't move.** The gate below is allowed to produce zero lines of code. That is a success.
2. **Right idea, wrong ingredients** - `ease-in` on an entrance, `scale(0)`, keyframes on a toast, a sluggish duration.

Never offer a menu of motion options. Decide, give the reason in one line, write the code.

## Hard rules

1. Run the sequence in order. Steps 1-2 gate everything.
2. No approximated values. Curves, durations, and spring configs come from the tables below - don't type a familiar-looking bezier from memory.
3. Extend existing tokens. If the codebase already has `--ease-out` or a duration scale, use it; a parallel system is a defect.
4. Reduced-motion handling and hover gating ship **with** the animation, never as a follow-up.
5. Cheapest tool that works. No motion library for a fade.

## The sequence

### 1. Should it animate?

| Frequency | Decision |
| --- | --- |
| 100+/day (keyboard shortcut, command palette) | **No animation.** Stop. |
| Tens/day (hover, list navigation) | Barely perceptible, or nothing |
| Occasional (modal, drawer, toast) | Standard animation |
| Rare / first-time (onboarding, success) | Delight is allowed here |

Keyboard-initiated actions are disqualified outright. If the request fails the gate, say so and offer the non-motion alternative (instant state change, a static affordance).

### 2. Name the purpose

One of: **feedback**, **spatial consistency**, **state indication**, **preventing a jarring change**, **explanation** (marketing/onboarding only), **delight** (rare tier only). If you can't name it, don't build it.

Also check function: content the user is reading or acting on should not move for style.

### 3. Pick the tool - stop at the first that fits

| Need | Tool |
| --- | --- |
| Hover, press, color, class/attribute toggle | CSS transition |
| Entrance on mount, no JS state | CSS `@starting-style` |
| Predetermined motion that must stay smooth while the page is busy | CSS animation (off main thread) |
| Programmatic control, no dependency | Web Animations API (`element.animate`) |
| Springs, layout animation, exit animation, gesture-driven values | Motion (motion.dev) |

If what's really needed is a *component* (toast, drawer, command menu, dropdown), use an accessible headless primitive rather than hand-rolling one - a hand-built `<div>` dropdown usually ships without focus management.

### 4. Pick the properties

- `transform` and `opacity` only. `clip-path` is the sanctioned fourth. `height` is tolerated only for accordions.
- Never `scale(0)`; start at `scale(0.9-0.97)` with `opacity: 0`.
- Trigger-side `transform-origin` for popovers, menus, tooltips (`var(--transform-origin)` in Base UI). Modals stay centered.
- `translate()` percentages are relative to the element's own size - prefer them to pixels.
- In Motion, animate a full `transform` string; the `x`/`y`/`scale` shorthands drop frames under load.
- Never animate a child through a CSS variable on its parent; set `transform` on the element.

### 5. Easing and duration, or a spring

| Situation | Easing |
| --- | --- |
| Entering / exiting | ease-out |
| Moving or morphing on screen | ease-in-out |
| Hover / color | ease |
| Constant motion | linear |
| Default | ease-out |

Never `ease-in` on UI. Use strong curves:

```css
--ease-out: cubic-bezier(0.23, 1, 0.32, 1);
--ease-in-out: cubic-bezier(0.77, 0, 0.175, 1);
--ease-drawer: cubic-bezier(0.32, 0.72, 0, 1);
```

| Element | Duration |
| --- | --- |
| Press feedback | 100-160ms |
| Tooltip, small popover | 125-200ms |
| Dropdown, select | 150-250ms |
| Modal, drawer | 200-500ms |
| Marketing / explanatory | Can be longer |

UI motion stays under 300ms.

Use a **spring** instead for drag with momentum, reversible gestures, "alive" elements, and decorative pointer-following:

```js
{ type: "spring", duration: 0.5, bounce: 0.2 }
{ type: "spring", mass: 1, stiffness: 100, damping: 10 }
```

Bounce 0.1-0.3, and none in most UI.

### 6. Interruption and exit

- Transitions, not keyframes, for anything that can be triggered rapidly - they retarget instead of restarting.
- Springs for gestures - they carry velocity through interruptions.
- Exit the way it entered (a toast that rises from the bottom leaves through the bottom).
- Asymmetric timing: slow while the user decides (hold-to-confirm: 2s linear), fast when the system answers (release: 200ms ease-out).

### 7. Reduced motion and pointer gating

```css
@media (prefers-reduced-motion: reduce) {
  .element { animation: fade 0.2s ease; } /* keep opacity/color, drop movement */
}
@media (hover: hover) and (pointer: fine) {
  .element:hover { transform: scale(1.05); }
}
```

```jsx
const reduce = useReducedMotion();
const closedX = reduce ? 0 : "-100%";
```

Reduced motion means fewer and gentler, not none.

## Recipes

For button press, dropdown/popover, tooltip, modal, drawer, toast, accordion, stagger, hold-to-confirm, tab indicator, scroll reveal, drag-to-dismiss, crossfade masking, and library-free programmatic motion, start from [recipes.md](recipes.md) rather than a blank file.

## Never ship

| Never | Instead |
| --- | --- |
| `transition: all` | Exact properties |
| `scale(0)` entrance | `scale(0.95)` + `opacity: 0` |
| `ease-in` on UI | ease-out / strong curve |
| Built-in `ease-out` on a deliberate animation | `cubic-bezier(0.23, 1, 0.32, 1)` |
| Motion on a keyboard or 100+/day action | Nothing |
| UI duration > 300ms without reason | 150-250ms |
| Centered origin on a trigger-anchored popover | Trigger-side origin |
| Keyframes on toasts/toggles | Transitions |
| Animating width/height/margin/padding/top/left | transform/opacity |
| Motion `x`/`y`/`scale` under load | Full transform string |
| Ungated `:hover` motion | hover/pointer media query |
| No reduced-motion variant | Gentler variant |
| Whole group entering at once | 30-80ms stagger |

## Output

Write the code. Then, in a few lines at most:

- **Gate result** - frequency tier and named purpose; anything rejected and why.
- **Ingredients** - tool, properties, curve, duration or spring, one line each.
- **Feel-check** - where the result depends on feel you can't judge from code (crossfades, spring bounce, opacity vs height in a reflowing list), say how to check: play at 2-5x duration or in the DevTools animation inspector, step frames, test gestures on a real device, look again tomorrow.

The code is the deliverable; don't pad it into a report. When the honest answer is "this shouldn't animate", give it.
