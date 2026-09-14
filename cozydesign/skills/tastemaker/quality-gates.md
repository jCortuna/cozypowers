# Quality gates

Two checks bracket every build: a **pre-emit self-critique** (before finalizing, while fixes are cheap) and the **gate sweep** (after building). Then a **manual scan** with search patterns stands in for automated scanners.

## Pre-emit self-critique

Score the planned output 1-5 on six axes. **Anything below 3 triggers a revision pass** before the gate sweep. Two passes is normal; needing a third usually means the brief is underspecified - reread it.

| Axis | Question |
| --- | --- |
| **Show-don't-tell** (score first) | Is each section mostly something to look at, with text as caption - or prose with a decorative icon? |
| **Philosophy** | Does the design take a position, a reason it looks like *this*? |
| **Hierarchy** | Primary, secondary, tertiary obvious in two seconds? |
| **Specificity** | Recognizably *this* product - or anyone's page in different colors? |
| **Restraint** | Has everything not earning its place been removed? |
| **Variety** | Structurally distinct from previous builds (a palette swap doesn't count)? |

Record the scores in the build stamp.

## Gate sweep

Every gate must land on the safe side. Mood notes loosen or tighten a gate for one mood; otherwise it binds all.

### Show-don't-tell and structure

1. **Visuals carry the meaning.** "Fast analytics" → a real chart; "3-step setup" → three visual panels; "powerful editor" → a mockup. Proof sections built from tiny label-plus-icon cards floating in empty space fail too - use an annotated capture, a real chart, or a constructed diagram.
2. **A named macrostructure**, not hero → 3 cards → testimonial → CTA → footer; no two sections share an archetype.
3. **Structure differs from the last build** (stamp and log present; macrostructure, nav, footer, hero all rotated).
4. **A real narrative arc** - four or more beats, a product-specific problem beat, a proof beat with real evidence.
5. **No template chrome** - no reflexive minimal nav on a multi-destination product, no reflexive four-column footer, no eyebrow-left/heading-right section heads, no hand-drawn fake browser/phone/IDE chrome.
6. **One intentional rule-break** - something that bleeds, an oversized number, an asymmetric moment. Perfectly safe pages read as generated.

### Hero and logo

7. **Five-second and subtraction tests pass** (hero-and-copy.md).
8. **Fits the fold at 1280x800** with headline sized to word count, short headlines capped, descenders clear. *Elegant/premium may run a taller art-directed fold, still a complete composition.*
9. **Hero motion in ≤4 beats**, not every label staggered.
10. **Not centered-everything** - at most two of eyebrow/headline/lede/CTA on one centered axis. *Playful and narrow elegant may center, with eyebrow or CTA off-axis.*
11. **No mid-page headline at hero scale** (≈50-65% max, 1-2 lines), except one stated statement moment.
12. **A real mark**, not a letter in a box; readable at 16px.
13. **Existing brand assets preserved.**

### Color and contrast

14. **Not the default gradient** - no indigo→purple or blue→cyan hero/button gradients; no gradient-clipped headline text in any mood.
15. **Every pairing used is in the color contract** for its purpose (badge label on fill, disabled, hover, state borders), not just body on background.
16. **The usual shipped failures:** button text within ~5% lightness of its fill; a dark panel (OKLCH L < 50%) still using dark text or leaving children dark; an accent used as a text-bearing fill with no verified on-accent color.
17. **Neutrals tinted toward the anchor hue.** *Technical and deliberately monochrome builds may use zero-chroma neutrals.*
18. **Accent ≤ ~5% of any viewport.** *Playful may run higher.*
19. **Nothing violates the lock's Do-not list.**

### Spacing and layout

20. **Spacing on the scale; internal padding ≤ external gaps;** content cards ≥24px; no stray `17px` values.
21. **Unequal two-column sections are balanced deliberately** - center, fill with a real supporting element, or cap; never three cards at the top with dead space below.
22. **One section-separation mechanism** at every boundary.
23. **Landing sections breathe** - pivotal sections 128-192px per side, adjacent gaps ~120-250px on desktop. *Not for app shells.*
24. **Density matches the mood.**
25. **No horizontal scroll 320-1920px:** `overflow-x: clip` (not `hidden`, which breaks sticky) on html and body; image grid tracks `minmax(0, 1fr)`; display headings `overflow-wrap: anywhere; min-width: 0`.
26. **No two-line clickable text** (buttons, nav, tabs, breadcrumbs, CTAs) at any width; 44px targets below 40rem.

### Motion

27. **Not static** - marketing screens have reveals and at least one scroll-story beat; app shells have panel, list, and state motion.
28. **No `transition: all`.**
29. **Only transform and opacity animate** (no width, height, top, left, margin, padding).
30. **No blanket hover-scale, no stacked hover effects, no overshoot easing on UI state**; named curves, not browser `ease`.
31. **Focus rings appear instantly** (never transitioned in) at ≥3:1.
32. **Reduced-motion fallback everywhere** - spatial motion becomes a ≤150ms opacity crossfade.
33. **Motion carries information** - prefer silent success, optimistic update + undo, ~800ms hover-tooltip delay and 0ms on focus. If removing an animation loses nothing, remove it.
34. **Motion craft passes** (animate skill's never-ship list): no `ease-in` on UI, no `scale(0)`, hover gated by pointer media query, UI durations ≤300ms unless modal/drawer/story.

### Typography

35. **No emoji as icons.**
36. **No monospace body copy.**
37. **Display line-height ≥1.0** on bold large headlines (higher for CJK), checked visually.
38. **No italic headings** - including a single italic emphasis word inside an upright heading. Italic only as body-copy emphasis.
39. **At most three families** (display, body, one outlier used in ≤2 places).

### Assets, states, honesty

40. **No asset-empty sections.**
41. **App states are real** - loading, empty, error, disabled, focus, hover, pressed, success.
42. **Assets share one DNA** - one icon library, consistent stroke and color treatment.
43. **SVGs are well-formed** - notably no `--` inside XML comments, which breaks rendering in strict parsers; open the file in a browser to confirm.
44. **Charts have a one-line caption and were actually looked at** - lines span the range, bars match labels, parts sum sensibly.
45. **Inputs:** border width constant across states (state via color/outline/shadow); disabled shown by opacity + `cursor: not-allowed` + the native attribute; input height matches adjacent buttons.
46. **Real content** - no lorem ipsum, "Jane Doe", "Acme", "Nexus".
47. **No invented metrics, testimonials, logos, or counts** - real, or an honest "metric to confirm" placeholder.
48. **No token improvisation** - every color and font family comes from a named token; lift stray literals into the token block.
49. **No visible attribution lines** - credits live in a code comment; a visible credit means an attribution-requiring source slipped in.
50. **Fallbacks stated honestly.**
51. **No captions narrating what the visual already shows**, and never a caption defending its own authenticity ("this is the real product").

### Generic-taste tells (reflect, don't just tick)

52. **Not the same pill eyebrow on every section.**
53. **Semi-brutalist (hairlines, flat fills, mono, sharp radius) is a choice that fits this product** - not the house default.

## Manual scan (in place of automated scanners)

Search the changed UI files for these patterns and review every hit. HIGH must be fixed before handoff; MEDIUM needs a fix or a stated reason the brief earns it.

| Pattern to search | Severity | Why |
| --- | --- | --- |
| `—` (em dash) in shipped copy | HIGH | Hard copy ban |
| `transition: all`, `transition-all` | HIGH | Motion tell |
| `from-indigo`/`to-purple`/`from-purple`/`to-cyan` gradients, `linear-gradient(` with violet/indigo/cyan stops on heroes or buttons | HIGH | Default gradient |
| `bg-clip-text`, `background-clip: text` on headings | HIGH | Gradient headline |
| Emoji characters in headings, feature lists, buttons (✨🚀⚡🔥🎯✅) | HIGH | Emoji icons |
| `<img` without `alt` | HIGH | Accessibility |
| `href="#"` or empty `href` | HIGH | Dead links |
| `lorem`, `Lorem`, `Jane Doe`, `John Doe`, `Acme`, `Nexus` | HIGH | Placeholder content |
| `outline-none` / `outline: none` without a `:focus-visible` style | HIGH | Invisible focus |
| `user-scalable=no`, `maximum-scale=1` | HIGH | Blocks zoom |
| `onPaste` with `preventDefault` | HIGH | Blocks paste |
| `ease-in` (not `ease-in-out`) on UI transitions | MEDIUM | Sluggish feel |
| `scale(0)`, `scale-0` entrances | MEDIUM | Appears from nothing |
| Transitions/animations on `width`, `height`, `top`, `left`, `margin`, `padding` | MEDIUM | Layout thrash |
| `:hover` / `hover:` motion without `(hover: hover)` gating | MEDIUM | Sticky touch hovers |
| Animation code with no `prefers-reduced-motion` anywhere | MEDIUM | Motion accessibility |
| Durations above `300ms` on UI elements | MEDIUM | Needs a reason |
| `h-screen` / `100vh` on heroes | MEDIUM | Mobile viewport jump - prefer `svh`/`dvh` or content height |
| elevate, seamless, unleash, next-gen, supercharge, revolutionize, game-changer, delve | MEDIUM | AI copy vocabulary |
| Template headlines ("The ... way to", "... made easy", "Everything you need to") | MEDIUM | Sentence templates |
| Repeated identical eyebrow/label markup on most sections | MEDIUM | Eyebrow spam |
| Imports from two or more icon packages | MEDIUM | Pulled components not unified |
| Imports from two or more motion engines (beyond the sanctioned GSAP-for-page + Motion-for-registry-icons pairing) | MEDIUM | Incoherent motion |
| Many distinct hard-coded `box-shadow` or `border-radius` literals instead of tokens | MEDIUM | Un-restyled components |
| Raw hex/`rgb(`/`oklch(` or `font-family:` literals outside the token block | MEDIUM | Token improvisation |

A clean scan is a floor, not the review - the gates decide the work.
