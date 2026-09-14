# Design directions and recipe index

Two jobs: (1) the **Direction Advisor** for vague requests, and (2) the index to the **style recipes** - concrete palettes, type, spacing, and signature moves tied to named real-world anchors.

## Direction Advisor

**Use when** the request is genuinely open ("make something nice", "I don't know what style I want", "give me some directions") and there's no design context, or the developer asks you to recommend a style.

**Skip when** they supplied Figma/screenshots/brand material, named a direction already, or it's a small tweak.

### Mechanism: three contrasting directions, not ten questions

Offer **three directions from three different schools** so the contrast is obvious and the choice meaningful. Each includes:

- a **named designer, studio, or product anchor** ("Pentagram-style information architecture", never just "minimalist");
- two or three lines on **why it fits this project**;
- **3-4 signature cues** (color, type, layout, motion);
- optionally one famous touchstone.

Never three from the same school. Never five or more (choice paralysis). Never "modern", "clean", or "minimal" as the direction's name. Don't ask them to score the options - recommend one.

### After they choose

- **"#2"** → confirmed; record it in `brand-spec.md` (or project notes) and continue the main workflow with it as context.
- **"A's color with C's layout"** → restate the remix in one sentence, confirm, continue.
- **"None of these"** → one narrowing question ("closer to formal and institutional, or playful and expressive?"), then three fresh directions from schools not yet shown.
- **"You pick"** → pick the safest fit (usually editorial/minimalist), say why, and propose a quick v0 to validate.

Then open the chosen school's recipe file and surface 2-3 concrete recipes.

## The schools

| School | Vibe | Anchors | Best for | Recipe file |
| --- | --- | --- | --- | --- |
| **Information architecture** | Rational, restrained, hierarchy-led; the design disappears so information speaks | Pentagram, Tufte, Vignelli, Bloomberg Terminal, NYT | B2B, institutional, data products | [information-architecture.md](style-recipes/information-architecture.md) |
| **Editorial / minimalist** | Whitespace as material, refined type, quiet confidence | Kenya Hara / MUJI, Apple, Dieter Rams, Aesop, Monocle | Premium, lifestyle, high-end B2C | [editorial-minimalist.md](style-recipes/editorial-minimalist.md) |
| **Modern tool / builder SaaS** | Hairline detail, warm dark, one accent, mono chips | Linear, Vercel, Raycast, Notion (pre-AI) | Dev tools, B2B SaaS, AI tools, infra | [modern-tool.md](style-recipes/modern-tool.md) |
| **Motion / experimental** | Movement *is* the brand; generative, cinematic | Field.io, Active Theory, Resn | Launches, brand moments, portfolios | [motion-experimental.md](style-recipes/motion-experimental.md) |
| **Brutalist / raw** | Deliberately unpolished, honest, confrontational | Are.na, Businessweek (Turley era), Balenciaga post-2017 | Counter-culture, publishing, artists | [brutalist-raw.md](style-recipes/brutalist-raw.md) |
| **Warm humanist** | Approachable, hand-touched, made by people for people | Mailchimp (Freddie era), Stripe Press, Headspace | Education, community, wellness, approachable B2C | [warm-humanist.md](style-recipes/warm-humanist.md) |
| *Specialty / genre* | Decade-coded; reached only when named directly | Y2K / Frutiger Aero, mid-century modern | Nostalgia, music, fashion, heritage | [specialty-genre.md](style-recipes/specialty-genre.md) |

Notes: Vercel and Linear use motion as *restraint*, so they sit in modern tool, not motion/experimental. Notion borrows warmth but is a tool first. Modern tool is the school model defaults most often fail to reach - they drift to purple-pink gradients instead.

### Sample pitches

- *Information architecture:* "Pentagram-style - the dashboard becomes a system of typographic relationships. Headlines carry the visual weight; everything else recedes. Right when institutional credibility matters and the data is the hero."
- *Editorial / minimalist:* "Kenya Hara-style quiet - mostly whitespace, one serif headline carrying the emotion, the product in a single hero shot. Right when premium positioning beats feature density."
- *Motion / experimental:* "Field.io-style - the page assembles itself through choreographed scroll sequences. Right when the launch moment matters and people will share clips. The most labor-intensive option."
- *Brutalist / raw:* "Are.na-style - system fonts, harsh contrast, no radius, no shadows. Confrontational on purpose; repels people who want generic SaaS. Half-measures look broken, not bold."
- *Warm humanist:* "Stripe Press warmth - humanist serifs, cream grounds, tactile imagery. Trust and approachability over corporate polish; the tone of a friend who happens to be an expert."
- *Modern tool:* "Linear-style - warm dark ground, 1px hairlines, one accent on under 5% of pixels, monospace shortcut chips. Right for technical audiences who want serious-but-designed."

## Using recipes

**Load a recipe when** an anchor is named ("Linear-style", "Aesop feel"), the Advisor narrowed to a school, or Step 3 needs a proven token set. Open **one school file** and use the one recipe you need.

**Don't use recipes when** the developer supplied brand assets, Figma, or code (extract from those), when extending an existing UI (match what's there), or when they gave a screenshot of a reference (that screenshot is the recipe).

Each recipe lists: school, vibe, best for, touchstone, palette (hex by role), typography, spacing, radius, shadow, motion, signature moves, avoid, image prompt seed, and when not to use it. Values are design tokens in words - translate them to the project's stack.

### Rules that apply to every recipe

- **One recipe per page.** "Linear with Aesop accents" usually reads as confused. Remix only when asked and you can say why the pairing is coherent.
- **Commit fully to brutalist and genre recipes.** Half-Y2K looks like a broken modern site; half-brutalism looks unfinished.
- **Use the recipe's fonts** (or the substitutes it names). Falling back to Inter erases 30-40% of a recipe's identity.
- **Don't add colors.** A restricted palette *is* the recipe.
- **Don't add default touches "to make it pop".** No sneaking in shadows, gradients, or emoji the recipe forbids.
- **Don't fake photography or illustration with CSS.** Aesop, Stripe Press, MUJI, Apple, Mailchimp, and Headspace depend on imagery; if you can't source or generate it, say so.
- **Don't invent recipes silently.** If none fits, say so and propose a named anchor with concrete values for approval.

### When nothing fits

1. Re-read the request - a "data-led research tool" is almost always Tufte or Bloomberg Terminal even if unnamed.
2. Combine two recipes deliberately, with explicit framing.
3. Run the Direction Advisor.
4. Articulate a new recipe (anchor, values, signature moves) and get sign-off.

State the chosen recipe in the Step 3 declaration so it's confirmed before code.

## Image prompts for a direction

Structure: **[philosophy DNA] + [content] + [technical parameters]**. Include hex colors (not "warm"), aspect ratio, composition rule, and what to avoid.

- Good: "Kenya Hara-influenced minimalism, 80% whitespace, single muted terracotta (#C04A1A) accent, serif headline, one product on warm off-white (#F2EFE8), soft top-down light, 3:2, no gradients, no people."
- Bad: "minimalist style, premium feel, high quality."

Each recipe carries a prompt seed; start from it.
