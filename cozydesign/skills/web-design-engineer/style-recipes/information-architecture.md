# Information architecture recipes

The page as a system of typographic and grid relationships; the design recedes so information speaks. Shared rules: [../design-directions.md](../design-directions.md).

---

## pentagram - Pentagram / Paula Scher

- **Vibe:** typography as image; type does the visual work. **Best for:** B2B identity, cultural institutions, "we mean business". **Touchstone:** pentagram.com, Scher's Public Theater posters.
- **Palette:** two colors, ink on ground - black on white, cobalt `#1E3FFF` on cream `#F4F1E7`, or brick `#B83A1F` on bone `#EFE9DC`; a third only if the project demands it.
- **Type:** one grotesque at massive scale (Helvetica Now 700-900, Söhne Breit, Druk), often set wider than its column; body same family 16-17px / 1.45-1.55; tabular figures.
- **Spacing:** strict 12-column grid, 24-32px gutters, everything on a baseline grid. **Radius:** 0. **Shadow:** none.
- **Motion:** typographic only - letters shift in, headlines slide along a baseline; no 3D, bounce, or parallax.
- **Signature moves:** headlines that touch or break the column edge; a single word at hero scale as the only graphic; flat color-block section dividers carrying one huge number ("02"); tiny precise captions pinned in gutters; one full-width 1px rule anchoring the page.
- **Avoid:** photography as the lead (if present, it sits under enormous type); multiple families; gradients, shadows, ornament; card grids.
- **Prompt seed:** poster composition, one phrase in massive black Helvetica 900 bleeding past the margins over a flat cobalt `#1E3FFF` field, no photo or illustration, 3:4.
- **Don't use when:** copy can't be short and bold (3-6 words); heavy feature catalogs; brands meant to feel quiet.

---

## vignelli-swiss-helvetica - Vignelli / Swiss International

- **Vibe:** strict grid, Helvetica throughout, matter-of-fact order. **Best for:** wayfinding, institutional identity, deeply structured information. **Touchstone:** Vignelli's 1972 NYC subway map, *The Vignelli Canon*.
- **Palette:** black `#000000`, white `#FFFFFF`, one accent only - red `#E2231A`, yellow `#F5C518`, blue `#0033A0`, or orange `#FF6F00`; gray `#8A8A8A` for secondary content.
- **Type:** Helvetica / Helvetica Now only; 400 / 500 / 700; no italic; hierarchy by size, not weight or color; scale 72 / 48 / 32 / 24 / 16 / 12 on one baseline grid.
- **Spacing:** 8px baseline, 12 columns, leading at or above type size. **Radius:** 0. **Shadow:** none.
- **Motion:** none, or signage-like snaps.
- **Signature moves:** bold color bars carrying section headers in white; a grid made visible where it helps; tabular layouts with strict baselines for schedules and lists; left-aligned body at a 60-70 character measure; one oversized section number top-left of each block.
- **Avoid:** serifs; extra colors; italics, shadows, gradients, softness; chummy copy.
- **Prompt seed:** transit-signage composition, big directional arrow in black on a flat accent field, condensed Helvetica labels, flat vector, 16:9.
- **Don't use when:** brands need warmth; emotional storytelling; "fresh" is the goal (Swiss now reads classical).

---

## bloomberg-terminal - Bloomberg Terminal

