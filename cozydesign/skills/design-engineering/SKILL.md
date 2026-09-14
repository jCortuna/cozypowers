---
name: design-engineering
description: Design-engineering judgment for UI polish - animation decisions, easing and timing, component feel, gestures, CSS transform and clip-path technique, and motion performance. Use this skill whenever building or reviewing interactive UI (buttons, popovers, tooltips, modals, drawers, toasts, tabs, drag gestures), whenever the developer says an interface "feels off", "feels cheap", "needs polish", or asks to review UI code for feel. Reviews produced by this skill use a Before/After/Why table.
---

# Design Engineering

Act as a design engineer: someone who writes the code *and* owns how it feels. When everyone's software works, feel is the differentiator - and feel is the sum of hundreds of details nobody consciously notices.

## Principles

- **Taste is trained.** It is not preference; it is pattern recognition built by studying good work and asking *why* it feels right. When in doubt, reverse-engineer a product that gets it right.
- **Invisible details compound.** The goal is an interface that behaves exactly as the user already assumed it would, so they never think about it. No single detail is noticed; their absence is.
- **Beauty is leverage.** People choose tools on overall experience. Excellent defaults and well-judged motion are real competitive advantages, and most software leaves them on the table.

## Review format (required)

When reviewing UI code, output **one markdown table** with columns `Before | After | Why`, one row per issue. Never a list of "Before:/After:" lines.

| Before | After | Why |
| --- | --- | --- |
| `transition: all 300ms` | `transition: transform 200ms ease-out` | Name the properties; `all` animates things you didn't intend |
| `transform: scale(0)` | `transform: scale(0.95); opacity: 0` | Real objects never appear from nothing |
| `ease-in` on a dropdown | strong custom `ease-out` | `ease-in` delays the moment the user is watching |

## The animation decision framework

Answer these in order before writing motion code.

### 1. Should it animate at all?

| How often the user sees it | Decision |
| --- | --- |
| 100+ times a day (shortcuts, command palette toggle) | Never animate |
| Tens of times a day (hover, list navigation) | Remove, or make it nearly imperceptible |
| Occasionally (modal, drawer, toast) | Standard animation |
| Rarely / first time (onboarding, success, celebration) | Room for delight |

Anything triggered from the keyboard does not animate. Repetition turns motion into latency. (A launcher like Raycast opening instantly is the correct design, not a missing feature.)

### 2. What is it for?

Motion must have a job: **feedback** (the press was heard), **spatial consistency** (it leaves the way it came), **state indication** (a change made legible), **explanation** (showing how something works - marketing and onboarding), or **preventing a jarring jump**. "It looks nice" on something seen often is a reason *not* to animate.

### 3. Which easing?

- Entering or exiting → `ease-out`
- Moving or morphing while on screen → `ease-in-out`
- Hover and color changes → `ease`
- Constant motion (marquee, progress) → `linear`
- Unsure → `ease-out`

Never use `ease-in` for UI: it starts slowly, exactly when attention peaks, so the same 300ms *feels* longer. The built-in CSS curves are also too soft - use stronger ones:

```css
--ease-out: cubic-bezier(0.23, 1, 0.32, 1);      /* UI enter/exit */
--ease-in-out: cubic-bezier(0.77, 0, 0.175, 1);  /* on-screen movement */
--ease-drawer: cubic-bezier(0.32, 0.72, 0, 1);   /* iOS-style sheet */
```

Don't invent curves by eye; pick from a curated easing reference if these don't fit.

### 4. How long?

| Element | Duration |
| --- | --- |
| Press feedback | 100-160ms |
| Tooltip, small popover | 125-200ms |
| Dropdown, select | 150-250ms |
| Modal, drawer | 200-500ms |
| Marketing / explanatory | Longer is fine |

Keep UI motion **under 300ms**. Duration shapes perceived performance: a 180ms select feels faster than a 400ms one, a quicker spinner makes the same load feel shorter, and `ease-out` at 200ms feels quicker than `ease-in` at 200ms.

## Springs

Springs model physics instead of a fixed timeline, so they feel alive and - crucially - **keep their velocity when interrupted**, where CSS keyframes restart from zero. Use them for drag with momentum, gestures the user may reverse, "living" elements, and decorative pointer-following.

```js
{ type: "spring", duration: 0.5, bounce: 0.2 }           // perceptual config - easiest to reason about
{ type: "spring", mass: 1, stiffness: 100, damping: 10 }   // physical config - more control
```

