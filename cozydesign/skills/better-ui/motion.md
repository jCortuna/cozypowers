# Motion

## Transitions vs keyframes

| | CSS transitions | CSS keyframes |
| --- | --- | --- |
| Behavior | Interpolate toward the latest state | Fixed timeline |
| Interruptible | Yes - retarget mid-flight | No - restart |
| Use for | Hover, toggle, open/close | One-shot sequences (entrances, loading) |

```css
/* Good: clicking again mid-animation reverses smoothly */
.drawer { transform: translateX(-100%); transition: transform 200ms ease-out; }
.drawer.open { transform: translateX(0); }

/* Bad: closing mid-animation snaps or restarts */
.drawer.open { animation: slide-in 200ms ease-out forwards; }
```

## Scale on press

Always `0.96`, via a transition so an early release returns smoothly.

```css
.button {
  transition-property: scale;
  transition-duration: 150ms;
  transition-timing-function: ease-out;
}
.button:active { scale: 0.96; }
```

Tailwind: `transition-transform duration-150 ease-out active:scale-[0.96]`. Motion: `<motion.button whileTap={{ scale: 0.96 }}>`.

**Static prop:**

```tsx
const tapScale = "active:not-disabled:scale-[0.96]";

function Button({ static: isStatic, className, ...props }) {
  return (
    <button
      className={cn("transition-transform duration-150 ease-out", !isStatic && tapScale, className)}
      {...props}
    />
  );
}
```

## Skip animation on first render

```tsx
<AnimatePresence initial={false} mode="popLayout">
  <motion.span
    key={isActive ? "active" : "inactive"}
    initial={{ opacity: 0, scale: 0.25, filter: "blur(4px)" }}
    animate={{ opacity: 1, scale: 1, filter: "blur(0px)" }}
    exit={{ opacity: 0, scale: 0.25, filter: "blur(4px)" }}
  >
    <Icon />
  </motion.span>
</AnimatePresence>
```

Right for icon swaps, toggles, tabs, segmented controls - anything with a default state at load. Wrong for components that rely on `initial` for a first-time entrance (staggered hero, loading state) - it skips the entrance entirely. Check a full refresh after applying.

## Theme switch without the smear

```tsx
"use client";
import { useEffect } from "react";

export function DisableThemeTransitions() {
  useEffect(() => {
    const mql = window.matchMedia("(prefers-color-scheme: dark)");
    const onChange = () => {
      const style = document.createElement("style");
      style.append(document.createTextNode("*,*::before,*::after{transition:none !important}"));
      document.head.append(style);
      void document.body.offsetHeight; // force a style flush while the override applies
      requestAnimationFrame(() => requestAnimationFrame(() => style.remove()));
    };
    mql.addEventListener("change", onChange);
    return () => mql.removeEventListener("change", onChange);
  }, []);
  return null;
}
```

The forced reflow commits the new theme with transitions off; the double `requestAnimationFrame` removes the override after that paint. An in-app toggle needs the same wrap around its own flip (apply override → change theme → flush → remove). `next-themes` offers this as `disableTransitionOnChange`.

## Motion restraint

- **High-frequency interactions** (keystrokes, row hovers, tab switches in a work tool) get instant feedback or ≤150ms opacity/background transitions. Save expressive motion for rare moments (first view load, success, empty states).
- **Motion is never the only feedback** - the state stays visible without the animation.
- **Brief and precise beats prominent** - if a smaller, shorter animation says the same thing, use it.

```css
/* Good */
.row:hover { background-color: var(--surface-hover); transition: background-color 100ms ease-out; }
/* Bad: every hover replays an entrance */
.row:hover .row-icon { animation: bounce-in 500ms; }
```

## Staggered entrances

For infrequent entrances where order conveys hierarchy (page hero on first load, success state, empty state):

1. Split into logical groups (title, description, actions).
2. Stagger ~100ms between groups.
3. Titles may split into words at ~80ms.
4. Combine opacity, blur, and translateY.

