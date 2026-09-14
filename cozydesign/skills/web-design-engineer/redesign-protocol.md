# Redesign protocol

Read before changing an existing visual product.

## 1. Classify the mode

- **Extension** - add or change a bounded element inside the current system. Match its vocabulary. Don't "improve" unrelated surfaces.
- **Redesign - Preserve** - modernize while keeping identity, information architecture, voice, and behavior. Targeted evolution.
- **Redesign - Overhaul** - new visual language, same agreed product, content, and technical contracts. Not a licence to rewrite everything.

If preserve vs overhaul would change the result and the request is ambiguous, ask one focused question.

## 2. Audit before editing

Record the current state in a short redesign brief.

**Visual system:** color roles and real usage ratios; type families, scale, weights, line lengths; spacing rhythm and container widths; radius, border, shadow, elevation rules; icons, illustration, photography treatment; motion durations, easing, triggers.

**Product and content:** page tree, navigation, key journeys, conversion paths; content blocks and their purpose; voice, legal copy, localization, real data; loading, empty, error, disabled, permission states.

**Technical contracts:** routes, slugs, anchors, deep links; form field names, order, validation, autofill; analytics events, data attributes, test selectors, experiment hooks; component APIs and consumers; semantics, keyboard behavior, focus order, announcements; SEO metadata, canonicals, structured data, social cards.

**Sort observations into:** *Preserve* (recognizable or contract-critical strengths), *Improve* (weak hierarchy, spacing, contrast, responsiveness, craft), *Remove* (clutter, broken patterns, dead interactions, fabricated content).

## 3. Protected contracts - never change silently

- Routes, slugs, anchor IDs, primary nav labels
- Logo, wordmark, identity-critical assets
- Form field names/order and submission behavior
- Legal, consent, privacy, pricing, compliance copy
- Analytics events, selectors, experiment IDs
- Existing accessibility wins
- Public component APIs and persisted-state keys
- The developer's content and real data

If the outcome genuinely requires changing one, ask first.

## 4. Modernization order

Use the lowest-risk lever that solves the problem, then reassess:

1. Fix functional and accessibility failures.
2. Repair hierarchy and typography.
3. Normalize spacing, alignment, responsiveness.
4. Consolidate tokens; remove rogue styles.
5. Improve states and feedback.
6. Add justified motion.
7. Recompose the hero or key sections.
8. Replace whole blocks only when they can't be repaired.

In Preserve mode, stop as soon as the brief is met. Incremental work must not become a portfolio redesign.

## 5. Dials by mode

- **Extension:** match every dial; brand fidelity 10.
- **Preserve:** keep density and assets; move variance and motion by at most one point unless asked.
- **Overhaul:** derive variance and motion from the brief, but keep a content-density map so nothing is lost.

## 6. Decision record (non-trivial redesigns)

```text
Mode:
Preserve:
Improve:
Remove:
Protected contracts:
Design Read + dials:
Highest-risk change:
Rollback / fallback:
```

A record, not an essay.

## 7. Verification

The default self-check confirms scope and protected contracts by inspection. Hands-on browser acceptance runs only when asked (see browser-acceptance.md) and should include regression checks on preserved journeys.
