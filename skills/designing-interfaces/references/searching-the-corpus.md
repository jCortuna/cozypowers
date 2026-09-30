# Searching the corpus

The design corpus lives in `data/` as CSV. There is no search program to run —
you already have one. Use your **Grep** tool with `output_mode: "content"`, and
because every row occupies exactly one line, a hit returns a complete record.

```
Grep(pattern: "dashboard", path: "<skill>/data/products.csv",
     output_mode: "content", -i: true, head_limit: 10)
```

Three habits make this work as well as a ranked search engine:

- **Read the header first.** Line 1 of every CSV names the columns, in order.
  `Read(file, limit: 1)` — or `head -1` — then map the commas in a hit.
- **Widen, then narrow.** Start with one strong term. If you get too many rows,
  add a second term with `.*`: `"fintech.*trust"`. If you get none, drop to the
  single most distinctive word.
- **Search whole words when the term is short.** `-i: true` for case, and
  `\bnav\b` rather than `nav`, which also matches `navigation` and `navbar`.

## Query discipline

This is the part the upstream search engine's relevance ranking used to do for
you. Without it, the discipline has to be yours:

- **One dominant intent per search, 2–5 meaningful terms.** `keyboard focus
  modal`, not a whole audit checklist in one pattern.
- **Verify the hit before you use it.** Check that the row's product type,
  platform, and stack actually match the situation. A plausible-looking row for
  the wrong platform is worse than no row.
- **Retry once, narrower.** If a search comes back empty or off-topic, rewrite it
  once — a more specific term, or a different file. Do not cycle through a dozen
  unrelated keywords.
- **Then stop and say so.** If the retry also fails, fall back to the priority
  table in `SKILL.md` and *tell the developer that is what you did*. Never
  present a guess as a corpus match.

## The files

| Need | File | Search these columns | Example pattern |
|---|---|---|---|
| Product-type patterns | `data/products.csv` | Product Type, Keywords, Key Considerations | `entertainment\|social` |
| Visual styles | `data/styles.csv` | Style Category, Keywords, Best For, Aliases, AI Prompt Keywords | `glassmorphism` |
| Colour palettes | `data/colors.csv` | Product Type, Notes | `fintech` |
| Font pairings | `data/typography.csv` | Font Pairing Name, Category, Mood/Style Keywords, Best For | `playful\|creative` |
| UX rules | `data/ux-guidelines.csv` | Category, Issue, Description, Platform | `error summary` |
| App / native polish | `data/app-interface.csv` | Category, Issue, Keywords, Platform | `safe area` |
| Icons | `data/icons.csv` | Category, Icon Name, Keywords, Best For, Semantic Role | `hamburger\|drawer` |
| Charts | `data/charts.csv` | Data Type, Keywords, Best Chart Type, When to Use | `time-series\|trend` |
| Landing-page structure | `data/landing.csv` | Pattern Name, Keywords, Section Order, Aliases | `social proof` |
| Motion / GSAP presets | `data/motion.csv` | Category, Intensity Tier, Keywords, Trigger | `scroll reveal` |
| React/Next performance | `data/react-performance.csv` | Category, Issue, Keywords | `rerender\|memo` |
| Design reasoning rules | `data/ui-reasoning.csv` | UI_Category, Decision_Rules, Reasoning | `dashboard` |
| Stack implementation | `data/stacks/<stack>.csv` | Category, Guideline, Description | `suspense` |

**Stacks available** (`data/stacks/`): `angular`, `astro`, `avalonia`, `flutter`,
`html-tailwind`, `javafx`, `jetpack-compose`, `laravel`, `nextjs`, `nuxt-ui`,
`nuxtjs`, `react`, `react-native`, `shadcn`, `svelte`, `swiftui`, `threejs`,
`uno`, `uwp`, `vue`, `winui`, `wpf`.

## Two columns that will bite you

**`styles.csv` → `Status`.** Of 88 styles, only **50 are `active`**; 29 are
`supplemental` and **9 are `deprecated`**. A deprecated row carries a
`Replacement Domain` and `Replacement ID` — follow those instead. Never recommend
a deprecated style because it matched a keyword.

**`data/stacks/*.csv` → `Status` and `Applies To`.** Stack files carry deprecated
guidance too — old APIs kept for people maintaining old code. Check `Status` is
`active`, and check `Applies To` covers the version in the project, before
repeating any of it as advice.

## A pattern that matches everything is a bug

Some columns hold the same value in every row — `icons.csv` → `Allowed Contexts`
is `decorative|meaningful|interactive` for all 105 icons. Searching `decorative`
there returns the entire file and tells you nothing. If a search returns most of
a file, the pattern is not selective: search a column that actually varies
(`Icon Name`, `Keywords`, `Semantic Role`) or move to a different file.

## Reading a wide row

`styles.csv` has 29 columns and rows run past 1,500 characters, so a raw Grep hit
is a wall of text. When a hit is the one you want, read it properly:

```
Read(file: "<skill>/data/styles.csv", limit: 1)   # the header
Grep(pattern: "^42,", path: "<skill>/data/styles.csv", output_mode: "content")
```

Every file's first column is `No`, a stable row number, so `^42,` re-fetches a
specific row exactly. Use it to pull a row back without re-running a fuzzy search.

## Accessibility searches

Accessibility is the one area where a loose search actively misleads, because
almost every row mentions it. Search **one observable outcome at a time**, and
never accept a generic accessibility hit as an answer for a specific criterion:

| Looking for | Pattern | File |
|---|---|---|
| Form error handling | `error summary\|inline validation` | `ux-guidelines.csv` |
| Focus obscured by sticky UI | `focus.*obscur\|sticky.*focus` | `ux-guidelines.csv` |
| Drag-only interactions | `dragging\|drag.*alternative` | `ux-guidelines.csv` |
| Authentication barriers | `authentication\|password manager` | `ux-guidelines.csv` |
| Decorative vs meaningful icons | `decorative` | `app-interface.csv`, `ux-guidelines.csv` |
| Icon-button naming | `accessible.*label\|icon.*button` | `icons.csv`, `ux-guidelines.csv` |
| Colour contrast | `contrast` | `ux-guidelines.csv`, `app-interface.csv` |

Search the **semantic outcome first**, then the stack for implementation detail —
in that order. `"badge chip label wraps"` against `ux-guidelines.csv` tells you
what correct behaviour is; `"chip badge overflow"` against
`stacks/html-tailwind.csv` tells you how to write it. Reversing the order gets you
a framework idiom with no idea whether it is the right thing to do.

## When the corpus has nothing

Say so. The priority table in `SKILL.md` is the built-in fallback, and it is a
good one — but label it as such: *"no palette row matched fintech-for-teenagers,
so this uses the general SaaS defaults."* An honest fallback is useful. A
fabricated citation is not.
