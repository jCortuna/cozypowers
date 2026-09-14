# Editorial / minimalist recipes

Whitespace as the primary material; restraint reads as confidence. Rules shared by all recipes: see [../design-directions.md](../design-directions.md).

---

## apple-hig - Apple product marketing

- **Vibe:** a stage for one product; generous space; one thought per screen. **Best for:** premium hardware or software that "deserves a stage". **Touchstone:** apple.com product pages, keynote slides.
- **Palette:** ground `#FFFFFF` (or `#000000` for film-like hero moments only); ink `#1D1D1F`; soft surface `#F5F5F7`; muted text `#86868B`; accent blue `#0071E3`, sparingly; hairline `#D2D2D7`.
- **Type:** SF Pro Display 600 for headlines, 400 for sub-display (Inter Tight only if SF Pro is unavailable); body SF Pro Text 17px / ~1.47; captions 12-14px in muted gray.
- **Spacing:** 4 / 8 / 16 / 24 / 40 / 64 / 96 / 160; section breaks 160px+.
- **Radius:** 12 small / 18 cards / 22 large panels - rarely sharp, never gummy. **Shadow:** at most `0 1px 2px rgba(0,0,0,0.04)`; elevation comes from space and contrast.
- **Motion:** expo-out; 350-650ms layout moves, 150-250ms hovers; never bouncy; slow Ken Burns on hero imagery.
- **Signature moves:** one product photo centered in whitespace (~40% of the hero); big display headline, muted line beneath, a single blue text-link CTA (buttons come later); long vertical sections - small label, big headline, one paragraph, one product shot, repeat; hairline dividers only; stats where the unit is set smaller than the number.
- **Avoid:** mesh/glow "tech atmosphere"; multiple hero CTAs; feature card grids; emoji.
- **Prompt seed:** studio-lit product photo, single object centered on pure white, soft diffused top light, faint floor reflection, 16:9, no text, no people, neutral grade.
- **Don't use when:** software with no hero object; scrappy/startup brands; anti-corporate audiences (reads as Apple cosplay).

---

## muji-kenya-hara - MUJI / Kenya Hara

- **Vibe:** emptiness as fullness; off-white as a value; near-silence. **Best for:** quiet premium positioning, everyday-craft goods. **Touchstone:** muji.com, Hara's book *White*.
- **Palette:** ground `#F4F2EC` (never pure white); ink `#2A2A28` (never pure black); secondary `#7C7B76`; hairline `#D9D6CD`; no accent - at most MUJI red `#C8161D` as a tiny corner mark or rule.
- **Type:** humanist sans (Söhne, Inter Tight, Calibre) at 400, never above 500, tracking +0.01-0.02em; body 15-16px / ~1.8; bilingual pairs with Noto Sans CJK weight-for-weight.
- **Spacing:** 8 / 16 / 32 / 48 / 96 / 160 / 240 - 240px between sections is normal.
- **Radius:** 0 (maybe 2px on inputs). **Shadow:** none.
- **Motion:** almost imperceptible; 600-900ms fades; nothing moves more than a few px.
- **Signature moves:** 60-80% empty page with content in a narrow column; one small, plainly captioned product image per screen; tiny letter-spaced labels ("01 - Cotton") instead of shouting headlines; hairline rules as the only ornament.
- **Avoid:** saturated color; shadows, glows, gradients; tabs, accordions, mega-menus, sticky banners; "above the fold" thinking.
- **Prompt seed:** one household object on warm off-white `#F4F2EC` paper, raking daylight from upper left, vast quiet space, 3:2, film look, neutral tone.
- **Don't use when:** the message is feature density (specs, tiers, comparisons); fast-scanning audiences; a noisy market where the brand must shout.

---

## aesop - Aesop

