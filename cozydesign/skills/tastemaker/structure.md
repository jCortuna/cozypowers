# Structure: arc, macrostructure, archetypes, rotation

Three questions, answered in this order:

1. **Why does each section exist, and in what order?** - the narrative arc.
2. **What shape is the whole page?** - the macrostructure.
3. **What does each section look like?** - the component archetypes.

A page can vary its shape perfectly and still have no throughline; variety and coherence are different properties, and a real page needs both. Skip this file for app shells (dashboards, tools behind a sidebar) - the sidebar-plus-topbar frame is their structure.

## 1. Narrative arc

Grounded in established conversion frameworks (StoryBrand's customer-as-hero, Problem-Agitate-Solution, and the converged SaaS sequence hero → problem → solution → how it works → proof → CTA).

| Beat | Job | Typical archetypes |
| --- | --- | --- |
| **Hook** | The promise (the hero, per hero-and-copy.md) | Any H# |
| **Problem / stakes** | What's specifically broken, and what happens if nothing changes - never "teams struggle with X" | Prose + a visual of the broken state or a before/after; sometimes folded into the hero subhead |
| **Solution / mechanism** | How the product fixes it - *shown*, not asserted | F1, F2, F5 |
| **How it works** | A handful of concrete steps (3-5), not a manual | F4, F3, F6 |
| **Proof** | Real logos, quotes, numbers - never invented | P1-P4 |
| **Close** | The ask, echoing the hook's promise | C1, C2, C4 |

- **At least four distinct beats; five is the default.** Hook → proof → close skips the part that persuades.
- "How it works" may merge into Solution for a simple product. Any merge or skip is a **stated** choice tied to the brief, never a section that quietly didn't get built.
- **Self-check:** read top to bottom - who is it for and what's the promise? what's wrong? how does this fix it? why believe it? what now? A section serving none of these is a gap.

## 2. Macrostructures (public/marketing pages)

Pick **one by name**, deliberately - reaching for the first shape that comes to mind always yields the generic one.

| # | Name | Shape | Reach for when | Mood affinity |
| --- | --- | --- | --- | --- |
| 1 | **Feature Stack** | Hero, then full-width alternating text/visual bands - never a 3-up card grid; every band leads with a real visual | 3-6 capabilities that each deserve a real visual | Any; common for premium/technical SaaS |
| 2 | **Bento Showcase** | Asymmetric mixed-span tiles, each a small live-looking UI fragment | Many small features better seen at a glance | Premium, technical, playful |
| 3 | **Editorial Index** | Masthead, numbered/categorized list, generous type, hairline rules | Portfolios, agencies, publications | Elegant, premium |
| 4 | **Long-Scroll Narrative** | The arc told one full section at a time, scroll-linked reveals | A non-obvious product that needs explaining; manifestos; launches | Any |
| 5 | **Stat-Led** | A dominant real number (or tight real metric row) is the spine | The story is genuinely quantitative *and the numbers are real* | Premium, technical |
| 6 | **Gallery Grid** | Real imagery fills the page; minimal chrome | Commerce, food, travel, photography, physical product | Elegant, warm, playful |
| 7 | **Product Demo / Workbench** | Hero is the product in use; page organized around doing | Dev tools and apps where seeing it work is the argument | Technical, premium |
| 8 | **Split Diptych** | Persistent statement column beside a scrolling content column, or a hard split fold | Studios, single-voice products, art-directed feel | Elegant, premium, playful |
| 9 | **Conversational FAQ** | Real audience questions answered directly, proof and CTA folded in | Trust gaps, regulated or high-consideration products | Warm, technical |
| 10 | **Manifesto** | Type-forward, few images, big statements; restraint is the design | Opinionated launches, studios staking a position | Elegant, premium, technical |
| 11 | **Catalogue** | Structured, near-tabular listing with editorial care | Many SKUs, pricing-as-page, changelogs, specs | Technical, elegant |
| 12 | **Poster Fold** | One full-bleed art-directed first screen; quieter page below | An event, fashion, a single launch image | Elegant, playful, warm |

- **Match shape to argument:** "look how many people use it" → Stat-Led; "look at the work" → Gallery Grid; "let me explain why this matters" → Long-Scroll Narrative.
- **Vague brief:** offer three categorically different shapes (one grid-led, one document-led, one poster-led) rather than defaulting.
- **Honesty:** Stat-Led, Catalogue, and every proof band use real figures, logos, and quotes - or a labelled "metric to confirm" placeholder. No real figures → pick a shape that doesn't need them.

## 3. Component archetypes

Carry forward only the IDs you pick. Typical page: one nav, one hero, one footer, one or two features, one proof, one CTA, a section-head treatment. No two sections on a page use the same archetype.

### Navigation - N#

- **N1 Minimal wordmark** - wordmark left, ≤2 links + one action. ⚠️ The most recognized AI nav when used reflexively; only for genuinely minimal pages.
- **N2 Balanced product bar** - wordmark · centered 3-6 links (some with panels) · sign-in + filled CTA; frosts on scroll.
- **N3 Floating pill** - content-sized detached pill with blur; needs a surface beneath (a 95%-wide "pill" is just a bar).
- **N4 Editorial masthead** - larger centered wordmark, thin issue/date line, rule beneath.
- **N5 Side rail** - thin vertical strip, rotated wordmark, section indicators; menu trigger on mobile.
- **N6 Command bar** - visible search pill or ⌘K spotlight of grouped destinations.
- **N7 Announcement + retract** - dismissible promo banner that retracts on scroll down.
- Knobs: position (static · sticky · frost) · link density · action style.
- Routing (default → alternatives): premium N2 → N4, N3, N1 · warm N2 → N7, N3 · technical N2 → N6, N5, N1 · playful N7 → N3, N2 · elegant N4 → N5, N1, N3.

### Hero - H#

- **H1 Statement fold** - one large promise, one action; type is the visual.
- **H2 Split demo** - headline, lede, CTA beside a real product capture or built UI fragment (maybe tilted 1-3° or clipped by the viewport).
- **H3 Photographic fold** - one real full-bleed photograph; text in a corner or below.
- **H4 Stat hero** - a giant real number with a qualifier line; never bare, never invented.
- **H5 Illustration centerpiece** - one sourced illustration recolored to the accent.
- **H6 Letter** - opens like correspondence; no buttons in the fold.
- Knobs: display size · alignment (left / centered / right bias - never eyebrow, headline, lede, and CTA all on one centered axis) · support (type · mockup · photo · illustration · stat).

### Feature - F#

- **F1 Alternating bands** - full-width bands, real visual alternating sides.
- **F2 Bento tiles** - mixed-span tiles of UI fragments, stats, mini visuals (knobs: tile count 4/6/9; spans; border).
- **F3 Sticky scroll stack** - pinned visual beside scrolling steps that swap it.
- **F4 Numbered steps** - 1 → 2 → 3, each with a line and a small real visual showing a state (not a bullet list).
- **F5 Annotated capture** - one real capture with numbered pins.
- **F6 Spec sheet** - rows with hairlines and tabular figures.
- **F7 Product card grid** - real product photo, name, price, one micro-action.
- If an F-archetype collapses into heading + two sentences + decorative icon, it failed.

### Proof - P# (all real, or honest placeholders)

- **P1 Logo wall** - monochrome real logos separated by hairlines, no card boxes.
- **P2 Pull-quote with marginalia** - one real quote wide, attribution in the margin.
- **P3 Single huge quote** - one real quote as a whole section.
- **P4 Stat strip** - 3-5 real figures with qualifiers, tabular numerals.

### CTA - C#

- **C1 Inline form** - the CTA is the form.
- **C2 Statement + action** - one large closing line, one action.
- **C3 Typographic link** - a word, an arrow, an underline.
- **C4 Sticky bottom bar** - pinned CTA with one line of reassurance.

### Footer - Ft#

- **Ft1 Masthead** - wordmark + tagline band, few links, address beneath.
- **Ft2 Inline single line** - one hairline-topped line of credits.
- **Ft3 Index columns** - 3-4 link columns. ⚠️ The Product/Company/Resources/Legal + social row is an AI fingerprint when reflexive - only for genuine hubs.
- **Ft4 Statement close** - one large closing sentence, minimal links.
- **Ft5 Newsletter-first** - signup form leads.
- **Ft6 Marquee** - infinite-scroll tagline.
- Routing: premium/elegant Ft1 → Ft4, Ft2 · technical Ft2 → Ft1, Ft5 · playful Ft6 → Ft4, Ft5 · commerce Ft5 → Ft3, Ft2.

### Section heads - S#

- **S1 Hanging** - heading in negative space, no rule, no eyebrow.
- **S2 Inline** - small-caps phrase emerging in the flow.
- **S3 Sticky pinned** - heading stays while content scrolls.
- **S4 Stacked eyebrow** - label directly above the heading, same column.
- ⚠️ **Banned:** eyebrow in a left column beside the heading on the right. Eyebrows default off; at most 1-2 per page.
- ⚠️ Section headlines render at roughly **50-65% of the hero's display size** and read in 1-2 lines. One deliberate large mid-page statement is allowed in Long-Scroll Narrative or Manifesto - once.

### Rules for every archetype

- **No fake chrome** - no hand-built browser bars with traffic lights, phone frames, or code-window chrome. A real screenshot in a `<figure>` with at most a hairline, or no chrome.
- **One icon family per page; no emoji as icons.**
- **Mobile:** single column below ~60rem, display type steps down below ~40rem, 44px targets, no horizontal scroll.

## 4. Rotation (mandatory for marketing pages)

Using the last 3-5 entries of `.tastemaker/log.json` and `~/.tastemaker/history.json` (see memory.md):

1. **Macrostructure** differs from the last build's (ideally from the last three).
2. **Nav** and **footer** each differ from the last build's - the most-violated rule; rotate deliberately through the routing alternatives instead of re-reaching for the mood default.
3. **Hero** differs from the last build's.
4. **Reusing an archetype** (genuine best fit) → change at least one knob and state the delta.
5. **Palette is exempt** - it's generated per project.
6. Check the cross-project history for over-represented picks (see memory.md).

Within one project, pages stay coherent (shared nav, footer, type system) even as page bodies vary. Don't over-rotate a single site into unrelated-looking pages.

## 5. Say it out loud, then stamp it

Before code, state the rotation and arc in plain text:

> Last 3 builds: Feature Stack · Editorial Index · Bento Showcase. Picking Long-Scroll Narrative - the product needs explaining. Nav N3 (last N2), footer Ft4 (last Ft1), hero H6 (last H2). Arc: hook (H6) → problem (prose + before/after) → solution (F1) → how (F4) → proof (P4) → close (C2); nothing skipped. Cross-project history: no pick above 60% of the last five.

First build: just the pick and why. If the developer asks for the same shape again, honor it and change knobs.

**Build stamp** - the first non-empty line of the built CSS (or top of an inline `<style>`):

```css
/* tastemaker · macrostructure: Long-Scroll Narrative · mood: warm · page: landing
 * arc: hook(H6) -> problem(prose) -> solution(F1) -> how(F4) -> proof(P4) -> close(C2)
 * nav: N3 · hero: H6 · footer: Ft4 · knobs: hero=letter/1-para/typed-signoff
 * palette: warm/light · contrast: matrix pass
 * critique: ShowTell 5 · Phil 4 · Hier 5 · Spec 4 · Restr 5 · Var 5 */
```

Write the stamp, the project log entry, and the cross-project history entry in the same pass - three records of one build.
