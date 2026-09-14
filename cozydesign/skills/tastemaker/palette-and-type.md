# Palette, type, and spacing

Use on a cold start (no style lock) or when the developer asks to change direction.

## A. Classify the mood

| Mood | Signals |
| --- | --- |
| **Premium / confident** | fintech, banking, B2B, SaaS, analytics, enterprise, legal, insurance, "for teams", admin/ops |
| **Warm / approachable** | wellness, health, coaching, community, parenting, nonprofit, general education, food, hobbies, peer marketplaces |
| **Technical / builder** | developer tools, APIs, CLIs, infra, devops, databases, monitoring, open source |
| **Playful / consumer** | games, creator tools, teen audiences, dating, music, social, anything explicitly "fun" |
| **Elegant / editorial** | publishing, blogs, portfolios, luxury, fashion, galleries, boutiques, agencies - "premium but soft" |

If the request already states the mood ("playful app for teens"), use it. Ask only when the idea genuinely spans two moods with no lean, or when the developer wants options first. Otherwise state the mood in one line and move on - they can redirect.

**Check the script too.** Non-Latin copy (Korean, Japanese, Chinese...) changes the typography model - see section E before choosing type.

## B. Generate a fresh palette (not a fixed set)

Two projects in the same mood must not ship the same palette. Build one per project:

1. **Base hue** - choose a hue inside the mood's character, varied per project (don't always take the anchor's hue):
   - Premium: saturated blue-to-violet family, or a confident deep green/teal; restrained secondary.
   - Warm: earthy hues - terracotta, clay, ochre, sage, olive; soft cream grounds.
   - Technical: dark-native; one vivid signal hue (green, cyan, amber, violet) over near-black neutrals.
   - Playful: high-chroma hues with a quiet base to pop against; two vivid roles max on solid UI.
   - Elegant: near-neutral warm grounds; one metallic or muted accent (gold, oxblood, forest).
2. **Harmony rule** for the accent - pick one per project: analogous, complementary, split-complementary, triadic, or monochrome.
3. **Roles:** text, background, surface, primary, on-primary (button label), secondary, accent, border.
4. **Solve lightness per role against the contrast floors** (below) - work in OKLCH so lightness steps are predictable; adjust lightness within the hue, not the hue itself.
5. **Compute the contrast matrix** and record it in the style lock's Color contract.

Compute contrast - never eyeball it. WCAG 2 ratio: linearize each sRGB channel (`c ≤ 0.04045 ? c/12.92 : ((c+0.055)/1.055)^2.4`), luminance `L = 0.2126R + 0.7152G + 0.0722B`, ratio `(L_light + 0.05) / (L_dark + 0.05)`. Use a quick calculation in the project's own runtime, the browser devtools contrast readout, or the better-colors skill - and show the numbers.

### Contrast floors (the color contract)

| Pairing | Floor |
| --- | --- |
| Body/muted text on background or surface | 4.5:1 |
| Button label on any solid fill | 4.5:1 |
| Accent or link used as text | 4.5:1 |
| A fill against the page (does the button show at all) | 3:1 |
| Accent as icon or highlight | 3:1 |
| Border that carries state (focus, error, the only boundary) | 3:1 (decorative hairlines exempt) |

Sort every pairing into **text-safe** (≥4.5), **UI-safe** (3-4.5), and **decorative** (<3). Later screens may only use pairings from the right list for their purpose; a new pairing means recomputing and updating the lock.

**Two checks people forget:** the button label on the primary fill (a pleasant swatch can clear only 2.5-3.6:1 with white text), and the primary fill against a **dark** background (a light-mode primary can vanish below 3:1 on near-black).

**When a pairing fails, in order:** reuse a pairing already legal for that purpose → nudge the color's lightness within its hue and recompute → fall back to a known-safe neutral (text or on-primary) for that pairing → if a fixed brand color truly can't meet the floor, stop and surface the conflict. Don't loop on a failing value, and don't ship it.

### Reference anchors (the intended character - do not ship verbatim)

| Mood | Text | Background | Primary | Secondary | Accent | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| Premium | `#050315` | `#FBFBFE` | `#2F27CE` | `#DEDCFF` | `#433BFF` | Dark: text `#F2F1FB`, bg `#0A0A12`, primary `#5850E0` (the light primary drops to ~2.2:1 on the dark bg), secondary `#17162A`, accent `#8F87FF` |
| Warm | `#2B2118` | `#FBF7F0` | `#B85A38` | `#F0E4D3` | `#7A8C6E` | Primary darkened from a terracotta that gave only ~3.6:1 with white labels. Dark: text `#F5EFE6`, bg `#14100C`, primary unchanged, secondary `#241C15`, accent `#9BAF8E` |
| Technical | `#E6E6EA` | `#0B0D12` | `#047857` | `#161A21` | `#34D399` | Dark-native. Bright emerald gave ~2.5:1 with white labels, so the brighter green is accent only |
| Playful | `#14042B` | `#FFFFFF` | `#4361EE` | `#7209B7` | `#F72585` | Extra gradient stops `#3A0CA3`, `#4CC9F0` for hero/illustration fills only. Dark bg `#0D0620` keeps the hue |
| Elegant | `#211F1C` | `#F7F4EE` | `#2F2A24` | `#E8E1D3` | `#B5762C` | Dark: text `#EFE9DC`, bg `#171310`, primary `#9C6524` (the near-black light primary vanishes on dark), secondary `#241E17`, accent `#D9A54A` |

