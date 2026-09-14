# Motion

**Motion should clarify, not decorate.** Each animation answers "what changed?", "where did this come from?", or "did the interface hear me?" - otherwise delete it. For component-level craft (easing choice, press feedback, popovers, drawers, toasts, drag), follow the **animate** skill; this file covers page-level motion and the per-screen tracks.

## Decision gate

| Question | Ship when | Cut or reduce when |
| --- | --- | --- |
| How often is it seen? | Occasional, first-run, explanatory | Keyboard actions, command palettes, core nav, dense lists, anything seen dozens of times a day |
| What's it for? | Feedback, spatial consistency, state, explanation, avoiding a jarring jump | Only "it looks cool" |
| Within budget? | UI ≤300ms, small pieces ≤200ms | Needs slow showmanship |
| Helps the task? | Clarifies state, hierarchy, progress | Moves data someone is reading or acting on |

## Tokens

```css
:root {
  --ease-out: cubic-bezier(0.23, 1, 0.32, 1);
  --ease-in-out: cubic-bezier(0.77, 0, 0.175, 1);
  --ease-drawer: cubic-bezier(0.32, 0.72, 0, 1);
  --duration-press: 120ms;
  --duration-popover: 180ms;
  --duration-panel: 240ms;
}
```

| Element | Duration | Easing |
| --- | --- | --- |
| Press | 100-160ms | ease-out |
| Tooltip / small popover | 125-200ms | ease-out |
| Dropdown / select | 150-250ms | ease-out |
| Modal / drawer | 200-500ms | drawer curve for sheets, ease-out for centered modals |
| On-screen movement | 180-300ms | ease-in-out |
| Scroll storytelling | As needed | `power3.out` or scrubbed |

No `ease-in` on UI. Entrances: a small fade + 8-16px rise; bounce, large distances, or rotation only when the locked mood is playful. Hovers 100-150ms and subtle.

## Engines - one per project

- **GSAP + ScrollTrigger** - default for marketing pages (scroll reveals, staggers, sequenced hero timelines). Load from its official CDN or npm per the stack.
- **Motion (motion.dev)** - React components needing springs, layout or exit animation, gestures; or a registry component that already ships with it (retune its values to the lock rather than rewriting). Also works build-free as an ES module import; pin the major version.
- **anime.js** - only when a page needs SVG path morphing/drawing (e.g. a constructed logo mark), where its single bundle is lighter than GSAP plus morph/draw plugins. Not for plain reveals. Its scroll thresholds don't accept GSAP strings, and it doesn't auto-fire for elements already in view - trigger an initial check.
- Never load two engines for one effect each. The one tolerated pairing is GSAP for the page plus Motion inside pulled registry icons - state it.

**Reveal convention (no starter file needed):** mark elements `data-reveal` (and a parent `data-reveal-group` for staggered children). Write a small project-local script that, inside `gsap.matchMedia()`, animates `[data-reveal]` from `opacity: 0, y: 16` to rest over ~0.22s with `power3.out` when it enters the viewport, and staggers group children ~0.06s. In the reduced-motion branch, set everything to its end state. Without GSAP, an IntersectionObserver toggling a class with CSS transitions does the same.

## Marketing track - scroll storytelling

- **Scrubbed reveals** (`scrub: true`) - progress tied to scroll: a visual that assembles, a number that counts, a path that draws.
- **Pinned sections** (`pin: true`) - one sticky panel whose content advances; one or two per page at most.
- **Sequenced hero timeline** - ≤4 beats (context → headline → subhead + actions → the proof visual, animated as one composition).
- **Parallax depth** - small offsets; large ones read as gimmick.
- Match the locked feel: premium storytells slowly and minimally; playful can be energetic.
- Every storytelling effect shows its end state under reduced motion.

### Pointer-driven "alive" hero (a deliberate upgrade)

For playful or premium heroes that should feel alive while the visitor reads:
- **Lerp, never 1:1.** Track a target from `mousemove`, then each frame move current toward it (`current += (target - current) * 0.06-0.12`) and apply as `transform`.
- **Depth via differential strength** - background ~small, mid layer medium, foreground 10-25px max. It's a drift, not a drag.
- **Characters:** eyes or one focal detail track the pointer at higher strength than the body - cheapest "it sees you" effect.
- Bind to the hero; ease back to rest on `mouseleave`.
- Attach only under `(hover: hover) and (pointer: fine)`; skip entirely under reduced motion; never move text or click targets out from under the pointer.

## App-shell track - dashboards, settings, tools

No scroll narrative exists, so no ScrollTrigger. Motion answers what changed, what's about to happen, whether it's loading:
- **Panel/tab switches** - short crossfade or 8-12px directional slide matching navigation direction.
- **List/table entrances** - stagger rows on data load (same reveal convention, triggered by load, not scroll).
- **State changes** - animate the thing that changed (KPI value, status badge, added/removed row), not the layout.
- **Loading** - skeletons mirroring the real layout, never a lone spinner.
- **Draggable controls** - use the engine already present (GSAP Draggable with inertia and snap points; anime.js draggable with release spring). The drag itself tracks the pointer and isn't reduced-motion gated; the **release settle** is - critically damped, no overshoot, under reduced motion.

A project can need both tracks (public landing + authenticated app) - pick per screen.

## Physicality and gestures

- Pressables respond on pointer down (e.g. `scale(0.97)`, 120ms ease-out); never enter from `scale(0)`; popovers grow from their trigger, modals from center; enter and exit along the same path; `translateY(100%)` for size-relative travel; `blur(2px)` only to hide a double-exposed crossfade.
- Springs for drag, swipe, interruptible layout: `{ type: "spring", duration: 0.4, bounce: 0 }` for standard UI, `bounce: 0.2` for momentum releases.
- Respond on pointer down, commit on pointer up; Pointer Events with `setPointerCapture`; respect the grab point; hand release velocity to the spring; soft resistance at bounds.

## Performance and accessibility

- Animate only `transform` and `opacity`; never `transition: all`; in Motion under load, a full `transform` string beats `x`/`y`/`scale`.
- Reduced motion keeps opacity/color feedback and drops slides, springs, parallax, large movement.
- Translucent surfaces also honor `prefers-reduced-transparency` and `prefers-contrast: more` (more opacity, less blur, clearer borders).
- Gate hover motion behind `(hover: hover) and (pointer: fine)`.

## Lock it

Record in the style lock: feel (a concrete phrase), curves, durations (press, popover, panel, story), travel distances, frequency rules, reduced-motion behavior.

## Review before delivery

- Run the motion rows of the manual scan (quality-gates.md).
- Slow key animations to 25% (DevTools or multiplied durations).
- Check origins: popovers from triggers, modals from center.
- Spam toggles, tabs, toasts - motion retargets, never restarts.
- Toggle reduced motion - movement drops, state feedback stays.
- Test on touch - no pointer-only hover motion.
- The real question: does the interface feel faster, clearer, and more trustworthy because of the motion?
