# Hero and copy

## Hero

The visitor should understand the product before they notice the composition. The goal is a decisive attention hierarchy, not minimalism for its own sake.

### Five-second answer

Before markup, complete: **"This product helps [specific user] achieve [valuable outcome] by [distinct mechanism]."** The outcome becomes the headline; the subhead clarifies the mechanism. If the hero needs a diagram, four metrics, or a paragraph to explain itself, the message isn't sharp yet.

### Attention budget (a limit, not a quota)

- **Eyebrow:** optional, only if it adds context the headline can't.
- **Headline:** one promise, usually 6-12 words.
  - **6-8 words** → full display size (top of the type scale's clamp range).
  - **9-12 words** → one tier down (~15-20% smaller across the clamp range). Needing both the long end *and* full size means cut the headline.
  - **3-5 words** → capped at the same full display size, never larger. Punch comes from word choice and space. A 1-2 word headline is a rare, deliberate art-directed statement.
  - Short headlines read on 1-2 lines - one word per line means the type is too big.
  - Tighten display line-height, but check visually that descenders and punctuation never touch the next line at the actual weight and size (≤0.87 on a bold, very large headline is a known clipper).
- **Subhead:** one sentence, ideally 16-28 words, at most two lines on desktop.
- **CTA:** one primary; one secondary only for a distinct lower-commitment path (demo, docs, proof).
- **Visual:** one focused visual that proves the outcome.
- **Nav:** stays quiet; never competes with the hero CTA.

**Not in the hero:** trust rows, feature chips, workflow rails, metric sidebars, floating badges, stamps, orbit lines, file/status footers, multiple mockups. Move them below the fold where they become real proof.

### One proof visual - show the result, not the machinery

- Builder/generator → one excellent finished output.
- Dashboard → crop to the one decision users care about, not the whole shell.
- Workflow → the completed state; steps go below.
- Physical product → one strong product-in-context image.
- Abstract service → one clear illustration or before/after tied to the promise.

At most one outer frame; no dashboard-inside-a-dashboard.

**Optional annotation chip:** one (at most two) small chips with a *real* number and a 1-3 word label, sitting **on** the proof visual's edge - caption scale, never floating alone in hero space.

**Animated comparison:** when proof is inherently before/after and both states exist as **real** captures, layer them and animate a `clip-path: inset()` wipe driven by a CSS variable on a slow yoyo loop (e.g. GSAP tweening `--wipe`, sine easing, ~4s). Keep the range around 15-85% so both sides stay visible; freeze at 50% under reduced motion. Never stage one side to look worse than it is. It replaces the proof visual rather than adding one.

**Ambient depth (optional):** a low-opacity accent glow behind the visual or a slow few-pixel idle float; or, when the brief wants real production value, a proper WebGL shader background behind the whole hero with a vignette keeping motion in the margins (see components.md). Slow, low amplitude, and static under reduced motion.

### Composition

- Headline and visual get separate territories with generous negative space; one side dominates slightly (equal columns read templated).
- At most one intentional rule-break: a controlled bleed, an off-grid edge, or a restrained accent bar.
- Hero palette quieter than the sections below; accent marks the key phrase, the action, *or* a detail - not all three at full intensity.
- An existing logo that clashes with the new theme stays untouched - solve it with space, scale, or its container.

### Reference check

Before calling a hero done, look at one genuinely excellent current site in the same category and name what it actually does. Often the answer is restraint at scale - huge type, a real product screenshot fading out, one small text-link secondary action, no badges or glow. "Award-winning" doesn't automatically mean more decoration.

### Motion

At most four beats: nav/context → headline → subhead and actions → the proof visual. Animate the visual as one composition - don't stagger every label and tile. No decorative parallax or orbits in the first viewport unless they explain the product. Reduced motion respected.

### Responsive checks

- 390px: no horizontal overflow; headline in roughly 3-5 lines with no avoidable orphan; subhead one compact paragraph; CTAs side by side or stacked full-width, never squeezed.
- At full display size, the headline fits in 2-3 lines; 5+ lines means step size down or shorten.
- The proof visual stays legible when stacked - crop or simplify internals rather than shrinking.
- On short desktop viewports, the promise and action are visible without scrolling.

### Subtraction pass

List every hero group and keep only those answering: What is this? Why care? What next? What does a good result look like? Move everything else down; if two groups answer the same question, keep the stronger.

## Copy

Palette and structure variety stop pages *looking* alike; nothing stops them *reading* alike. The tell isn't vocabulary - swapping "elevate" for "transform" writes the same sentence. **The tell is the sentence template.**

### 1. Ground every headline in one checkable fact

Ask: **what fact about this product would be false with a close competitor's name swapped in?** A specific mechanism ("renders diffs before you merge"), a real number from the brief (never invented), a user action only this product enables ("comment directly on the running chart"), or a contrast with the obvious alternative ("no build step", "runs on your own infra"). Write the sharpest sentence containing it. Don't let the mechanism slot collapse into "efficiency" or "growth".

### 2. Three candidates, three angles

1. **Mechanism-led** - what it specifically does.
2. **Outcome-led** - how the user's situation changes, still grounded in the fact.
3. **Tension-led** - the specific problem or contrast it resolves.

Reject any matching the template bank; pick the best survivor for the locked mood and structure.

### Voice dials by mood

State the dial before drafting.

| Mood | Rhythm | Formality | Avoid |
| --- | --- | --- | --- |
| Premium | Short, declarative; certainty over adjectives | "You", restrained, no exclamation marks | Stacked intensifiers |
| Warm | Slightly longer, conversational, contractions | Friendly | Baby-talk, forced cheer |
| Technical | Terse, dense, real technical nouns | Peer to peer, no gloss | Explaining the obvious; "blazing fast" instead of a number |
| Playful | Punchy, verbs over nouns, may bend grammar | Casual | Borrowed internet-speak; emoji as icons |
| Elegant | Measured, subordinate clauses allowed | Understated, magazine-lede | "Exquisite", "unparalleled", "curated" as filler |

### No em dashes in shipped copy

The em dash is banned from everything a visitor reads - headlines, subheads, body, buttons, alt text, meta descriptions, FAQ answers, empty and error states. It's one of the most recognizable machine-writing tells on its own. Rewrite the sentence (period, comma, colon, parentheses, or cut the second clause) rather than swapping punctuation. The only exception is exact copy the developer supplies.

### Template bank - reject on sight

- "The [adjective] way to [verb]."
- "Built for [audience] who [verb]." as the whole headline
- "[Verb] your [noun] in [time]." (unless a real measured time)
- "Where [noun] meets [noun]."
- "[Adjective], [adjective] [noun]."
- "Everything you need to [verb]."
- "[Noun] made [adjective]."
- "Say goodbye to [problem]."
- "Your [noun], reimagined."
- "One platform for all your [noun]."

Also reject the generic vocabulary: elevate, seamless, unleash, next-gen, game-changer, supercharge, revolutionize, delve, robust, cutting-edge, empower, streamline (as the whole claim).

### Cross-project memory

Record the shipped headline, CTA, and winning angle in `~/.tastemaker/history.json` (memory.md). Before finalizing, compare against recent entries: a near-paraphrase of another project's headline, or the same template, is a flag to rewrite. Once enough outcomes resolve (4+), angle kept-rates can break ties between equally good candidates - never replace writing three real ones.

### Rules

- Product names, real feature names, and real numbers are exempt - they're the specific content this protects.
- Never override a headline the developer supplied; match the rest of the page to its register.
- CTAs meet the same bar at small scale: "Watch a trace", "See the work", "Start your first deploy" beat "Get started" and "Learn more" whenever a named first action exists.

## Logo

**Preserve first.** Search the repo, public assets, manifest, favicon links, and brief. An existing mark is locked - reuse it exactly unless the developer asks for a rebrand; adapt spacing, scale, or lockup around it.

**Cold start only:** a **mark** plus a **wordmark**.

- **Never a letter in a box** - a lone letter on a rounded tile is the logo equivalent of the purple gradient.
- 2-5 primitive shapes, flat fill, one sentence to describe ("two overlapping leaves", "stacked offset swatches", "an upward arc breaking a circle").
- One concept - the single idea the product is about, reduced to its simplest shape.
- Recognizable at 16px - render it small and check.
- Two colors max from the locked palette; balanced in a rough square.
- Wordmark in the locked heading font; mark left (or above for stacked), optically aligned with cap height.
- Save mark and lockup SVGs under `design/assets/logo/`. Wire an SVG favicon (`<link rel="icon" type="image/svg+xml" href="...">`) into `<head>`; PNG/ICO sizes and an OG card need an export tool the developer runs - say so rather than skipping it silently.
- Never source marks from unvetted third-party symbol sites with no verifiable license.
- Record the concept, shapes, and wordmark font in the lock. Don't oversell a constructed mark as bespoke agency work.