White is the correct label color on all five anchor primaries. Shape character per mood: premium flat or hairline, 4-8px radius, no depth shadows, one saturated color; warm 12-20px radius, soft shadows, illustration-friendly, no corporate blue; technical sharp corners, visible borders over shadows, no pastels or pill buttons; playful large radius, layered depth, motion-friendly, but a quiet base; elegant generous margins, hairline rules instead of cards, no pill buttons.

## C. Type pairing (curated per mood; all Google Fonts)

| Mood | Heading + body | Alternative |
| --- | --- | --- |
| Premium | Unbounded + Albert Sans | Inter + Inter with tight heading tracking |
| Warm | Zain + Nunito | Epilogue + Baskervville (softer, literary) |
| Technical | Archivo + IBM Plex Sans (Plex Mono only for code, data, timestamps) | IBM Plex Sans + Plex Mono for data |
| Playful | Urbanist + Open Sans | Fredoka + Nunito |
| Elegant | Gloock + Inter | EB Garamond + DM Mono accents (bylines, dates) |

Never set long-form body copy in monospace - it's a template tell even for developer products. If no pairing fits, browse a curated pairing catalog (e.g. fontpair.co) and slot it into the same role structure rather than inventing a new mood.

## D. Light/dark toggle (an explicit decision)

Only when the product truly needs a runtime switch (common for internal tools):
- Derive the dark palette from the **same** base hue, harmony, and chroma as light - a companion pair, not two unrelated palettes - then solve each mode's lightness against its own floors and compute both matrices.
- Both role sets as CSS custom properties swapped by `data-theme` on `<html>`; components read only variables.
- Initial value from `prefers-color-scheme` (set before first paint to avoid a flash); an explicit toggle overrides it and persists in `localStorage`.
- Record "runtime toggle - both modes verified" in the lock.

## E. Non-Latin scripts (CJK, Korean)

The Latin display + body pairing model doesn't transfer.
- **One family across a weight scale:** headings SemiBold/Bold, body Regular, UI chrome Medium. Mixing families in dense CJK glyphs looks inconsistent.
- **Korean starting point:** Pretendard (variable, 9 weights, SIL Open Font License) - not on Google Fonts; load from its official CDN and verify the current embed and Hangul rendering at build time. Japanese/Chinese: Noto Sans JP / SC are reasonable starts but less vetted - say so.
- **Letter-spacing 0** by default - don't carry negative Latin heading tracking into Hangul syllable blocks.
- **`word-break: keep-all`** for headings, buttons, labels, and short UI copy; long-form paragraphs are the exception.
- **Looser line-height** than Latin display floors, verified visually.
- Mixed Latin inside CJK copy often needs optical size adjustment - check it rendered.

## F. Spacing scale (4px base)

| Token | Value | Use |
| --- | --- | --- |
| space-1 | 4px | Icon-to-label, badge internals |
| space-2 | 8px | Label and value, stacked related lines |
| space-3 | 12px | Dense table cells, app-shell nav rows |
| space-4 | 16px | Button padding, compact stat tiles |
| space-6 | 24px | Gaps between a card's parts; **minimum content-card padding** |
| space-8 | 32px | Showcase card padding; gaps between groups in a section |
| space-12 | 48px | Compact section padding; major gaps inside a hero |
| space-16 | 64px | Default section padding; floor for connective landing sections |
| space-24 | 96px | Standard weighty sections |
| space-32 | 128px | Pivotal sections (hero, primary proof) |
| space-40 | 160px | The page's strongest beat |
| space-48 | 192px | Ceiling - the single section that must dominate |

Values between steps are legal but rare.

**Internal ≤ external.** A group's surrounding space is at least the space inside it (Gestalt proximity). Cards 24px apart get at least 24px internal padding; a 64px-padded section has smaller gaps inside.

**Card floors:** compact/dense (stat tile, nav row, list item) 12-16px · content card (feature, pricing tier, testimonial) ≥24px · showcase/featured card ≥32px.

**Landing-page section padding - weight by role, don't flatten:**
- Connective (logo strip, trust bar, transition band): 48-64px.
- Standard content: 64-96px.
- Pivotal (hero, primary proof/demo): 128-192px.

The combined gap between adjacent sections on well-separated pages is commonly ~120-250px on desktop; undershooting it makes everything feel cramped. Whitespace alone is a legitimate separator. **Step down one or two tiers on mobile** (≤40rem: pivotal → 96-128px, standard → 64px), keeping the relative weighting. App shells stay dense - never pad a settings screen like a hero.

**Radius:** one scale project-wide (e.g. 4 / 8 / 16).

Record the tokens actually used in the style lock's Density & spacing section.