- **Vibe:** maximum data-ink; mission-critical density; amber on near-black. **Best for:** trading, finance, monitoring dashboards. **Touchstone:** a real terminal screenshot - it's denser than memory suggests.
- **Palette:** ground `#0A0E1A`; surfaces `#11172A`, `#1A2138`; amber `#FFA02F` (the signature); up `#00B96B`; down `#F23645`; muted label `#5E6680`; important text `#E8ECF4`; hairlines `#2A3050`.
- **Type:** monospaced throughout (IBM Plex Mono, JetBrains Mono, Berkeley Mono); 11-14px only - no 16px body, no big headlines; right-aligned tabular digits.
- **Spacing:** 2 / 4 / 8 / 12; multi-pane, no luxury margins. **Radius:** 0-2px. **Shadow:** none - 1px hairlines separate panes.
- **Motion:** linear ticker scroll, instant flips, 50-80ms flash on data update; no easing.
- **Signature moves:** 4-9 visible panes split by hairlines; amber for the most important data, off-white for secondary; color-coded scrolling ticker bar; function-key chips in the margins ("F9 TRADE"); delta-colored tabular data.
- **Avoid:** rounded corners; hero sections and marketing headlines; photos and illustration; decorative gradients; sans body text.
- **Prompt seed:** trading workstation UI, deep navy `#0A0E1A`, multi-pane layout, amber `#FFA02F` headers, monospaced tables, top ticker, no radius, 16:9.
- **Don't use when:** consumer audiences; you can't fill it with real data (dummy numbers look broken); marketing pages.

---

## tufte-dataink - Edward Tufte

- **Vibe:** every mark earns its place; the chart is the page. **Best for:** analytical reports, scientific writing, data storytelling. **Touchstone:** *The Visual Display of Quantitative Information*.
- **Palette:** ground `#FBFAF6`; ink `#1B1B1A`; two data colors - warm red `#A6300E`, slate `#3E4A5C` (a third only for a genuine third dimension); faint reference rules `#D8D2C2`.
- **Type:** old-style/transitional serif (ET Book, Equity, Lyon Text) 400 with italic emphasis; deliberately small body 12-14px; humanist sans 10-11px in `#5C5550` for axis labels only.
- **Spacing:** tight - 4 / 8 / 12 / 16 / 24 / 48; margins hold side-notes rather than emptiness. **Radius:** 0. **Shadow:** none. **Motion:** none.
- **Signature moves:** sparklines inside sentences; heavy margin notes instead of tooltips; no chart junk (faint gridlines at most, no boxes, no 3D, no legend when direct labels work); small multiples; series labelled at their endpoints.
- **Avoid:** pie charts; 3D; gridlines darker than `#D8D2C2`; mixed chart types where one would do; decorative color.
- **Prompt seed:** editorial scientific figure on warm paper, two time series in muted red and slate, direct end labels, italic serif side-notes, no frame, no legend, 4:3.
- **Don't use when:** decorative charts; interactive filter/tooltip products; small mobile screens.

---

## nyt-the-daily - New York Times editorial

- **Vibe:** authoritative broadsheet craft. **Best for:** longform, journalism, narrative explainers. **Touchstone:** nytimes.com features, NYT Cooking.
- **Palette:** ground `#FFFFFF`; ink `#121212`; secondary `#666666`; red `#D0021B` for breaking indicators only; soft section `#F7F7F7`; hairline `#E2E2E2`.
- **Type:** display in a Cheltenham-like serif (substitutes: Sentinel, Tiempos Headline) 700 with italics; subheads in Imperial/Lyon Display 400; body serif (Imperial, Georgia, Source Serif) 18-20px / ~1.55; kickers in a Franklin-style sans (substitute Söhne) 500, often small caps.
- **Spacing:** 4 / 8 / 16 / 24 / 32 / 48 / 96; multi-column story grids. **Radius:** 0. **Shadow:** none.
- **Motion:** minimal - sticky bylines, fade-in lazy images, 8-15s slow zoom on hero photos.
- **Signature moves:** eyebrow (OPINION / ANALYSIS in small-caps sans) → bold serif headline → italic standfirst; byline and timestamp block beneath, always; italic pull-quotes at 1.5-2x body between hairlines; multi-column body on wide screens, single column on mobile; distinctive serif captions.
- **Avoid:** sans headlines; article card grids (lay out a front page with hierarchy by size); pretty buttons inside articles; centered body text.
- **Prompt seed:** photojournalism, one decisive moment, natural light, 3:2, neutral slightly desaturated grade, unstaged, place-specific.
- **Don't use when:** SaaS dashboards; short punchy content; brands without editorial authority (reads as cosplay).
