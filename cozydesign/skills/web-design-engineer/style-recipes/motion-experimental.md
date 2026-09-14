# Motion / experimental recipes

Movement and surprise *are* the brand; a static screenshot can't capture it. Reach for this school only when motion genuinely is the point - it is the most labor-intensive. Shared rules: [../design-directions.md](../design-directions.md).

---

## field-io - Field.io (generative motion identity)

- **Vibe:** the page generates itself in front of the visitor. **Best for:** brand films, launches, agency portfolios, "the visit is the experience". **Touchstone:** field.io.
- **Palette:** dark base `#0B0B0F` to `#000000`; one or two generative hues cycled through the motion (e.g. cyan `#0CE0E5` blending to violet `#5B2EFF`, or procedural); type `#FFFFFF`; secondary `#A0A4B0`.
- **Type:** a variable display face whose axes animate (Söhne Variable, Editorial New Variable, Inter Display Variable) - weight, width, or optical size morph on scroll; body a single restrained grotesque.
- **Spacing:** deliberately irregular; content lands in unexpected places; the grid appears and disappears. **Radius:** 0. **Shadow:** from generative lighting in WebGL/canvas, not CSS.
- **Motion:** the whole recipe - multi-stage choreography; scroll drives state changes, not just parallax; long-tail curves such as `cubic-bezier(0.83, 0, 0.17, 1)`.
- **Signature moves:** letters appearing, morphing, and resolving into headlines on scroll; particle or mesh systems reacting to cursor and scroll; section breaks where a full-bleed canvas takes over the layout; staggered multi-element entrances.
- **Avoid:** treating it as static; too many cursor-reactive elements (one or two WebGL moments); heavy reading content.
- **Prompt seed:** generative type - one phrase resolving from a particle field, violet `#5B2EFF` and cyan `#0CE0E5` light traces on near-black, long motion trails, 16:9 cinematic.
- **Don't use when:** it will live as a static image (loses ~70% of impact); small build budget; low-end hardware or accessibility/performance-first audiences.

---

## active-theory - Active Theory (cinematic WebGL)

- **Vibe:** a film you move through; physical-feeling interaction. **Best for:** launch sites, games and entertainment, experiential marketing. **Touchstone:** activetheory.net.
- **Palette:** black plus one dramatic signature hue drawn from the content; high contrast; tinted neutrals only (cool cast for sci-fi, amber for cinematic) - never flat gray.
- **Type:** strong grotesque or campaign-specific display (Druk, Editorial New, ABC Diatype Mono); frequent all-caps with very tight or very open tracking; little body copy - witnessing over reading.
- **Spacing:** cinematic - content centered or tucked in corners over a full-bleed canvas. **Radius:** 0. **Shadow:** WebGL lighting.
- **Motion:** feature-film grade; scroll is the camera path; physics debris and particles.
- **Signature moves:** full-screen WebGL hero traversed by scrolling; real-time physics reacting to cursor or device tilt; art-directed scene transitions (not generic fades); optional ambient sound that ducks under text; one maximum-impact payoff frame.
- **Avoid:** many small WebGL moments (one set-piece); content-heavy sites; off-the-shelf Three.js demos (generic WebGL reads cheap).
- **Prompt seed:** cinematic VFX still from a sci-fi launch film, single key light, deep shadows, one accent hue in the scene, particle debris, 2.39:1.
- **Don't use when:** performance or accessibility rules out heavy WebGL; utilitarian products; builds under ~3 weeks.

---

## resn-storytelling - Resn (story through scroll)

- **Vibe:** surprise is the reward; the page tells a story to whoever keeps scrolling. **Best for:** brand storytelling, campaign microsites, portfolios. **Touchstone:** resn.co, site-of-the-day archives.
- **Palette:** project-driven; often warm against cool within one piece; saturated where the story peaks, muted where it breathes.
- **Type:** a campaign-specific or unusual display face; quiet humanist sans body at small sizes; titles often live *inside* the 3D scene rather than on a UI layer.
- **Spacing:** composition-driven, not grid-strict. **Radius / shadow:** per project; shadows baked into scenes.
- **Motion:** long-form choreography - e.g. a 90-second story across 8-12 scroll triggers with payoffs at set moments.
- **Signature moves:** scroll triggers reveal narrative beats (a character crosses, a product unveils, a punchline lands); easter eggs for returning visitors; cursor-reactive materials or audio cues; each section art-directed as its own scene; a reward scene only for those who finish.
- **Avoid:** too many beats (fewer, better); decoration that doesn't advance the story; forgetting the payoff.
- **Prompt seed:** mid-action scene from a brand microsite, subject in motion with intentional blur, warm-cool contrast, theatrical lighting, 16:9.
- **Don't use when:** there's no story; impatient audiences; rushed builds.
