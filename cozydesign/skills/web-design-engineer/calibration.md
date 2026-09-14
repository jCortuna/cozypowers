# Calibration: Design Read and five dials

Use after gathering context and before declaring the design system. The point is to turn a brief into visible decisions - not to decorate a reply with numbers.

## Design Read

- **Artifact** - landing page, dashboard, prototype, deck, visualization, campaign page...
- **Audience** - who must understand, trust, or act.
- **Visual language** - a specific family: restrained builder SaaS, kinetic editorial, warm humanist, institutional data-first. Never "modern" or "clean".
- **Mode** - greenfield, extension, redesign-preserve, redesign-overhaul.
- **Constraints** - brand, accessibility, platform, viewport, content, deadline, supplied assets.

If two plausible readings would lead to materially different work, ask one focused question. Otherwise state the read and continue.

## The dials (whole numbers, 1-10)

### Visual variance - departure from familiar composition

| Band | Behavior |
| --- | --- |
| 1-3 | Stable grids, symmetry, familiar navigation |
| 4-6 | One or two asymmetric moves, varied section rhythm |
| 7-8 | Strong art direction, off-grid moments, several layout families |
| 9-10 | Experimental; only where comprehension and brand allow |

### Motion intensity - how much meaning travels through time

| Band | Behavior |
| --- | --- |
| 1-2 | Static; state feedback only |
| 3-4 | Hover, focus, short entrances |
| 5-7 | Sequenced reveals, state choreography, restrained scroll response |
| 8-10 | Cinematic transitions, pinning, scrubbing, spatial storytelling |

Every animation must carry hierarchy, feedback, causality, or narrative. Beyond simple feedback, honor reduced motion.

### Information density - useful information per viewport (not clutter)

| Band | Behavior |
| --- | --- |
| 1-3 | Gallery-like; one dominant idea; long pauses |
| 4-6 | Balanced marketing/product density |
| 7-8 | Analytical, operational, comparison-heavy |
| 9-10 | Cockpit; needs strong grouping and progressive disclosure |

### Asset dependence - reliance on real imagery, screenshots, illustration, identity assets

| Band | Behavior |
| --- | --- |
| 1-3 | Type, data, or interface structure can carry it |
| 4-6 | A few key visuals materially help |
| 7-10 | Fails without high-fidelity assets |

At 7+, inventory assets before laying anything out. Never hide missing assets behind decorative CSS.

### Brand fidelity - how strictly existing identity must be kept

| Band | Behavior |
| --- | --- |
| 1-3 | New or exploratory identity |
| 4-6 | Adapt recognizable cues; allow evolution |
| 7-8 | Keep core assets, tokens, voice, signature patterns |
| 9-10 | Extension-level; new work looks native |

## Presets (starting points)

| Brief | Variance | Motion | Density | Assets | Fidelity |
| --- | ---: | ---: | ---: | ---: | ---: |
| Mainstream SaaS landing | 6 | 5 | 4 | 6 | 5 |
| Creative studio / campaign | 8 | 7 | 3 | 8 | 4 |
| Developer tool landing | 6 | 5 | 5 | 6 | 6 |
| Data dashboard | 4 | 3 | 8 | 3 | 7 |
| Public-sector service | 3 | 2 | 6 | 3 | 9 |
| Editorial presentation | 7 | 5 | 4 | 7 | 5 |
| Existing-product extension | match | match | match | match | 10 |
| Redesign - Preserve | current +1 max | current +1 max | match | match | 9 |
| Redesign - Overhaul | 6-8 | 4-7 | match content | 6-9 | 5-7 |

## Resolving conflicts

- **High variance + high density** → keep a stable navigation and grid spine; experiment in one layer only.
- **High motion + high density** → animate transitions and focus, not every element.
- **High assets + low fidelity** → write a new visual bible before sourcing or generating a set.
- **High assets + high fidelity** → official assets first; generation may extend the world but never replace identity-critical material.
- **High fidelity + overhaul** → name which brand invariants survive before changing the language.
- **Accessibility beats every dial.** Reduce motion, clarify hierarchy, and keep contrast without asking.

## Optional image-first exploration

Worth it only for visually critical greenfield or overhaul work (campaign page, brand launch, product hero, art-directed portfolio). Skip it when Figma/screenshots/a mature system exist, for extensions, repairs, dashboards, forms, and tables, when the open question is behavior rather than look, or when generation adds cost without reducing risk.

When used: define a visual bible (palette, type character, radius, material, image treatment, forbidden drift); generate only the references that resolve real uncertainty; prefer clean section-level references over cropping details from a compressed full-page board; extract implementation decisions; when generated pixels conflict with code or supplied brand assets, the latter win. If no image tool is available, list honest asset requirements instead.

## Completion test

Calibration worked only if someone can point from each dial to a concrete consequence in the artifact. If changing a score wouldn't change the plan, drop the score or make the mapping explicit.
