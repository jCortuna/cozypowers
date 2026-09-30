# Changelog

All notable changes to cozypowers are documented here.

## [Unreleased]

### Added
- `validating-claims` skill and `/validate-claim` command — score a claim's
  correctness and completeness (0-100 each, with a verdict) against one named
  source using only that source. Judging runs in a fresh sub-agent that sees
  nothing but the claim, the source, and `procedure.md`; every label must carry
  a verbatim quote and location.
- `cozydesign` companion plugin (v1.0.0) in the same marketplace: 15 markdown-only design-engineering skills - `design-engineering`, `animate`, `web-design-engineer`, `landing-page-design`, `video-to-superprompt`, `awwwards-quality-sites`, the `better-*` review family, `interface-review`, and `tastemaker`. Clean-room recreations of community design skills; see `cozydesign/CREDITS.md`.
- Marketplace description in `marketplace.json`.
- `designing-interfaces` skill and `/design` command — UI/UX design intelligence
  backed by a local 2,374-row corpus (192 colour palettes, 192 product profiles,
  192 reasoning rules, 119 UX guidelines, 105 icons, 88 styles, 74 font pairings,
  44 React performance rules, 34 landing patterns, 32 app-interface rules, 25
  chart types, 17 motion presets, 22 technology stacks). Ported from
  [UI/UX Pro Max](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill)
  (MIT © 2024 Next Level Builder) with its Python search engine replaced by a
  documented Grep procedure, preserving the plugin's zero-executable-code rule.

### Changed
- `shipping` now runs the interface pre-delivery checklist when a change is
  player- or user-visible.
- README's audit instructions updated: the plugin now contains CSV data files, so
  the file-type check and the note about URLs in the corpus were corrected.

## [1.1.0] - 2026-08-23

### Added
- `shaping-specs` skill and `/spec` command — turn a feature idea into a reviewed spec folder (plan, shape, standards, references) before planning starts.
- `writing-plans` now checks for project-level `standards/`, `product/`, and `specs/` context before drafting a plan.

## [1.0.0]

### Added
- Initial release: `brainstorming`, `writing-plans`, `executing-plans`, `test-driven-development`, `systematic-debugging`, and `shipping` skills, with `/brainstorm`, `/plan`, `/execute`, `/debug`, and `/ship` commands.
