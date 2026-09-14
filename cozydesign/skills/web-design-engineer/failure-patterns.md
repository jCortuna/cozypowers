# Failure patterns

Recurring ways generated designs go wrong. Read only the sections relevant to the artifact. Each is a strong default with exceptions, not a universal law: **default → why → how to detect → exceptions → repair**.

## Marketing and multi-section pages

**Eyebrow on every heading.** A tiny uppercase label above every section heading creates a mechanical rhythm. *Detect:* label + headline + paragraph repeats in most sections. *Exceptions:* manuals, deliberately indexed editorial systems, established brand pattern. *Repair:* drop low-information labels; vary the lead-in (a sentence, image, number, quote, or just the headline).

**Zigzag monotony.** Three or more alternating image/text splits in a row. Mirroring is not composition. *Repair:* break the run with a full-width proof point, a vertical narrative, a comparison, a gallery, a diagram, or a focused text moment.

**Default centered hero.** Centered headline + gradient + two buttons, chosen without the brief supporting it. *Exceptions:* manifestos, launch statements, search-first utilities, ceremonial pages. *Repair:* recompose from content hierarchy, the role of the key asset, audience, and viewport.

**Trust theater.** Invented metrics, testimonials, client logos, security badges, "used by" claims. False credibility is worse than an honest gap. *Repair:* labelled placeholders or real proof.

**CTA sprawl.** "Get started", "Try free", and "Create account" all do the same thing. *Exceptions:* tested funnel copy, genuinely different commitment levels. *Repair:* one label per intent, or make the difference explicit.

## Layout and components

**Cardification.** Every paragraph, metric, and icon in its own rounded card. Containers should mean grouping, selection, or elevation. *Repair:* whitespace, alignment, dividers, typography, or a single shared surface.

**Bento without rhythm.** Filler cells, uniform text tiles, arbitrary spans. *Repair:* match cell count to real content; create hierarchy through size, media, data, or interaction - not empty geometry.

**Shape drift.** Pills, sharp cards, soft cards, and circles with no rule. *Repair:* assign radius by component role; consolidate tokens.

**Split-header filler.** Big headline left, small floating paragraph right, the split communicating nothing. *Repair:* stack them, or give the second column a real job (visual, action, evidence).

## Typography and content

**Generic display type.** Reflexively choosing Inter, Roboto, Arial, system-ui, Fraunces, or Instrument Serif as the identity-bearing face. *Exceptions:* brand/system requirement, accessibility contexts, deliberate platform neutrality. *Repair:* the recipe's font, the brand font, or a justified pairing.

**Micro-label noise.** Decorative version numbers, fake coordinates, weather, status dots, section numbers, or metadata that helps no one. *Repair:* delete it or bind it to real state.

**Copy-shaped decoration.** Vague claims, fake precision, agency slogans, captions that only fill space. *Repair:* real copy from the developer, a clear placeholder, or fewer words.

**Unreadable hero.** CTA falls below the intended first viewport, display text clips, copy and image fight. *Repair:* recompose - don't impose an arbitrary word or line cap.

## Imagery and brand

**CSS as counterfeit asset.** Decorative shapes standing in for a recognizable product, logo, or interface. *Repair:* official material, a clearly non-identity-critical generated extension, or an honest asset slot.

**Labels on images.** Pills and captions overlaid on imagery that neither identify, control, nor explain it. *Repair:* move needed metadata to a stable caption, or remove it.

**Generated-world drift.** A set of generated images wanders in palette, material, lighting, type character, device treatment, or brand symbols. *Repair:* keep a visual bible; regenerate the off frame rather than patching it with decoration.

## Motion and interaction

**Spectacle-only motion.** If removing the animation changes no understanding or feedback, it's decoration. *Repair:* remove it, lower the motion dial, or bind it to meaningful state.

**Scroll-state rendering.** Updating broad React state on every scroll or pointer frame. *Repair:* CSS, motion values, IntersectionObserver, or an animation library suited to the stack.

**Stacked spectacle.** Multiple marquees, pinned chapters, magnetic buttons, and ambient loops on one surface. *Repair:* choose one signature moment; quiet the rest.

**No reduced-motion path.** Anything beyond simple state feedback must collapse cleanly, preserving content order and task completion.

## Dashboards and product UI

**Marketing styling on operational UI.** Giant headlines, lavish whitespace, cinematic cards that slow scanning. *Repair:* raise density, stabilize the grid, clarify state, prioritize task completion.

**Decorative data viz.** Gradients, 3D, shadows, or animation obscuring comparison. *Repair:* better data-ink ratio, direct labels, semantic color, accessible alternatives.

**Happy-path-only components.** Only the populated success state exists. *Repair:* loading, empty, error, permission, disabled, and overflow states as relevant.

## Using this file

Report only consequential failures - never paste the catalog at the developer. Fix safe in-scope problems directly; surface exceptions and trade-offs that affect intent.
