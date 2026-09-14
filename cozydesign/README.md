# cozydesign

*Interfaces, but cozy.* Design-engineering skills for Claude Code, so generated UI stops looking generated. A companion plugin to [cozypowers](../README.md), living in the same marketplace and built to the same rules:

- **Zero executable code.** No hooks, no scripts, no starter JS. Markdown plus one manifest.
- **Zero network calls from the plugin.** Skills may *ask* the agent to look things up or fetch assets during your session, always with your approval.
- **Auditable.** Every "run the scanner" step from the originals became a written procedure the agent follows by hand.

These are clean-room recreations of community design skills. See [CREDITS.md](CREDITS.md) for the original authors and licenses.

## What's inside

| Skill | Use it for | From |
| --- | --- | --- |
| `design-engineering` | Motion decisions, easing and timing, component feel, gestures; UI reviews as Before/After/Why tables | Emil Kowalski |
| `animate` | Building one animation correctly, gate first, with ready recipes | Emil Kowalski |
| `web-design-engineer` | Checkpointed visual builds (design read, declared system, v0, critique), 25 style recipes, redesign protocol | ConardLi (Garden) |
| `landing-page-design` | Conversion structure and copy plus a strict visual system for landing pages | Elaya |
| `video-to-superprompt` | Turning a reference video into a build-ready recreation prompt | Meng To |
| `awwwards-quality-sites` | Art-directed, motion-led marketing sites with honest assets | Meng To |
| `better-accessibility` | Semantics, focus, keyboard, forms, announcements, reduced motion, zoom | Jakub Krehel |
| `better-layout` | Grouping, alignment, ordering, spacing, breakpoints, RTL, clipping | Jakub Krehel |
| `better-writing` | Interface copy: buttons, errors, empty states, settings | Jakub Krehel |
| `better-typography` | Type scale, wrapping, numerals, truncation, fonts, bidi | Jakub Krehel |
| `better-colors` | Color systems, tokens, measured contrast, dark mode, gamut | Jakub Krehel |
| `better-ui` | Polish details with exact values: radii, shadows, icons, press, exits | Jakub Krehel |
| `better-interface` | One consolidated review across all six `better-*` domains | Jakub Krehel |
| `interface-review` | Reviewing a branch, PR, or uncommitted change (invoke it yourself: `/interface-review`) | Jakub Krehel |
| `tastemaker` | Taste-grounded builds with a per-project style lock and personal profile; `study`, `audit`, `comps` verbs | codeswithroh |

## Installation

### From the marketplace

```bash
claude plugin marketplace add jCortuna/cozypowers
```

```bash
claude plugin install cozydesign@cozypowers
```

### Skills-directory (offline)

Copy just this folder into your personal skills directory:

```bash
cp -r cozydesign ~/.claude/skills/cozydesign
```

## Notes on overlap

Several sources hold opinions that differ slightly. The skill you invoke wins:

- **Press scale:** `design-engineering` and `animate` use `scale(0.97)`; `better-ui` uses exactly `0.96`.
- **Landing-page house style:** `landing-page-design` has strict font, gradient, and hero rules. If you've chosen a `web-design-engineer` style recipe or a `tastemaker` style lock, that governs look, while the landing-page structure, copy, spacing discipline, and ship checklist still apply.
- **Reviews:** `web-design-engineer` scores designs on five dimensions; `better-interface` runs an evidence-based, file-and-line review; `tastemaker audit` hunts for AI-generated tells. Pick the lens you need.

## Memory files tastemaker writes

`tastemaker` keeps plain files: `.tastemaker/` in your project (style lock, decision log, build log) and `~/.tastemaker/` in your home directory (profile and cross-project history). Delete them any time to reset. Add `.tastemaker/` to `.gitignore` if you don't want it committed.