- **Vibe:** apothecary refinement; sage and ink; serif copy as conversation. **Best for:** premium consumer goods, literary hospitality. **Touchstone:** aesop.com, the amber bottle.
- **Palette:** ground `#E8E4D9` (warm chamois) or `#F2EFE5`; cream surface `#F0EDE4`; ink `#1B1B1B`; sage `#7A8470`; amber accent `#7A4623` for a single rule or seal.
- **Type:** one transitional serif at every size (Suisse Works, Lyon Text, GT Sectra) at 400 with italics; a single sans (Söhne, Helvetica Now) for UI labels; body 16-18px / ~1.65; labels in small caps 10-11px, +0.12em.
- **Spacing:** 8 / 16 / 24 / 40 / 72 / 120. **Radius:** 0 everywhere, including inputs. **Shadow:** none.
- **Motion:** gentle fades; slow drawer slides (~450ms ease-out); never springy.
- **Signature moves:** body copy with literary cadence, justified, no marketing punch; product on chamois with one natural prop and a long shadow; small-caps section labels (INGREDIENTS, RITUAL); letter-spaced all-text navigation; asymmetric layouts - image one side, generous copy block the other.
- **Avoid:** bold weights; any color beyond sage/amber/ink; pop-up modals; smiling stock models.
- **Prompt seed:** amber glass bottle on textured chamois `#E8E4D9`, linen and a dried sage sprig, raking afternoon window light, long soft shadow lower right, 4:5, warm grade with slight green cast.
- **Don't use when:** digital-first products (the object photography is half the recipe); price-comparison audiences; funny or casual voices.

---

## dieter-rams-braun - Dieter Rams / Braun

- **Vibe:** "less, but better"; functional honesty; industrial restraint. **Best for:** hardware, audio gear, tools, design-led B2B. **Touchstone:** Braun T3 radio, ET66 calculator, Rams's ten principles.
- **Palette:** ground `#E4E1DC` (light concrete) or `#F5F4F0`; ink `#191919`; grays `#A8A8A8`, `#5C5C5C`; one signal accent - orange `#E96A26` or yellow `#F5C518` - only on functional elements (power dot, active state).
- **Type:** precision grotesk (Akzidenz-Grotesk, Helvetica Now, Söhne) 400 body, 500 emphasis, never 700; monospaced numerals for spec tables.
- **Spacing:** 4px sub-grid; 4 / 8 / 16 / 24 / 32 / 64 / 128; no luxury inflation. **Radius:** 2-4px max. **Shadow:** none.
- **Motion:** utilitarian; 80-120ms state changes; no flourish.
- **Signature moves:** diagrammatic exploded views with measurement callouts; one orange dot meaning "on"; spec tables as a first-class layout element; literal labels ("ON / OFF"); the page itself feels like equipment.
- **Avoid:** romantic product photography (shoot it like a specimen on a grid); multiple accents; bouncy hover; lifestyle imagery.
- **Prompt seed:** 1960s Braun-style hardware on light gray `#E4E1DC` grid, frontal orthographic view, thin sans dimension labels, gray/black with one orange marker, 4:3.
- **Don't use when:** emotional or lifestyle products; teams wanting warmth; non-technical consumers (reads as a boring spec sheet).

---

## monocle-magazine - Monocle

- **Vibe:** international, considered, magazine-grade hierarchy. **Best for:** editorial, travel, hospitality, journals. **Touchstone:** monocle.com, the Monocle quarterly.
- **Palette:** ground `#F2EFE7` (cream paper); ink `#1A1A1A`; editorial red `#C7322E`; olive `#5E6347`; hairline rules `#C8C2B0`.
- **Type:** refined serif display (Plantin, Mercury, Tiempos Headline) with generous italics; body Plantin/Tiempos Text 16-17px / ~1.6; kickers in a precision grotesk 10-11px, +0.08em, often red; drop caps on features.
- **Spacing:** 4 / 8 / 16 / 24 / 32 / 48 / 96; 16-24px column gutters. **Radius:** 0. **Shadow:** none.
- **Motion:** minimal - page-turn fades, slow Ken Burns on lead photos.
- **Signature moves:** three-deck hierarchy (small red kicker → bold serif headline → italic dek); 2-3 column body with hairline column rules; numbered features ("Feature 04 - Lisbon"); lead photo cropped hard at one edge with the headline in its negative space; large italic pull-quotes.
- **Avoid:** sans headlines; stock photography; card grids; more than one accent.
- **Prompt seed:** place-specific editorial photo (a Tokyo backstreet at dusk), warm grade, light grain, one person mid-ground, 3:2, warm earth tones with one red object.
- **Don't use when:** SaaS product pages; no editorial/human/place content to lead with; scanning audiences.
