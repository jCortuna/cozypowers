---
name: better-layout
description: Improve layout structure - grouping with space, distinct controls, shared alignment edges, importance ordering, disclosure affordances, spacing between targets, edge insets, content-bleed vs floating controls, content-driven breakpoints, and resilience to translation, RTL, and clipping. Use when building or reviewing page/component layout, when something "looks cluttered", "feels unbalanced", breaks on resize or in another language, and as the layout pass inside better-interface reviews.
---

# Better Layout

Position, spacing, and alignment communicate hierarchy before anyone reads a word. Build that structure, then stress-test it: resize it, translate it, mirror it for RTL.

Write fixes in the project's styling system. The numbers here are **starting points for interfaces without an established density system**; where one exists, use it as written. Deliberate platform chrome, compact professional tools, and project tokens stay as long as they pass the stress tests.

Hit areas and focus belong to **better-accessibility**; radius, shadow, and animation to **better-ui**; line length and text spacing to **better-typography**.

## Principles

### Group with space, not lines

Space first, background shapes second, separator lines last (only where space can't carry the structure). The gap **between** groups must be at least **2x** the gap **within** one (e.g. 8px inside, 16px+ between), or grouping reads as noise. → [structure-and-spacing.md](structure-and-spacing.md)

### Controls look like controls

Every interactive element gets a background shape, a border, an underline, or a consistent placement zone. A control styled like adjacent text is invisible - and a non-interactive badge shaped like the buttons beside it collects dead clicks.

### Align to shared edges

Choose a few alignment edges and put everything on them; every stray edge is noise. One spacing step per level of subordination (16px is a sensible default). Use **logical properties** (`padding-inline-start`, `margin-inline-end`) for direction-dependent layout; physical left/right only for genuinely physical geometry.

### Order by importance

The most important content sits near the top and the leading edge; reading order flows top-to-bottom, leading-to-trailing. Think leading/trailing, not left/right. Don't overload the entry point: one primary action per view, secondary actions behind a menu beyond two or three.

### Hint at hidden content

Progressive disclosure needs a visible cue: the product's existing pattern, the next item peeking 16-32px past a scroll edge, or a labelled disclosure control. Hidden with no cue means it doesn't exist.

### Breathing room between targets

Without a density system: 12px between adjacent bordered/filled controls; 24px around borderless text or icon controls. Compact layouts may use less as long as hit areas don't overlap and controls stay distinct.

### Inset buttons from edges

In content layouts, full-width buttons stay inside layout margins with a visible radius (~16px inline on mobile). Edge-to-edge actions are fine when they're deliberate platform chrome that respects safe areas.

### Content bleeds, controls float

Backgrounds and media run to the viewport edge; text and controls stay within margins and safe areas (`env(safe-area-inset-*)`). Sticky chrome floats above content rather than blocking it.

### Hold structure until it breaks

Breakpoints come from content, not device presets. Keep the expanded layout while it genuinely fits; collapse late. Prefer container queries for components. Test smallest and largest sizes first.

### Plan for growth and clipping

Translated strings grow - short strings proportionally most, so one-word button labels are the riskiest thing on screen. No fixed width or height on text containers; let rows wrap; test with pseudo-localization and one long-string locale. Never park a critical action where resizing or scrolling can clip it.

## Before you finish

| Mistake | Fix |
| --- | --- |
| `margin-left` / `padding-right` in a localizable layout | `margin-inline-start` / `padding-inline-end` |
| Content-layout button touching the viewport edge | Inset within margins (keep intentional platform chrome) |
| Breakpoints at 768/1024 because they're defaults | Break where content stops fitting |
| Fixed-width text container sized to English | `max-width` + wrapping; pseudo-localize |
| Primary action at the clip-prone bottom of a pane | Sticky or stable chrome with safe-area padding |

## Reporting (standalone)

**Severity.** HIGH: blocks content or an action at a supported viewport. MEDIUM: harms hierarchy, reading order, or adaptability. LOW: isolated alignment/spacing polish.

**Verification.** Without a browser: logical vs physical properties, container/media queries against supported viewports, DOM order vs intended reading order. With one: every supported width, 200% zoom, RTL mirror. Unrun checks are **Not verified**.

**Format.** Grouped by principle, severity-ordered, one row per root cause with all locations:

| Severity | Location | Before | After | Why |
| --- | --- | --- | --- | --- |

End with **Block** (any HIGH) or **Approve**. Never approve uninspected coverage. Nothing found → "No actionable layout findings", plus verification.