Keep bounce at 0.1-0.3 and absent from most UI; save it for drag-to-dismiss and playful moments. Smoothing pointer-driven values through a spring (e.g. Motion's `useSpring`) removes the robotic feel of values snapping to the cursor - but only where the effect is decorative. A chart someone is reading should not wobble.

## Component rules

- **Pressables respond.** `:active { transform: scale(0.97) }` with `transition: transform 160ms ease-out`. Keep the scale between 0.95 and 0.98. `scale()` scales children too, which is what makes it read as physical.
- **Never enter from `scale(0)`.** Start at `scale(0.9)` or higher, combined with `opacity: 0`.
- **Popovers grow from their trigger.** Set `transform-origin` to the trigger side (headless libraries such as Base UI expose `var(--transform-origin)`). **Modals are the exception** - not anchored to anything, they stay centered.
- **Tooltips: delay the first, not the rest.** Once one tooltip is open, neighbours open instantly with the transition set to `0ms`. The toolbar feels faster without losing protection from accidental hovers.
- **Transitions over keyframes for dynamic UI.** Transitions retarget from the current value when interrupted; keyframes restart. Anything that can fire twice in a second (toasts, toggles) uses transitions.
- **Blur hides a bad crossfade.** If two overlapping states read as two objects no matter the curve, add `filter: blur(2px)` during the swap. Keep blur under 20px - it is expensive, especially in Safari.
- **Enter animations without JS:** `@starting-style { opacity: 0; transform: translateY(100%) }` inside the rule. Fall back to a `data-mounted` attribute set after first render where support is missing.
- **Asymmetric timing.** Slow where the user is deciding (hold-to-delete fill: 2s linear), fast where the system responds (release: 200ms ease-out). Exits are generally quicker than entrances.
- **Stagger group entrances** by 30-80ms per item. Longer feels sluggish. Stagger is decoration - never block interaction while it plays.
- **Match motion to personality.** A toast library tuned slightly slower with plain `ease` can feel elegant; a pro dashboard should be crisp. The easing, timing, visual design, and even the name should belong together.

## Transform and clip-path technique

- `translateY(100%)` moves an element by **its own** height - ideal for drawers and toasts of unknown size. Prefer percentages to hard-coded pixels.
- `transform-style: preserve-3d` with `rotateX/rotateY/translateZ` gives real 3D (coin flips, orbits) with no JS.
- `clip-path: inset(top right bottom left)` is an animation primitive, not just a shape:
  - **Reveal:** `inset(0 100% 0 0)` → `inset(0 0 0 0)`.
  - **Hold to delete:** colored overlay clipped fully; on `:active` transition to fully visible over 2s linear; on release snap back in 200ms ease-out; add press scale.
  - **Tabs with perfect color change:** duplicate the tab list, style the copy as active, clip the copy to the active tab, animate the clip. Background and text change in lockstep because it is one reveal, not two interpolations.
  - **Scroll image reveal:** `inset(0 0 100% 0)` → `inset(0 0 0 0)` on entering the viewport, once (IntersectionObserver, or `useInView` with `{ once: true, margin: "-100px" }`).
  - **Before/after slider:** stack two images and adjust the top image's right inset from drag position. No extra DOM.

## Gestures

- **Dismiss on velocity, not only distance:** `velocity = |distance| / elapsedMs`; dismiss if past the threshold **or** velocity > ~0.11. A flick should be enough.
- **Damp past boundaries:** the further past the edge, the less it moves. Friction, not an invisible wall.
- **Capture the pointer** once dragging begins so the drag survives leaving the element.
- **Ignore extra touch points** mid-drag, or switching fingers makes the element jump.

## Performance

- Animate **`transform` and `opacity`** (plus `clip-path`). Width, height, margin, padding, top, left trigger layout and paint every frame.
- Don't drive a moving element through a CSS variable on its parent - it restyles every child. Set `transform` on the element itself.
- In Motion (Framer Motion), the `x`/`y`/`scale` shorthands run on the main thread and drop frames under load; animate a full `transform` string for hardware acceleration.
- CSS animations run off the main thread and stay smooth while the page is busy; use CSS for predetermined motion and JS for dynamic, interruptible motion.
- Need JS control without a library? The Web Animations API (`element.animate(...)`) gives CSS-grade performance and is interruptible.

## Accessibility

- `prefers-reduced-motion: reduce` means **fewer, gentler** animations - keep opacity and color changes that aid comprehension, remove movement.
- Gate hover motion behind `@media (hover: hover) and (pointer: fine)`; touch devices fire hover on tap.

## Building components people love

1. Minimal setup beats configurability - one mount point, one function call.
2. Defaults matter more than options; most people never customise.
3. A memorable name builds identity.
4. Handle edge cases invisibly: pause timers when the tab is hidden, fill gaps between stacked items so hover doesn't flicker, capture pointers during drags.
5. Let people touch it: interactive docs with copyable snippets lower the barrier to adoption.

## Debugging feel

- Slow animations to 2-5x or use the DevTools Animations panel; step frame by frame. Look for overlapping states in crossfades, abrupt starts/stops, wrong transform origin, and properties drifting out of sync.
- Test gestures on a real phone (dev server over LAN plus remote devtools), not only a simulator.
- Look again the next day. Fresh eyes catch what a long session hides.

## Review checklist

| Issue | Fix |
| --- | --- |
| `transition: all` | Name exact properties |
| `scale(0)` entrance | `scale(0.95)` + `opacity: 0` |
| `ease-in` on UI | `ease-out` or the strong custom curve |
| Centered origin on a popover | Trigger-side origin (modals exempt) |
| Motion on a keyboard action | Remove it |
| UI duration over 300ms | 150-250ms |
| Ungated hover motion | `(hover: hover) and (pointer: fine)` |
| Keyframes on rapidly triggered UI | Transitions |
| Motion `x`/`y` props under load | Full `transform` string |
| Exit as slow as enter | Faster exit |
| Group appears all at once | 30-80ms stagger |
| No reduced-motion handling | Gentler variant |
