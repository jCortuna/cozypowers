# Color system: structure, generation, naming

## What a system needs

| Ramp | Count | Notes |
| --- | --- | --- |
| Neutral | 1 | 80-90% of the interface: backgrounds, borders, body text |
| Accent | 1 | Brand hue; interactive and selected states |
| Status | 0-4 | danger, warning, success, info - only those the product shows |

A second accent hue never sits adjacent to the first; use the accent ramp's own steps for range.

## Step roles

| Role | Tailwind | Radix |
| --- | --- | --- |
| Page background | 50 | 1 |
| Subtle background | 50 | 2 |
| Component background | 100 | 3 |
| Component hover | 200 | 4 |
| Component active / selected | 200 | 5 |
| Subtle border | 200 | 6 |
| Border, separator | 300 | 7 |
| Strong border, focus ring | 400 | 8 |
| Solid fill | 500 | 9 |
| Solid fill hover | 600 | 10 |
| Low-contrast text | 700 | 11 |
| High-contrast text | 900 | 12 |

- **Radix steps are defined by role** - step 9 is the solid fill in every ramp and in both appearances (dark is a separate ramp with the same numbers), so component CSS never changes.
- **Tailwind steps are defined by lightness** - the mapping holds in light mode and inverts in dark (background at 950, text at 50), so components swap steps per appearance or read a semantic token.
- Match the project. For a new system, prefer role-defined steps. On Tailwind, keep 50-950 and put roles in the semantic tier. Tailwind's 11 steps cover 12 roles, so some double up; if subtle border and component hover must differ, you need 12 steps.

## Neutrals

Pure gray is a fine default - it sits under any accent and survives rebrands. Tinting toward the accent (a few percent of its vividness) is a stylistic choice, not a correction. Warm neutrals read approachable and editorial; cool ones technical and precise. Whatever you choose, hold it across the whole ramp - a warm gray border on a cool gray surface is visible. Neutrals carry the most roles, so never give them fewer steps than the accent.

## Status colors

Convention first: red danger, amber warning, green success (see cultural exceptions in usage-and-contrast.md).
- Keep every status hue distinct from the accent - a red brand needs a deeper crimson danger, checked side by side, or destructive and primary look identical.
- Status ramps usually need four roles (background, border, solid, text); build a full ramp only if the product uses the whole range.

## Starting from a brand color

1. **Which step?** A brand color for buttons and links belongs on the solid-fill step (500 / 9), so the fill renders the real brand color.
2. **Pinned or snapped?** Pin a contractually fixed brand color (the ramp builds outward; that step spaces slightly unevenly). Otherwise snap it onto an evenly spaced ramp - it almost always looks better.
3. A brand color that fails contrast behind white text is still the brand - put it where it lands and use a darker step for interactive fills. Never quietly darken the brand.

## A correct ramp

- Evenly spaced in perceived lightness (HSL lightness is not perceptual; its even steps bunch).
- Constant hue - every step recognizably the same color.
- Vividness peaks in the middle; ends nearly neutral (full vividness at the ends makes a glowing 50 and an inky 950).
- Denser at the light end - keep 50-200 close, 800-950 further apart.
- No adjacent steps indistinguishable on a calibrated screen - if so, drop a step.
- Ends stop short of pure black and white.

**Generate with a color library** (e.g. culori, colorjs.io, chroma.js): read the brand color in any notation, interpolate in a perceptual space (Lab/OKLab) through light, brand, and dark anchors, sample the steps, and emit the project's notation. Never hand-pick or interpolate a ramp in sRGB (muddy mid-steps). Example output shape:

```css
:root {
  --brand-50: #eff6ff;  --brand-100: #dbeafe; --brand-200: #bfdbfe;
  --brand-300: #93c5fd; --brand-400: #60a5fa; --brand-500: #3b82f6;
  --brand-600: #2563eb; --brand-700: #1d4ed8; --brand-800: #1e40af;
  --brand-900: #1e3a8a; --brand-950: #172554;
}
```

## Several hues together

Ramps must agree step for step, or a red button looks heavier than a blue one at the same step.
- **Match perceived lightness exactly** across hues.
- **Match vividness proportionally** - each hue has a different maximum. Set each ramp to the same fraction of its own maximum; copying a saturation number leaves yellows and cyans washed out.