```tsx
const item = {
  hidden: { opacity: 0, y: 12, filter: "blur(4px)" },
  visible: { opacity: 1, y: 0, filter: "blur(0px)" },
};

<motion.div initial="hidden" animate="visible" variants={{ visible: { transition: { staggerChildren: 0.1 } } }}>
  <motion.h1 variants={item}>Welcome</motion.h1>
  <motion.p variants={item}>A description of the page.</motion.p>
  <motion.div variants={item}><Button>Get started</Button></motion.div>
</motion.div>
```

CSS-only:

```css
.stagger-item {
  opacity: 0; transform: translateY(12px); filter: blur(4px);
  animation: fade-in-up 400ms ease-out forwards;
}
.stagger-item:nth-child(2) { animation-delay: 100ms; }
.stagger-item:nth-child(3) { animation-delay: 200ms; }
@keyframes fade-in-up { to { opacity: 1; transform: translateY(0); filter: blur(0); } }
```

## Exits

Attention is moving on - don't fight for it.

```tsx
/* Subtle (default) */
exit={{ opacity: 0, y: -12, filter: "blur(4px)", transition: { duration: 0.15, ease: "easeOut" } }}

/* Full, when spatial context matters (card returning to a list, drawer closing) */
exit={{ opacity: 0, x: "-100%", transition: { duration: 0.2, ease: "easeOut" } }}
```

- Small fixed offset, not full height; keep a hint of direction.
- Exit shorter than enter (e.g. 150ms vs 300ms).
- Remove instantly when motion adds no information, the interaction repeats often, or reduced motion is on.
- Never `translateY(-100%) scale(0.5)` over 400ms with `transition: all`.

## Contextual icon cross-fades

With Motion (import from `"motion/react"` if `motion` is installed, `"framer-motion"` if that is; follow neighboring imports if both):

```tsx
<AnimatePresence mode="popLayout">
  <motion.span
    key={isActive ? "active" : "inactive"}
    initial={{ opacity: 0, scale: 0.25, filter: "blur(4px)" }}
    animate={{ opacity: 1, scale: 1, filter: "blur(0px)" }}
    exit={{ opacity: 0, scale: 0.25, filter: "blur(4px)" }}
    transition={{ type: "spring", duration: 0.3, bounce: 0 }}
  >
    <Icon />
  </motion.span>
</AnimatePresence>
```

Without a motion library - both icons stay mounted:

```tsx
<div className="relative">
  <div className={cn(
    "absolute inset-0 flex items-center justify-center",
    "transition-[opacity,filter,scale] duration-300 ease-[cubic-bezier(0.2,0,0,1)]",
    isActive ? "scale-100 opacity-100 blur-0" : "scale-[0.25] opacity-0 blur-[4px]"
  )}>
    <ActiveIcon />
  </div>
  <div className={cn(
    "transition-[opacity,filter,scale] duration-300 ease-[cubic-bezier(0.2,0,0,1)]",
    isActive ? "scale-[0.25] opacity-0 blur-[4px]" : "scale-100 opacity-100 blur-0"
  )}>
    <InactiveIcon />
  </div>
</div>
```

The in-flow icon sets the size; the absolute one overlays it.

| Animate | Don't |
| --- | --- |
| Icons appearing on hover | Static navigation icons |
| State icons (play→pause, like→liked) | Decorative icons |
| Contextual toolbar icons | Always-visible icons |
| Loading/success indicators | Text labels beside icons |

Exact values: scale 0.25→1 (never 0.5 or 0.6), opacity 0→1, blur 4px→0, spring duration 0.3 with bounce 0.

## Performance

**Transition only what changes.** `transition: all` watches every property, animates things you didn't intend, and blocks optimizations.

```css
.button { transition-property: scale, background-color; transition-duration: 150ms; transition-timing-function: ease-out; }
```

Tailwind: `transition-[scale,background-color]`, not `transition-all`. `transition-transform` = transform, translate, scale, rotate.

**will-change** pre-promotes a layer to avoid first-frame stutter (Safari benefits most). Each layer costs memory - add only when stutter appears.

| Property | GPU-compositable | will-change worthwhile |
| --- | --- | --- |
| transform, opacity, filter | Yes | Yes |
| clip-path | Newer Chromium only | Rarely |
| top, left, width, height | No | No |
| background, border, color | No | No |

Never `will-change: all`.
