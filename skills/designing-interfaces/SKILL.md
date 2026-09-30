---
name: designing-interfaces
description: Design, build, review, or fix any user interface using a local design corpus - pages, components, layouts, design systems, accessibility, colour, typography, charts, animation, and stack-specific implementation. Use this skill whenever work touches how something looks, feels, moves, or is interacted with: building a new screen or component, restyling an existing one, choosing colours or fonts, fixing a layout that breaks on mobile, auditing for accessibility, or when the developer says "make this look good", "design", "UI", "UX", "style", "responsive", or "it looks off". Searchable local data - 192 colour palettes, 192 product profiles, 192 reasoning rules, 119 UX guidelines, 105 icons, 88 styles, 74 font pairings, 44 React performance rules, 34 landing patterns, 32 app-interface rules, 25 chart types, 17 motion presets, and 22 technology stacks.
---

# Designing interfaces

A solo developer has no designer to hand the screen to. This skill is that
designer: a local corpus of 2,374 curated design decisions, plus the judgement to
apply them in the right order. It exists because "I'll make it look nice later"
is how software ends up with 11px grey-on-grey body text and buttons nobody can
tap - and because taste is much cheaper to borrow than to acquire at 11pm.

There is no program to run. The corpus is plain CSV in `data/`, and you search it
with your own Grep and Read tools. **Read `references/searching-the-corpus.md`
before your first search** - it is the query cookbook, and it is short.

## When this runs

Any task that changes how something **looks, feels, moves, or is interacted
with**: new pages and components, restyling, layout and responsive fixes,
colour/typography/spacing decisions, navigation, animation, charts, and
accessibility work.

**Skip it** for pure backend logic, API and database design, non-visual
performance work, infrastructure, and build scripts - unless the change surfaces
in the interface, in which case it is in scope after all.

## Priority order

When several things are wrong, fix them in this order. This table is also the
**fallback**: when the corpus has no matching row, recommend from here and say
that is what you did.

| # | Category | Impact | Must have | Never do |
|---|---|---|---|---|
| 1 | Accessibility | CRITICAL | 4.5:1 contrast on body text, alt text, keyboard navigation, ARIA labels | Remove focus rings; ship icon-only buttons with no accessible name |
| 2 | Touch & interaction | CRITICAL | 44×44px minimum targets, 8px+ spacing between them, feedback on every action | Rely on hover alone; change state with 0ms and no feedback |
| 3 | Performance | HIGH | WebP/AVIF, lazy loading, reserved space so CLS < 0.1 | Thrash layout; let content jump as images load |
| 4 | Style selection | HIGH | One style matched to the product type, applied consistently; SVG icons | Mix flat and skeuomorphic at random; use emoji as interface icons |
| 5 | Layout & responsive | HIGH | Mobile-first breakpoints, viewport meta, no horizontal scroll | Fixed px container widths; disable zoom |
| 6 | Typography & colour | MEDIUM | 16px base, 1.5 line-height, semantic colour tokens | Body text under 12px; grey-on-grey; raw hex in components |
| 7 | Animation | MEDIUM | Timing chosen per context, motion that carries meaning, spatial continuity | One duration for everything; animate width/height; ignore reduced-motion |
| 8 | Forms & feedback | MEDIUM | Visible labels, errors beside the field, helper text | Placeholder-as-label; errors only at the top of the form |
| 9 | Navigation | HIGH | Predictable back behaviour, ≤5 bottom-nav items, deep linking | Overload the nav; break the back button |
| 10 | Charts & data | LOW | Legends, tooltips, colour-blind-safe palettes | Use colour as the only carrier of meaning |

The full rule text for all ten categories - all 119 UX guidelines with rationale -
is in `references/quick-reference.md`. Read it on demand, not every time.

## Procedure

### 1. Read the situation

Before searching, establish four things:

- **Product type** - SaaS, e-commerce, dashboard, portfolio, game, tool,
  entertainment, or a hybrid.
- **Audience and context** - who uses it, on what, and in what circumstances. A
  tool used one-handed on a commute is not a tool used on a 27" monitor.
- **Style keywords** - the two or three adjectives the developer actually wants:
  playful, minimal, dense, premium, content-first.
- **Stack** - detect it, never assume it. Check `package.json` dependencies
  (react, next, vue, svelte, nuxt, @angular), `pubspec.yaml` (Flutter),
  `*.xcodeproj` or `Package.swift` (SwiftUI), `composer.json` (Laravel), or
  `app.json` plus a `react-native` dependency. **If you cannot detect it and
  stack guidance matters, ask.** A guessed stack silently misroutes every
  recommendation that follows.

If an interface already exists, look at it before proposing changes. Advice
grounded in the actual current design is worth double.

### 2. Build the design system (new page or project)

