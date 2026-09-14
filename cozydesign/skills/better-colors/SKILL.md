---
name: better-colors
description: Build and review color systems - ramps with a job per step, primitive vs semantic tokens, role-correct token use, perceptual ramp generation, one color one meaning, one filled action per view, measured contrast (APCA and WCAG), gradient interpolation spaces, dark and increased-contrast variants, P3 gamut fallbacks, and format conversion. Use for any color question (palettes, tokens, contrast checks, dark mode, conversions), when colors "feel off", and as the color pass inside better-interface reviews.
---

# Better Colors

A color system is a small set of ramps, named by role, verified against the backgrounds they actually render on. Most color bugs are system bugs: a value picked in isolation, a token borrowed because it looked right, a pair nobody measured.

**Never report a contrast value you didn't measure, and never estimate a color you could compute.** Color is one of the few interface concerns with an exact answer - produce it (with the project's color library or a calculation you actually run, not by eye).

When contrast is *required* belongs to **better-accessibility**; surfaces, shadows, and icon color to **better-ui**.

## Principles

### Match the project's system

Reuse existing tokens and notation. A second notation added to fix one value makes the palette harder to reason about - consistent hex beats hex with scattered `oklch()`. For a **new** system, `oklch()` is the best default because its numbers behave perceptually. → [usage-and-contrast.md](usage-and-contrast.md)

### Ramps, not colors

One neutral ramp, one accent ramp, and only the status ramps the product actually renders. An unused `warning` ramp is maintenance for zero pixels. A second accent hue earns its place only when two things must be told apart at a glance.

### Every step has a job

A ramp isn't a gradient to pick from by eye. Each step exists for a role - page background, component hover, border, solid fill, body text. Don't generate steps no role uses. → [system.md](system.md)

### Primitives by hue, semantics by role

Primitives name values (`--blue-500`) and never appear in components. Semantic tokens name jobs (`--color-text-secondary`), point at primitives, and are the only tier components use. That seam is what makes theming possible.

### Use a token only in its role

Never borrow a token because its value happens to fit. A border token used as text color breaks the day borders get lighter. Missing role → add a token.

### Hold the hue across the ramp

A well-formed ramp: evenly spaced in **perceived** lightness; constant hue; vividness peaking mid-ramp and falling off at both ends; steps denser at the light end; ends short of pure black and white. Generate with a color library in a perceptual space.

### One color, one meaning

Use a hue for one purpose across the interface (treat anything within ~15° as the same color). If the accent means "interactive", accent-colored static text invites false clicks - and a neutral interactive element misleads just as badly. Color is never the sole carrier of meaning.

### Fill one action per view

When filled color signals primary emphasis, exactly one action gets it; peers stay neutral. Color goes on the background, not the label - accent text on a neutral button reads as a link. Several colored backgrounds are fine when they encode distinct states or categories. Don't recolor an established hierarchy that already signals emphasis another way.

### Measure the rendered pair, then report

Measure the foreground against the background it actually sits on (the nearest painted ancestor), not the page. When it fails, report the pair, the measured value, and the threshold missed - and leave the colors alone unless asked. After any change, remeasure.

### Choose a gradient's interpolation space

It's a look, not a correctness setting: `in oklab` for even brightness (best default); `in oklch` to stay vivid around the hue wheel (fixes a gray middle); the sRGB default darkens and mutes the midpoint.

## Before you finish

| Mistake | Fix |
| --- | --- |
| Raw value where a token exists | Reuse or add the role token, in project notation |
| Lone `oklch()` in a hex codebase | Keep established notation unless migrating |
| Primitive (`--blue-500`) in a component | Point a semantic token at it |
| Token named by appearance or first use | Name by role (`--color-accent-solid`, `--color-bg-surface`) |
| `--color-primary` = brand and `--color-text-primary` = body text | `accent` for brand; `primary` = most prominent of its group |
| Token used outside its role | Add a token for the missing role |
| Ramp built by varying HSL lightness | Rebuild on perceived lightness, constant hue |
| Evenly spaced across the full range | Tighten the light end so 50 and 100 read as two surfaces |
| Same saturation number across hues | Match each hue's proportion of its own maximum |
| Status hue colliding with the accent | Move it until destructive and primary read apart |
| Dark mode = mechanically reversed light palette | Reverse, then reduce vividness, widen dark-end separation, recheck pairs |
| `prefers-color-scheme` for some tokens, `.dark` for others | One switching mechanism throughout |
| Contrast "fixed" by changing hue | Change lightness |
| P3 color without sRGB fallback | sRGB first, then override in `@media (color-gamut: p3)` |

## Reporting (standalone)

**Severity.** HIGH: content unreadable, or a misleading semantic color. MEDIUM: noticeable theme, token, or gamut failure. LOW: isolated polish.

**Verification.** Without a browser: token values, gamut of every declared color, both theme blocks present, contrast computed from declared token pairs. With one: the actual rendered background (including opacity and images beneath), measured in light and dark. Failing pairs are reported, not repainted. Unrun checks are **Not verified**.

**Format.** Grouped by principle, severity-ordered, one row per root cause with all locations:

| Severity | Location | Before | After | Why |
| --- | --- | --- | --- | --- |

End with **Block** (any HIGH) or **Approve**. Nothing found → "No actionable color findings", plus verification.
