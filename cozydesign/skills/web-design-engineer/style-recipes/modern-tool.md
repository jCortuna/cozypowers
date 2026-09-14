# Modern tool / builder SaaS recipes

Quiet luxury for tools: hairline detail, restraint, a single accent. Reads as "made by people who use tools". Shared rules: [../design-directions.md](../design-directions.md).

---

## linear - Linear

- **Vibe:** warm dark, hairline precision, restraint as confidence. **Best for:** dev tools, AI tools, serious-but-designed B2B SaaS. **Touchstone:** linear.app, its changelog.
- **Palette:** ground `#08090A` (warm near-black); surfaces `#16171C`, `#1E1F25`, raised `#26272E`; hairline `rgba(255,255,255,0.06)`; text `#F7F8F8` / `#9CA3AF` / `#6B7280`; accent purple `#5E6AD2` on under 5% of pixels; hero-only gradient mesh under 8% opacity.
- **Type:** display Inter Tight 600 (or Söhne, Geist Sans) at -0.02em - never plain default Inter; body Inter 14-15px, 400-500, 1.55; mono (Geist Mono, JetBrains Mono, Berkeley Mono) for code and shortcut chips.
- **Spacing:** 4 / 8 / 12 / 16 / 24 / 40 / 64 / 96.
- **Radius:** 6 small / 12 cards / 16 large - never above 16. **Shadow:** `0 1px 2px rgba(0,0,0,0.3)` on raised surfaces; never glows or colored shadows.
- **Motion:** ~150ms ease-out hovers; 350-450ms layout moves on a quint curve such as `cubic-bezier(0.22, 1, 0.36, 1)`; snappy, not bouncy.
- **Signature moves:** 1px low-opacity hairlines between every panel; accent only on focus/active states, tiny pills, key brand surfaces; inline code in mono on `#1E1F25` with `#A78BFA` text; a barely-there hero mesh (not the loud AI gradient); keyboard shortcut chips everywhere; a real product screenshot anchored at the bottom of the landing hero.
- **Avoid:** emoji; springy/elastic easing; a second saturated color; radius above 16; stock people; 2018-style "Get Started Free" hero buttons.
- **Prompt seed:** abstract product UI, warm dark `#08090A`, hairline borders, `#16171C`/`#1E1F25` panels, faint blue-violet light along the top edge, no people, no text, 16:9.
- **Don't use when:** playful consumer brands; products needing warmth; non-technical audiences.

---

## vercel-mesh - Vercel (gradient-mesh era)

- **Vibe:** black-and-white precision broken by one shimmering mesh. **Best for:** platforms, infrastructure, technical AI products. **Touchstone:** vercel.com, nextjs.org.
- **Palette:** ground `#000000`; surfaces `#0A0A0A`, `#111111`; hairline `#1F1F1F` or `rgba(255,255,255,0.08)`; text `#EDEDED` / `#888888`; mesh hues blue `#0070F3` → magenta `#FF0080` → orange `#F5A623`, low saturation and heavily feathered, hero/section breaks only; primary button white on black.
- **Type:** Geist Sans 500-600 display (substitute Inter Tight 600); body Geist 15-16px / 1.6; Geist Mono for code, commands, deploy logs.
- **Spacing:** 4 / 8 / 16 / 24 / 40 / 64 / 96 / 128.
- **Radius:** 8 / 12 / 16. **Shadow:** minimal on components - the page is lit by the mesh.
- **Motion:** `cubic-bezier(0.16, 1, 0.3, 1)`; 200ms hovers; 500-700ms layout; the mesh drifts on a 10-20s loop.
- **Signature moves:** one diffuse full-bleed hero mesh fading to black; everything else black-and-white with hairlines and mono accents; realistic deploy/terminal logs as a hero element; cards that glow softly from below on hover; flat white buttons.
- **Avoid:** saturated purple-pink gradients (the cliché this replaces); more than one mesh; glow on everything; colored buttons.
- **Prompt seed:** diffuse atmospheric gradient on pure black, deep blue into magenta and orange, feathered edges, soft focus, very low saturation, no objects, 16:9.
- **Don't use when:** not a platform/tooling product (reads as trying too hard); multiple meshes needed; warm, human brands.

---

## raycast - Raycast

- **Vibe:** glassy command palette, keyboard-first, color used just enough to feel playful. **Best for:** productivity tools, launchers, dev utilities. **Touchstone:** raycast.com and its store.
- **Palette:** ground `#0F0F11`; translucent surface `rgba(255,255,255,0.06)` over a colorful backdrop; hairline `rgba(255,255,255,0.10)`; text `#FFFFFF` / `#B0B3B8`; brand red `#FF6363` on icons and key CTAs; bright per-extension colors (lime, coral, lavender, cyan) as small dots only.
- **Type:** Söhne or Inter Tight 600 display at -0.02em; body Inter 14-15px at 500 (punchier than Linear); SF Mono or JetBrains Mono for shortcut chips.
- **Spacing:** 4 / 8 / 12 / 16 / 24 / 40 / 64.
- **Radius:** 8 / 12 / 16 cards / 24 large modal. **Shadow:** cushioned `0 16px 40px rgba(0,0,0,0.4)` under the palette; little elsewhere.
- **Motion:** mild-overshoot springs welcomed for signature moments (palette appearing, tile lift); 150ms ease-out otherwise.
- **Signature moves:** a floating, slightly tilted command-palette screenshot with a soft blurred color backdrop showing through the glass; every shortcut as a mono chip (⌘ ↵ ⌥) with hairline border; tiny per-tile color dots; soft orange-to-magenta banded backdrop behind the hero; generous sections with clear hover lift.
- **Avoid:** too many bright colors on one screen; solid bright buttons (use translucent pills with chips); fully monochrome scenes.
- **Prompt seed:** floating command palette centered over a soft-focus warm orange/magenta gradient, dark charcoal UI, cushioned shadow, no people, 16:9.
- **Don't use when:** not a keyboard-first/launcher product; audiences who don't use shortcuts; strictly enterprise tone.

---

## notion-pre-ai - Notion (c. 2017-2022)

- **Vibe:** friendly serif headlines, emoji as structure, soft cream and warm ink. **Best for:** collaborative tools for non-engineers, "second brain" products. **Touchstone:** pre-2023 notion.so via the Wayback Machine.
- **Palette:** ground `#FFFFFF`; cream surface `#F7F6F3`; ink `#37352F`; secondary `#787774`; hairline `#E9E9E7`; soft block tints mint `#E4F4F1`, peach `#FFEDD5`, rose `#FCE7F3`, sand `#FEF3C7` - backgrounds, never bright accents.
- **Type:** friendly modern serif display (GT Sectra, Sentinel, Source Serif) at 500; body Inter or Söhne 16px / 1.6; emoji at 1.25x body as section markers and page icons.
- **Spacing:** 4 / 8 / 16 / 24 / 40 / 64.
- **Radius:** 4 / 8 / 16. **Shadow:** `0 2px 8px rgba(15,15,15,0.04)` - felt, not seen.
- **Motion:** 200-300ms ease-out; cards lift 2-4px with a slightly wider shadow on hover.
- **Signature moves:** one emoji per section header as the hierarchy marker; simple black line-drawn doodles in the hero; visibly block-based layout; soft color-tagged pills; conversational microcopy.
- **Avoid:** emoji clusters; dark mode unless required; sans headlines; aggressive CTAs.
- **Prompt seed:** simple black-line doodle of a tidy desk with notebooks and plants on cream `#F7F6F3`, small washes of mint and peach, 3:2.
- **Don't use when:** serious enterprise audiences; graphics-heavy products; authoritative voices.