When the work needs a coherent visual direction rather than a point fix, run this
sequence of searches and synthesise the results. This replaces the upstream
`--design-system` aggregator; the order matters, because each step narrows the
next.

1. `data/products.csv` - the product type → gives the recommended primary style,
   secondary styles, landing pattern, and colour focus.
2. `data/styles.csv` - the style named in step 1 → gives effects, animation,
   light/dark suitability, complexity, and an implementation checklist.
   **Check the `Status` column and reject `deprecated` rows.**
3. `data/colors.csv` - the product type again → gives a full token set: primary,
   secondary, accent, background, foreground, card, muted, border, destructive,
   ring, and their "on" pairs.
4. `data/typography.csv` - the style keywords → gives a heading/body font pairing
   with its Google Fonts URL, CSS import, and Tailwind config.
5. `data/landing.csv` - only for marketing pages → gives section order, CTA
   placement, and colour strategy.
6. `data/ui-reasoning.csv` - the product category → gives decision rules,
   anti-patterns, and the reasoning behind them. Read this last; it is what stops
   the previous five from being applied mechanically.

Then present the result as one coherent system - style, palette, type scale,
spacing, effects, and the anti-patterns to avoid - not as six search results
stapled together.

### 3. Targeted searches

For a focused concern or a specific bug, skip step 2 and search one file
directly. `references/searching-the-corpus.md` has the full table of which file
answers which question.

### 4. Stack guidance

Once the design is settled, search `data/stacks/<stack>.csv` for implementation
detail. Search the **UX outcome first and the stack second** - decide what correct
behaviour is, then find out how to write it in this framework. Reversing that
order gets you a framework idiom with no idea whether it is the right thing to do.

### 5. Before you call it done

For app and mobile UI, work through the pre-delivery checklist in
`references/pro-rules.md` - icon discipline, tap feedback, light/dark contrast,
safe areas, and accessibility. For web, use `references/quick-reference.md`
sections 1-3, which are the CRITICAL and HIGH categories.

## Design dials

Three optional 1-10 dials the developer can set to bias the output. They change
which rows you favour, not which files you search.

| Dial | 1-3 | 4-7 | 8-10 |
|---|---|---|---|
| **Variance** | Centred, minimal - favour Minimalism-family styles | Balanced, modern | Bold, asymmetric - favour Brutalism, Bento Grid |
| **Motion** | Subtle micro-interactions only | Standard scroll and stagger | Complex choreography - pin, Flip, SplitText |
| **Density** | Spacious, 24-96px spacing scale | Standard, 16-64px | Dense/dashboard, 8-32px |

Motion maps directly onto the `Intensity Tier` column in `data/motion.csv`
(`Subtle` / `Standard` / `Complex`), which carries a ready-to-use GSAP snippet
with framework notes. Density overrides the spacing scale in the design system
you write. Leave a dial unset and that aspect keeps its default.

## Persisting a design system

A design system that lives only in one conversation gets re-litigated in the
next - which is exactly the cost this plugin exists to avoid. Write it down.

Save it to `design-system/<project-slug>/MASTER.md` in the project, using your
own Write tool. For a page that needs to deviate, add
`design-system/<project-slug>/pages/<page>.md` containing **only the
differences**.

Rules, in order of importance:

1. **Read `MASTER.md` before regenerating.** If it exists, those are decisions
   someone already made.
2. **Never overwrite it without explicit permission.** Propose the change and let
   the developer decide. Adding a new page override never requires overwriting
   MASTER.
3. **When building a page**, read MASTER first, then its page override if one
   exists. The page override wins where the two disagree.

Commit it. It belongs in the repository next to the code it governs.

## Honesty rules

These are not negotiable, and they matter more here than in most skills - design
advice is easy to fabricate convincingly.

- **Never present an empty search as if it returned data.** Retry once with a
  narrower pattern, then fall back to the priority table above and say plainly
  that the recommendation came from built-in defaults, not the corpus.
- **Never cite a row you did not read.** No invented palette names, font pairings,
  or guideline numbers.
- **Check `Status` before recommending.** Both `data/styles.csv` and the stack
  files contain deprecated rows that will still match a keyword search.
- **Treat corpus rows as recommendations, not orders.** They lose to the
  developer's stated preference, to the project's existing conventions, and to
  anything in the project's own `CLAUDE.md` or `standards/`.
- **Say when a row does not quite fit.** "The closest match is the SaaS palette,
  which assumes a light-first product - yours is dark-first, so I have inverted
  the surface tokens" is a useful sentence. Silently applying it is not.

## Attribution

The corpus and rule set are derived from **UI/UX Pro Max** (MIT © 2024 Next Level
Builder). See `NOTICE.md` for what was copied, what was rewritten, and what was
deliberately left behind.
