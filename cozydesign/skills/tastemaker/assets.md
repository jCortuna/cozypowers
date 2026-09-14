# Assets

A page with no real photography, illustration, or icons reads as static and generic however good the tokens are. The goal is a **complete page in one pass** - every section that needs a visual has one - using only **attribution-free** sources, so no credit line ever sits on the finished site.

Fetching from external services and saving files into the project is an action the developer should approve - propose the sourcing plan (what, from where, into which folder) before downloading.

## 1. Build an asset cast first

Good pages don't decorate with assets; they cast a small set and reuse it at different scales, crops, and motion. Pick 4-6 roles before markup:

- **Hero anchor** - the thing proving the product exists: a real screenshot, product photo, generated artwork, or constructed scene.
- **Range** - 3-5 visual registers showing the product isn't one layout recolored (where the product has range).
- **Process artifacts** - files, commands, checklists, logs, receipts, annotations that show how it works.
- **Proof** - real logos, avatars, demos, public artifacts. Never invented.
- **Texture object** - one tactile element (paper, stone, fabric, a card, a device, a plant) so the page isn't purely digital.
- **Micro assets** - icons, swatches, arrows, labels, pins, small crops that connect the larger pieces.

Record it (in the reference board or style lock):

```markdown
## Asset cast
- Hero anchor:
- Range:
- Process artifacts:
- Proof:
- Texture object:
- Micro assets:
- Rejected:
```

Assign each section one primary asset role; a section without one must be intentionally text-led (a manifesto moment). If one screenshot family appears more than twice, add a role or crop family.

**Composition patterns** (built with project tokens, no special kit required): an *artifact board* (layered screenshots, notes, swatches, command blocks around one anchor), a *mode runway* (overlapping cards each showing a different aesthetic lane), a *process ledger* (calm file cards with real paths or commands), a *poster break* (one typographic section with one or two tiny image fragments), a *tactile close* (a physical-feeling still life tied to the brand).

**Asset gates:** every important image has a distinct role; at least one section shows range, one shows process, one shows physicality; motion belongs to assets too, not only text; captures live locally in the deployable folder. Anti-patterns: one screenshot repeated in different card sizes, decorative screenshots that teach nothing, a "modes" claim with no visible modes, stock assets that could belong to any product, claims with no visual proof beside them.

## 2. Photography vs illustration - decide per section

- **Factual or physical** (office, product in use, people, places) → real photography.
- **Abstract** (mission, values, an idea, a feature benefit) → illustration.
- If the developer's request uses "illustration" or "illustrate" anywhere, run the illustration workflow for that concept.

Both get filled in the same pass.

## 3. Photography

- **Openverse** (openverse.org, public API, no key) - filter to **CC0** and **Public Domain Mark**, which legally need no attribution. Large and eclectic.
- **Pixabay** - more stock-polished, also attribution-free, needs a free API key; use only when Openverse lacks a clean match.
- **Not Unsplash** for this purpose - its API terms require visible on-site attribution.
- **Credits in code, never on the page:** record creator, source, license, and link for each photo in a comment at the top of the HTML/CSS - a voluntary courtesy invisible to visitors. Never promote it to visible text, and never use this as a loophole for sources that *require* visible credit.

## 4. Icons

- React + Tailwind + shadcn: animated registry icons first (components.md).
- Everywhere else: **Iconify** (`api.iconify.design`, no key) serving open, attribution-free sets - Lucide, Tabler, Phosphor, Heroicons, Material Symbols, Iconoir, Solar, Carbon, MingCute, Fluent. SVGs can be requested pre-tinted (e.g. `https://api.iconify.design/<set>:<icon>.svg?color=%23<hex>`).
- **One set per project** for consistent stroke and corners - but vary the set by mood across projects instead of always reaching for Lucide (e.g. premium → Heroicons or Phosphor, warm → Tabler, technical → Lucide or Carbon, playful → Phosphor or Iconoir, elegant → Material Symbols or Solar - choose between two per project).
- Use icons *in* the design; don't build an end-user "icon picker" feature that re-exposes a set, which some licenses restrict.
- Never emoji as icons, never hand-drawn one-offs when a real set is a fetch away.

## 5. Brand and logo walls - real marks, never text chips

Any "works with", "integrates with", "as seen in", or "compare models" row names real brands and needs their real marks - plain-text chips next to real assets everywhere else read as a stub.

1. Fetch from Iconify's **simple-icons** (monochrome, tintable - usual for a one-tone wall) or **logos** (official multi-color).
2. **Check slugs before declaring a miss** - they often differ from the product name (ChatGPT is `openai`, Gemini is `googlegemini`, Bing Copilot is `microsoftbing`). A request to `https://api.iconify.design/simple-icons:<slug>.svg` returning 200 confirms it.
3. A genuine miss means **drop that item**, not one text chip in a row of real logos.
4. Social platform icons (X, LinkedIn, YouTube, GitHub, Discord, TikTok, Instagram...) come from the same place.
5. Any other icon pack found by search: **verify it has a license** - a public repo with no LICENSE grants no rights.
6. If client trademark policy is a concern, say so rather than silently falling back to text.

