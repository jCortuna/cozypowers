# Components, patterns, and stacks

**Tastemaker directs; it doesn't fabricate what a production-grade library already ships.** Hand-rolled charts, bento grids, pricing tables, and dropdowns are reliable "AI-built" tells. Pull the part, then spend the design effort restyling it to the locked tokens and unifying everything pulled - that coherence pass *is* the design work.

Adding a dependency or running an installer changes the developer's project - propose it and get a yes first.

## 1. Detect the stack first

Check `package.json` (React? Next? Tailwind v3 or v4?), `components.json` (shadcn already set up?), and the actual file types.

| Stack | What applies |
| --- | --- |
| React + Tailwind + shadcn | Everything below |
| React + Tailwind, no shadcn | shadcn init first (additive) - confirm on an established repo |
| React, no Tailwind | Registries won't drop in; port the *pattern* by reading the source |
| Static HTML/CSS | **No registry installs.** Motion via ES-module CDN still works. Write the CSS yourself, informed by good registry components, and say you ported a pattern |
| Vue / Svelte / React Native | shadcn MCP tooling supports some; Tailwind registries generally don't |
| SwiftUI / Flutter / native | No registries; direction, motion principles, and quality rules still apply |

Never emit an install command for a stack that can't consume it.

## 2. Behavioral primitives (hard to get *right*)

Decision order: identify the task → check existing dependencies and imports → extend a healthy existing library → otherwise pick one default → hand-roll only if simple, static, or dependencies are forbidden. Don't replace a working library just because a different default exists; flag it.