## Dark mode

Reversal is the starting point, not the result. Swap semantic roles first:

```css
:root { --color-bg: var(--brand-50); --color-text: var(--brand-950); }
.dark { --color-bg: var(--brand-950); --color-text: var(--brand-50); }
```

Then tune: reduce accent vividness a step or two (confident on white is neon on near-black); add separation at the dark end (pale-distinct steps collapse as dark surfaces); recheck every pair (contrast isn't symmetric).

**Switching mechanism - pick one:**
- `prefers-color-scheme` alone when there's no theme toggle.
- A `.dark` class once users can override the system (the media query only sets the initial value).
- `light-dark()` for the least code when `color-scheme` is set - it reads `color-scheme`, not a class, so a class toggle must set `color-scheme` too.

```css
:root { color-scheme: light dark; --color-bg: light-dark(#ffffff, #172554); }
```

Mixing mechanisms half-themes the interface the moment someone overrides their system setting.

## Token tiers

```css
:root {
  /* Primitives - named by appearance, never used in components */
  --blue-500: #3b82f6;
  --neutral-200: #e5e7eb;
  --neutral-700: #374151;

  /* Semantics - named by role, the only tier components reference */
  --color-accent-solid: var(--blue-500);
  --color-border: var(--neutral-200);
  --color-text-secondary: var(--neutral-700);
}
```

Dark mode, white-label themes, and increased contrast all repoint the semantic tier and leave primitives and components untouched. A component-level tier (`--color-button-danger-bg`) is for genuine, intentional divergence only - one is an exception, twenty means missing roles.

## Role inventory

| Group | Roles |
| --- | --- |
| Surfaces | page, surface, raised (menus, popovers), sunken (inputs, wells), overlay scrim |
| Text | primary, secondary, disabled, inverse, on-accent |
| Borders | subtle, default, strong, focus ring, separator |
| Accent | subtle background, border, solid, solid hover, text |
| Status (each shipped) | subtle background, border, solid, text |

Separator and border are distinct roles even with the same value today: a separator divides content, a border encloses a control, and they diverge the first time inputs are restyled.

## Naming grammar

One shape: `--color-{role}-{variant}-{state}` - e.g. `--color-bg-surface`, `--color-text-secondary`, `--color-border-strong`, `--color-accent-solid-hover`.

| Concept | Use | Never mix in |
| --- | --- | --- |
| Foreground | `text` | fg, foreground, content, ink |
| Background | `bg` | background, surface-as-synonym, fill |
| Edge | `border` | stroke, outline, line |
| Brand | `accent` | primary, brand, theme interchangeably |

Reserve `primary` for one meaning - "most prominent of its group" - and call the brand `accent`.

| Anti-pattern | Problem | Instead |
| --- | --- | --- |
| `--color-blue-button` | Appearance at the semantic tier | `--color-accent-solid` |
| `--color-sidebar-gray` | Named after first usage | `--color-bg-surface` |
| `--color-light-gray` | A lie in dark mode | `--neutral-200` primitive |
| `--color-text-2` | Numbers carry no meaning | `--color-text-secondary` |
| `--color-gray-hover` | Hue + state, no tier | `--color-bg-surface-hover` |
| `--blue-500` in a component | Skips the theming seam | A semantic token |

**Tailwind v4:** names in `@theme` become utilities. Declare primitives and semantics together (`--color-brand-500`, `--color-accent-solid: var(--color-brand-500)`); templates use `bg-accent-solid`, and raw `bg-brand-500` in a component is the thing to flag. Opacity modifiers (`/50`) can't be contrast-checked statically - use solid tokens under text.

## Auditing an existing palette

1. Collect every literal - hex, `rgb(`, `hsl(`, `oklch(`, utility prefixes, plus SVG fill/stroke, chart configs, email templates.
2. Sort by perceived lightness within each hue family; duplicates surface as near-identical neighbors.
3. Collapse near-duplicates (closer than about one ramp step) into the most-used value - never average.
4. Assign each survivor a role; a color with no role is a missing token or a mistake - say which.
5. Count: more than one ramp per role means the palette outgrew its structure.

Report the inventory before changing anything. Consolidation changes screens nobody asked about, so it stays a proposal until accepted.