## 6. Illustrations - reuse real illustrator work

Model-drawn SVG people and scenes come out as crude pictograms; the quality lives in a real illustrator's path data. So: **match a real unDraw illustration and recolor it**.

**One-time setup:** a personal library at `~/.ideagram/undraw/`, populated by the developer with 20-30 free SVGs from undraw.co spanning common themes (teams, devices, data, growth, communication, security, travel). unDraw's license allows free use without attribution but forbids redistributing a compiled collection - so the library lives on the developer's machine, never in the plugin or a public repo. If it doesn't exist, say so plainly and ask the developer to populate it (a minute, reused across projects), or use the primitive fallback and state the quality drop.

**Workflow:**

1. **Distill** the concept to one sentence plus keywords. Two ideas means two illustrations.
2. **Match** by scene, not loose keywords - list the library, read filenames, open likely candidates. A dashboard concept wants a screen or chart; teamwork wants multiple figures; "an AI assembling a design system" might best match a person laying out screen components. No real fit → say so; don't force it.
3. **Recolor** by copying the original into the project (e.g. `design/assets/illustrations/<name>.svg`) and replacing unDraw's accent `#6c63ff` (match case-insensitively) with the locked accent. Leave everything else: ink `#090814`; greys `#e6e6e6` and `#d6d6e3`; dark clothing `#3f3d56`, `#2f2e41`; skin tones such as `#ed9da0`, `#9f616a`, `#ffb6b6`. Secondary accents `#8ed16f` (green) and `#ff6584` (pink) change only if they should. To change the color again later, start from the original file - the purple is gone from a recolored copy. No brand color given → unDraw's purple is a fine deliberate choice.
4. **Compose (only if no single illustration fits):** lift *whole* components - an entire figure group or device group (`<g transform="translate(...)">` blocks) - into a new SVG as a real scene: background panel, midground device carrying the accent, figure interacting with it, ground shadow. Place with wrapper `translate()`/`scale()`, measuring bounds in the browser rather than guessing through nested transforms. Never graft sub-parts (an arm onto another torso) - coordinate spaces and shading don't join.
5. **Validate:** the SVG must be well-formed XML - notably no `--` inside `<!-- -->` comments, which breaks rendering in strict parsers. Open it in a browser to confirm.
6. **Place it:** reference the file in the section's markup with meaningful `alt` (or inline it). An illustration left unused on disk is not done.
7. **Record** the source (library match, or primitive fallback) in the lock's Assets section.

**How unDraw scenes are built** (useful when composing): figures are one group, back to front - back limbs, trousers (ink), torso (dark clothing), shirt (grey or accent), arms and hands (skin), head (a skin circle), hair (one detailed ink path). Shading is semi-transparent black (opacity 0.05-0.2) over base fills. A whole illustration is a *scene* - background, midground device, figure(s), decorative bits - never a figure floating on white.

**Primitive fallback (last resort):** flat geometric illustration in exactly **two colors** (near-black base `#262631`, one accent from the palette), no gradients or shadows, rounded corners on objects, circles and capsules for organic forms, generous negative space, one concept and one focal point with the accent on it, and a simple figure *doing something* with the prop (e.g. pointing at it) rather than a bare object - unless it's a small inline icon. Distinguish two actors of the same kind by solid vs outlined fill, never a third color. Be upfront that this is simpler than real illustration.

**Other options:** if the session has a real image-generation tool, a generated illustration with one reusable style prompt (saved to the lock) is legitimate - say so. Streamline is a manual exception only with a premium (attribution-free) license or explicit acceptance of its free-tier credit.

**Known limitation:** matching from a finite library means two projects can land on the same base scene recolored differently. A broader library reduces it; say so if it matters.

## 7. Characters and mascots - honestly

1. **Image-generation tool connected?** Generate an original character with one consistent style prompt reused across poses; save the prompt in the lock.
2. **No such tool?** Say so - don't imply a custom mascot was made.
3. **Default fallback:** a geometric SVG character built from primitives in the locked palette - free, consistent, and easy to give tracking eyes for a pointer-reactive hero.
4. **Never approximate a real brand's mascot.** Extract the technique (bold rounded shapes, flat color, a character in the hero, reactive detail) and build something original.
5. Set expectations: a primitive character suits a simple reactive detail, not a full multi-pose character system.

## 8. Logos

See hero-and-copy.md - preserve existing marks; construct a simple geometric mark only on a genuine cold start.

## 9. Last resort and honesty

If an asset truly can't be sourced (no network, no library, developer declines), build it code-native from the locked palette - SVG shapes or CSS - rather than leaving a gap or a grey box, and **say plainly that's what happened**. Save everything under `design/assets/` (photos, illustrations, icons, logos in subfolders) for reuse across screens.
