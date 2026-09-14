---
name: better-accessibility
description: Make interfaces accessible - native semantics, visible focus, full keyboard support, focus trapping, hit areas, labelled forms, announced errors and live updates, alt text, reduced motion, zoom and reflow. Use when building or reviewing any interactive UI for accessibility, when the developer mentions a11y, WCAG, screen readers, keyboard navigation, or focus, and as the accessibility pass inside better-interface reviews.
---

# Better Accessibility

Most accessibility is free if you use the platform: native elements come with keyboard support, real labels announce themselves, and a visible focus ring is one CSS rule.

Write every fix in the project's own styling system, using the exact values below rather than similar-looking substitutes.

A review is two walks: **keyboard only** (every flow completes without a mouse), then **screen reader** (every control announces a name, a role, and its state). When unsure, prefer the platform default to a custom rebuild, and remove ARIA rather than add it.

Contrast measurement belongs to **better-colors**; text sizing and iOS input zoom to **better-typography**; RTL spatial layout to **better-layout**.

## Principles

### Native elements first

Don't use ARIA when a native element exists. `<button>` for actions, `<a href>` for navigation, never `<div onClick>`. Real links must keep Cmd/Ctrl/middle-click. Bad ARIA is worse than none. → [screen-readers-and-semantics.md](screen-readers-and-semantics.md)

### Visible focus

Style `:focus-visible`, not bare `:focus`. Prefer the browser's own indicator (adding only `outline-offset` keeps it). A custom ring uses a project focus token or explicit color, at least a 2px solid perimeter (or equivalent area), verified against every color it crosses - `currentColor` included. Never `outline: none` without a verified replacement; keep system colors in forced-colors mode. → [keyboard-and-focus.md](keyboard-and-focus.md)

### Full keyboard support

Every pointer interaction has a keyboard path, following the ARIA Authoring Practices: Escape closes overlays, arrows move within composite widgets, Tab moves between widgets, Enter/Space activate. Only `tabindex="0"` (join tab order) and `tabindex="-1"` (programmatic focus) - never positive values. Composite widgets use roving tabindex.

### Trap and restore focus

Modals make the background `inert`, move focus inside on open, return it to the trigger on close, and set `overscroll-behavior: contain`.

### Hit areas

WCAG 2.5.8 AA floor: 24x24 CSS px (or one of its exceptions). Aim for 44x44 on touch and 40x40 on desktop where density allows. Grow the hit area with a pseudo-element when the visual should stay small. Extended areas never overlap; decorative overlays get `pointer-events: none`. → [targets-motion-zoom.md](targets-motion-zoom.md)

### Label and type every control

Every input has `<label for>` or a wrapping `<label>`; a placeholder is never the label. Label and control share one hit target. Add `autocomplete` with a meaningful `name`, plus `type`/`inputmode` for the right keyboard. Never block paste. → [forms.md](forms.md)

### Errors that announce

Submit stays enabled until the request starts, then disables with a spinner beside its original label. Validate on submit; set `aria-invalid="true"`, point `aria-describedby` at inline error text, focus the first invalid field. Native `disabled` for genuinely unavailable controls; `aria-disabled="true"` only when it must stay focusable - then block activation in code and style it explicitly.

### Accessible names everywhere

Icon-only buttons need a descriptive `aria-label`. Visible label text must be contained in the accessible name. Decorative elements get `aria-hidden="true"` - never on anything focusable.

### Never color alone

Status gets a redundant cue: icon, text, or underline. Identify which contrast requirement applies and have better-colors measure the rendered pair; report failures without changing colors unless asked.

### Honor reduced motion

Make motion opt-in with `@media (prefers-reduced-motion: no-preference)`. Under reduced motion, slides and scales become opacity crossfades; parallax and autoplay stop entirely. Regardless of preference: autoplaying media has a visible pause control, and toasts with an action or error stay until dismissed.

### Announce dynamic content

Field-specific validation → `aria-describedby`. Non-urgent untied updates (toasts, result counts) → a polite region, `role="status"`. Urgent untied errors → `role="alert"`, and nothing else. Repeated polite updates need a stable, empty region rendered before its text changes.

### Alt text by purpose

Decorative → `alt=""`. Informative → the meaning. Functional → the action (`alt="Search"`, not "magnifying glass").

### Structure is navigation

Descriptive headings forming a coherent outline, one `<h1>`, no skipped levels. One visible `<main>`. A "Skip to content" link first when chrome precedes main content. Anchored headings get `scroll-margin-top`.

### Survive zoom

Works at 200% zoom; reflows at 320px width without horizontal scroll. `min-height`, not fixed `height`, on text containers. Prefer `rem` breakpoints where the codebase allows. Never cap zoom in the viewport meta.

## Before you finish

| Mistake | Fix |
| --- | --- |
| Custom focus color assumed fine everywhere | Verify against every adjacent color and in forced-colors mode |
| Repeated polite updates announced inconsistently | Keep a stable empty status region; update its text |
| `assertive` region for a routine toast | `polite`; reserve assertive for errors |
| `aria-hidden="true"` on something focusable | Remove it, or make the element unfocusable |
| Submit disabled until the form is valid | Keep enabled; validate on submit; focus first error |
| Hover style stuck after tap | Gate hover behind `@media (hover: hover)` |
| Tooltip on a natively disabled control | Visible reason beside it, or `aria-disabled` so it stays focusable |

## Reporting (standalone)

**Severity.** HIGH: prevents a task, hides content from assistive tech, or is systemic. MEDIUM: makes an interaction meaningfully harder. LOW: isolated polish.

**Verification.** Without a browser: accessible names on all interactive elements, keyboard handlers on non-native controls, focus styles, reduced-motion guards, labels bound to inputs. With a browser: tab through each flow, read computed names/roles from the accessibility tree, confirm a visible indicator at every stop, run an automated audit. Anything not run is **Not verified**.

**Format.** Findings grouped by the principle violated, ordered by severity, one row per root cause listing all locations:

| Severity | Location | Before | After | Why |
| --- | --- | --- | --- | --- |

Location is `path/to/file:line`; Why names the principle and user impact. End with **Block** if any HIGH remains, otherwise **Approve** (remaining rows are work to do). Never approve coverage you didn't inspect. Nothing found → "No actionable accessibility findings", plus verification.