| Task | Default |
| --- | --- |
| Dialogs, popovers, menus, selects | Base UI (or the repo's existing headless layer) |
| Command palette | cmdk |
| Toasts | Sonner |
| One-time codes | input-otp |
| React springs, layout/exit animation, gestures | Motion |
| Simple hover, press, reveal | CSS transitions or GSAP |
| Changing numbers | NumberFlow |
| Charts | A registry chart (e.g. bklit) or Recharts - **never hand-rolled** |
| Streaming real-time charts | Liveline |
| Drag and drop | dnd kit |
| Long lists and tables | Virtuoso |
| Shared client state | Zustand |
| Conditional classes / variants | clsx / cva |
| Next.js theme switching | next-themes |

Catch: custom dropdowns with manual focus handling, toasts built from modals, number tickers that replace text each render, 1,000-row tables rendered directly, drag systems without keyboard support or pointer capture, nested-ternary class strings.

## 3. Visual components and blocks (hard to make *look finished*)

**shadcn-compatible registries** install editable source (React + Tailwind):

| Registry | Pull with | Best for |
| --- | --- | --- |
| shadcn/ui | `npx shadcn@latest add <name>` | Foundation primitives and official blocks |
| Watermelon UI | registry URL `https://registry.watermelon.sh/r/{name}.json` (note the `/r/` path) | Breadth - 260+ components and full blocks |
| KokonutUI | `@kokonutui` → `https://kokonutui.com/r/{name}.json` | Designed components with motion character (Tailwind v4) |
| bklit UI | `@bklit` → `https://ui.bklit.com/r/{name}.json` | Charts: area, bar, line, pie, scatter, candlestick, sankey, heatmap |
| lucide-animated | `https://lucide-animated.com/r/{name}.json` | Default icons on this stack - animated Lucide set (MIT, uses Motion) |
| itshover | `https://itshover.com/r/{name}.json` | Second icon source - brand and tech marks (Apache 2.0) |

Register namespaces once in `components.json` under `"registries"`. Two traps: **`shadcn init` overwrites the token block** with its own neutrals - reapply the lock afterwards, and point its `--chart-*` and `--sidebar-*` tokens at the locked palette; some items **prompt interactively** and hang non-interactive runs - pass `--yes`.

**MCP component search** (shadcn MCP server, 21st.dev) only if actually connected this session; 21st.dev needs its own API key - never make a build depend on it. Figma/Framer/Webflow-only block libraries can be recommended to the developer but can't be installed by an agent.

**Precedence:** what's already in the repo → shadcn base → Watermelon for breadth → KokonutUI for character → bklit for anything chart-shaped → lucide-animated then itshover for icons → MCP search to discover → hand-roll only when nothing applies.

**Icons:** on React + Tailwind + shadcn, animated registry icons first (one source per concept, never both for the same icon). Elsewhere, a static open set via Iconify (Lucide, Tabler, Phosphor, Heroicons, Material Symbols, Iconoir, Solar, Carbon, MingCute, Fluent - all attribution-free); vary which set by mood across projects rather than always defaulting to Lucide. **One icon family per project**, recolored to the locked accent.

**Shader backgrounds (Paper Shaders):** `@paper-design/shaders` (vanilla, zero-dependency; pin an exact version when loading from a CDN) or `@paper-design/shaders-react` - real animated GPU shaders, Apache-2.0, no attribution. The honest upgrade over a hand-rolled canvas blob loop. Mesh gradient is the simplest reliable first choice (no noise texture needed); vary the effect by mood:

| Mood | Effects |
| --- | --- |
| Premium | Mesh Gradient, Static Radial Gradient |
| Warm | Waves, Neuro Noise |
| Technical | Grain Gradient, Warp |
| Playful | Metaballs, Dot Orbit |
| Elegant | Smoke Ring, God Rays |

Feed colors from the locked palette. **Never put a shader directly behind text:** full-bleed behind the whole hero at ~0.3-0.6 opacity, with a radial vignette in the locked background color (opaque at the text center, transparent at the edges), and check the rendered headline contrast. Speed 0 (one static frame) under reduced motion.

## 4. The director's job

Six components from six registries stacked together is *worse* than hand-rolling - mixed radii, three icon families, four shadow depths, competing motion.

1. **Restyle every pulled component to the lock** - its origin colors, radii, and shadows are unfinished work.
2. **One icon family** - convert a block's bundled static icons to the project's set.
3. **One radius, shadow, and spacing scale** - from the lock, not whichever component arrived first.
4. **One motion feel** - retune durations and easings to the lock.
5. **Delete what the brief can't fill** - a block's stat row, logo wall, or testimonial slot gets cut, not filled with invented content.
6. **Structure still comes from the arc and macrostructure** - don't let a block's built-in section order become the page.

Verify with the coherence rows of the manual scan (quality-gates.md). **Say what was pulled and from where** in the handoff ("pricing from Watermelon, restyled; chart from bklit"), and say when a registry *didn't* apply and a pattern was ported by hand.

## 5. Patterns by screen type

### Show, don't tell (overrides every pattern)

| Instead of | Show |
| --- | --- |
| Feature card: heading + two sentences | A small mockup of that feature's UI, one-line caption |
| "Fast / real-time analytics" | An actual chart in the locked palette |
| "Simple 3-step setup" bullets | Three numbered visual panels, each a screen state |
| "See the difference" prose | A literal before/after split or slider |
| A stat buried in a sentence | A big number + one-word label tile |
| "Works with your stack" paragraph | The integration logo grid |
| "Trusted by teams" | A real logo strip or a real testimonial |
| Abstract benefit (calm, focus, security) | An illustration of that concept |

- Every chart needs a one-line caption stating what it shows, tied explicitly to nearby numbers.
- **Proof has a higher floor than feature cards:** a real supporting visual (annotated capture, real chart, constructed diagram, before/after) doing the work. Small label-plus-icon cards floating in empty space fail; swap to an archetype with more surface area or one larger real visual.

### Column balance

When two columns differ noticeably in height, choose deliberately: vertically center the shorter one; fill the remaining height with a real element (stat, short testimonial, small illustration, secondary note); or cap the taller column. Never leave the short side trailing into dead space.

### Section separation

One mechanism for the whole project, at every boundary: alternating surface tint (dense marketing pages), hairline dividers (projects already using hairlines instead of shadows), or generous fixed padding alone (only works at the weighted section-padding tiers). Record it in the lock.

### Landing / marketing

Shape comes from the macrostructure (structure.md); inside it: hero discipline (hero-and-copy.md), workflow steps and detailed proof below the fold, each section given room to be its own moment, and no stacks of identical icon + heading + line cards.

### App shell (dashboards, internal tools)

- **Frame:** persistent sidebar (grouped past ~7 destinations; collapses to icons, not hidden) + contextual topbar (breadcrumb, search, account - never duplicating the sidebar) + a content area with one job per screen.
- **Chrome mapping (lock it once):** sidebar on Surface (or inverted in dark-native projects, deliberately); content on Background; topbar shares Background with a hairline; active nav item is the one place Primary gets a dedicated treatment (filled row *or* primary left-border - one treatment everywhere); inactive hover is a subtle surface shift, never active-weight; breadcrumbs muted except the current segment. Every new pairing goes through the color contract.
- **Denser than its marketing page** - more rows visible, tighter rows, smaller data type. That's the mood applied to a tool, not a contradiction.
- Lead with the one number or status people open the app to check; group related metrics; design empty, loading, error states explicitly; build the full action path (check, change, see the result, recover); all control states present.

### Data tables and collections

Filtering, sorting, bulk actions, and visible selection in the first pass. Comparison jobs want tables or compact rows, not identical card grids. Separate empty, no-results, and error messages. Virtualize past a few hundred rows; sticky headers when columns matter. Don't animate rows during scanning - only occasional inserts/removals.

### Pricing

Three tiers by default. Highlight one tier with a border or background shift, not only a ribbon. Keep the billing toggle next to the prices. A tall headline column beside short tier cards is the column-balance case.

### Onboarding

Mirror the real step list (don't compress five necessary steps into a "clean" three). Show steps remaining. First-run empty states teach by example (pre-filled samples) where possible.

### Empty states

Explain what will appear and offer one clear action. A good place for the project's anchor illustration.

### About / company

Statement → concept illustrations → real credibility stats → real logo strip → values grid → team → physical presence in real photography. Deliberately mix illustration (mission, values) with photography (offices, real people) - ask which sections should feel real vs conceptual. Keep stats (3-4) and logos (5-6) restrained.

### Settings and forms

Group by relatedness, not alphabet or schema. Destructive actions visually separated and never styled like safe ones. Save state unmistakable (clear autosave confirmation or an explicit save).

## 6. Tokens per stack - one source of truth

- **React/Next + Tailwind:** palette, radius, spacing in the Tailwind theme with role names (`surface`, `accent`); fonts via `next/font` wired to CSS variables; repeated patterns as components. GSAP via npm with ScrollTrigger registered once and driven through `useGSAP` for proper cleanup.
- **Vue/Nuxt:** Tailwind config or a CSS custom-property file; GSAP registered in a composable, created in `onMounted`, killed in `onUnmounted`.
- **Plain CSS:** tokens on `:root` with a `[data-theme="dark"]` override; every component uses `var(--token)`. GSAP from its official CDN.
- **SwiftUI:** `Color`/`Font` extensions or asset-catalog colors mirroring lock roles.
- **Flutter:** `ThemeData`/`ColorScheme` built from the lock at the app root.

A literal hex or magic spacing number in component code means the token setup was bypassed - add it to the source instead.

## 7. Prototype variants (when direction is genuinely uncertain)

For a hero, pricing layout, dashboard card, onboarding step, empty state, toast, command palette, table interaction, or motion-heavy explainer where guessing is costly - not for routine wiring or small fixes.

- **2-3 variants** (4 only for a wide design space), each differing on a named axis: layout, density, hierarchy, interaction model, or motion. **Color swaps are not variants.**
- Each uses locked tokens and real content and is shippable on its own - no dead controls or lorem.
- Write a small direction table first (variant · axis · bet · cost); merge any two that differ only by color.
- **Picker:** one variant at a time at real size in realistic context; a neutral floating pill (bottom center unless it covers the work); number keys switch, arrows cycle, `R` replays entrance motion; variant stored in the URL (`?v=2`); exactly one active item with `aria-current="true"`; switching is instant (a repeated action gets no animation). The picker's own styling is harness chrome, not product tokens.
- **Verify before showing:** open it, flip through every variant by mouse and keyboard, replay motion, check the console, check 390px and desktop, confirm reduced motion.
- **Promote only the chosen variant**, delete the picker unless asked to keep it, and log kept/rejected in the decision log.
