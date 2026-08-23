# Changelog

All notable changes to cozypowers are documented here.

## [Unreleased]

### Added
- `designing-interfaces` skill and `/design` command — UI/UX design intelligence
  backed by a local 2,374-row corpus (192 colour palettes, 192 product profiles,
  192 reasoning rules, 119 UX guidelines, 105 icons, 88 styles, 74 font pairings,
  44 React performance rules, 34 landing patterns, 32 app-interface rules, 25
  chart types, 17 motion presets, 22 technology stacks). Ported from
  [UI/UX Pro Max](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill)
  (MIT © 2024 Next Level Builder) with its Python search engine replaced by a
  documented Grep procedure, preserving the plugin's zero-executable-code rule.
- `shaping-specs` skill and `/spec` command — turn a feature idea into a reviewed spec folder (plan, shape, standards, references) before planning starts.
- `writing-plans` now checks for project-level `standards/`, `product/`, and `specs/` context before drafting a plan.

### Changed
- `shipping` now runs the interface pre-delivery checklist when a change is
  player- or user-visible.
- README's audit instructions updated: the plugin now contains CSV data files, so
  the file-type check and the note about URLs in the corpus were corrected.

## [1.0.0]

### Added
- Initial release: `brainstorming`, `writing-plans`, `executing-plans`, `test-driven-development`, `systematic-debugging`, and `shipping` skills, with `/brainstorm`, `/plan`, `/execute`, `/debug`, and `/ship` commands.
