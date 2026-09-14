---
name: better-ui
description: UI polish details with exact values - concentric border radius, optical alignment, shadows vs borders, interruptible transitions, staggered entrances and subtle exits, contextual icon cross-fades, image outlines, scale on press, no animation on first load, no smeared theme switches, explicit transition properties, sparing will-change, icon stroke matched to text weight, one recolorable SVG per icon, and motion restraint. Use when an interface works but "feels unpolished", when building buttons, cards, icon buttons, toggles, or enter/exit animations, and as the UI-polish pass inside better-interface reviews.
---

# Better UI

Polish is a pile of small details that compound. This skill says which details are worth having and what values they take.

When reviewing, slow the interface down - what feels off at 10% speed is subtly wrong at full speed.

Keep the project's component library, tokens, and density, and match its motion language except where a rule below prescribes an exact interaction. **Values here are exact, not ranges**: `cubic-bezier(0.2, 0, 0, 1)` is not `cubic-bezier(0.4, 0, 0.2, 1)`, and `0.96` is not `0.95`.

Wrapping, font rendering, tabular numbers, and text spacing belong to **better-typography**; hit areas, focus, keyboard, ARIA, and reduced motion to **better-accessibility**; grouping, section spacing, breakpoints, and RTL layout to **better-layout**.

## Principles

### Concentric border radius

`outer radius = inner radius + padding`. Mismatched nested radii are the most common reason an interface feels off. → [surfaces-and-icons.md](surfaces-and-icons.md)

### Optical over geometric alignment

When geometric centering looks wrong, nudge optically - icon buttons, play triangles, asymmetric glyphs.

### Shadows for elevation, borders for structure

Where a border exists only to suggest depth, use layered transparent `box-shadow`. Keep borders that communicate structure or state: dividers, separators, selected and focus states.

### Interruptible animations

CSS transitions for interactive state changes (they retarget mid-flight); keyframes only for staged sequences that run once. → [motion.md](motion.md)

### Split and stagger entrances

For an infrequent staged entrance where order conveys hierarchy, split content into semantic chunks and stagger by ~100ms. Never stagger high-frequency interactions.

### Subtle exits

A small fixed `translateY` (e.g. -12px), not the full height. Exits are softer and shorter than entrances; `ease-out` both ways.

### Contextual icon animations

Animate appearing/changing icons with opacity, scale, and blur - exactly: scale `0.25 → 1`, opacity `0 → 1`, blur `4px → 0px`. With a motion library already installed (`motion` or `framer-motion` - match the import path the project uses), `transition: { type: "spring", duration: 0.3, bounce: 0 }`; bounce is always 0. Without one, keep both icons in the DOM (one absolutely positioned) and cross-fade with `cubic-bezier(0.2, 0, 0, 1)`. Never add a dependency just for this.

### Image outlines

A 1px low-opacity outline for consistent depth: `oklch(0 0 0 / 0.1)` in light mode, `oklch(1 0 0 / 0.1)` in dark. Pure black/white only - never slate, zinc, or a tinted neutral, which reads as dirt on the edge.

### Scale on press

`scale(0.96)` on `:active` for tactile feedback - always 0.96; below 0.95 feels exaggerated. Provide a `static` prop to disable it where motion would distract.

### No animation on first load

`initial={false}` on `AnimatePresence` keeps enter animations off the first render - but not where a component depends on its initial animation (a staggered hero, a loading entrance).

### No smeared theme switches

A theme flip transitions color, background, border, and shadow on nearly every element at once. Inject `*,*::before,*::after{transition:none !important}`, force a reflow, and remove it on the next frame.

### Transition only what changes

Name exact properties (`transition-property: scale, opacity`). Never `transition: all`. Tailwind's `transition-transform` covers transform, translate, scale, rotate.

### will-change sparingly

Only `transform`, `opacity`, `filter` (GPU-compositable). Never `will-change: all`. Add it when you see first-frame stutter, not preemptively.

### Icon stroke matches text weight

1.5px stroke beside regular (400) text, 2px beside semibold (600), 2.5px beside bold. One stroke convention and one icon library per surface.

### One SVG, recolored per state

Icons use `currentColor`; hover, selected, and disabled come from CSS color/opacity, never separate assets. Outline is the default variant; fill marks the active state.

### Motion restraint

High-frequency interactions get instant feedback, or at most a ≤150ms opacity/color transition. Every animated state change also leaves a static cue (color, icon, label) - motion is never the only channel.

## Before you finish

| Mistake | Fix |
| --- | --- |
| Icons look off-center | Nudge optically, or fix the SVG |
| Jarring staged entrance or exit | Stagger infrequent entrances; keep exits subtle |
| Theme toggle crossfades the page | Disable transitions for the swap, reflow, restore next frame |
| `transition: all` | Exact properties |
| First-frame animation stutter | `will-change: transform`, sparingly |
| Hairline icon beside bold text | Match stroke to text weight |

## Reporting (standalone)

**Severity.** HIGH: breaks an interaction, makes motion unusable, or leaves a state change visible only while animating. MEDIUM: visible inconsistency in surfaces, icons, or motion. LOW: isolated polish.

**Verification.** Without a browser: every state the component defines (hover, focus, active, loading, empty) and durations/easings from code. With one: walk each state; replay motion at 10% in the Animations panel. Unrun checks are **Not verified**.

**Format.** Grouped by principle, severity-ordered, one row per root cause with all locations:

| Severity | Location | Before | After | Why |
| --- | --- | --- | --- | --- |

End with **Block** (any HIGH) or **Approve**. Nothing found → "No actionable UI-polish findings", plus verification.
