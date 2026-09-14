---
name: awwwards-quality-sites
description: Art-direct and build distinctive, motion-rich marketing, editorial, portfolio, and landing websites - an original visual concept, a standout hero, GSAP choreography, exactly one smooth-scroll engine, optional purposeful Three.js shaders, honest asset/icon/logo sourcing, accessibility, and performance safeguards. Use when asked for an "Awwwards-quality", premium, cinematic, interactive, high-concept, or motion-led website.
---

# Awwwards-Quality Sites

Build a site whose visual idea, media, typography, and motion all tell the same story. "Awwwards quality" is an **acceptance bar** - never a claim that the site has won or will win anything.

## 1. Set the art direction

- Study the developer's references fully before building, but extract only high-level traits: hierarchy, pacing, contrast, image treatment, motion principles.
- Create a **materially new** identity, layout, copy system, imagery, and interaction language. Never reuse, trace, or closely reproduce reference assets, screenshots, code, identity, or copy.
- Anchor the look in one coherent system - e.g. a single style recipe from the **web-design-engineer** skill - and don't blend unrelated aesthetics.
- Before coding, write a compact direction: **visual thesis**, hero focal asset, type hierarchy, color system, section sequence, motion narrative, chosen smooth-scroll engine, Three.js decision, and where every asset will come from.

## 2. Build an honest asset system

- Generate original hero or project imagery when it materially strengthens the concept; use properly licensed media when that's stronger. Keep provenance noted in the source.
- **Don't draw illustrations with model-authored SVG, CSS, or canvas paths.** Use original generated or licensed transparent PNG cutouts for illustrative elements. Simple authored brand marks, interface icons, data graphics, and a justified shader canvas are fine.
- **Avatars are photographs** - provided or properly licensed. No initials, illustrated heads, or silhouettes, and never generated people presented as real customers, staff, or endorsers.
- **Icons:** a single consistent set (e.g. Solar via Iconify). **Real company logos** (e.g. Iconify's SVG Logos) only in truthful contexts. **Placeholder logos** (e.g. Logo Ipsum) only for clearly disclosed fictional specimens, never as customer proof. No honest proof → no logo wall.
- Set deliberate aspect ratios, crop behavior, alt text, loading strategy, and missing-media fallbacks. No generic stock, copied mockups, watermarks, or media without a narrative role.

## 3. Compose the hero

- The first viewport is the site's strongest authored moment: a clear message and CTA combined with original imagery, video, pointer-responsive interaction, or a justified 3D scene.
- Choreograph a GSAP intro - but navigation, the primary message, and the CTA must be readable and usable **before** it finishes.
- Pointer effects are additive: support touch, keyboard, coarse pointers, window blur, and visibility changes without leaving the UI half-animated.
- The static first frame must be complete when JavaScript, media, WebGL, or motion are unavailable.

## 4. Motion system

- **GSAP** is the primary animation system.
- Evaluate Lenis and Locomotive Scroll and pick **exactly one** smooth-scroll engine - never install or initialize both. Wire it correctly to ScrollTrigger, refresh measurements after fonts and media load, and destroy it on cleanup.
- Under `prefers-reduced-motion: reduce`, **bypass** smooth scrolling and scrubbed timelines entirely and render final states - don't merely shorten them.
- Choreograph section by section: major headings reveal word by word with a restrained stagger, then supporting copy and media follow.
- Split text accessibly: keep an unsplit accessible name, hide decorative split words from assistive tech, never split links or meaningful inline markup, and keep the text visible without JavaScript.
- Use CSS for simple hover, focus, and tap states. Reserve ScrollTrigger for justified pinned or scrubbed sequences. Never let two systems animate the same property.

## 5. Three.js only with purpose

- Use Three.js/custom shaders when spatial depth, texture transitions, displacement, or pointer response genuinely serve the direction - never as ornamental background noise.
- The canvas has one clear job and stays subordinate to semantic content and controls.
- Cap device pixel ratio, pause rendering offscreen and when the tab is hidden, throttle pointer input, avoid per-frame allocations.
- Provide a static poster and replace the canvas entirely under reduced motion or WebGL failure.
- Dispose of animation frames, observers, listeners, render targets, textures, geometries, materials, and the renderer; handle context loss without breaking the page.

## 6. Quality bar

- A complete semantic site, not a hero concept: responsive navigation, a coherent section progression, concrete conversion content, a final CTA, a footer, robust form/control states, visible keyboard focus.
- A distinct art-directed idea, a memorable first viewport, disciplined type and spacing, intentional crops, authored transitions, and refined hover, focus, active, loading, disabled, error, touch, and reduced-motion states.
- Performance: responsive media, lazy loading below the fold, bounded transforms, limited blur, capped canvas work, nothing animating offscreen continuously.
- **Reject:** generic gradient blobs, ornamental bento grids, glass on everything, stock component layouts, fake testimonials, invented partnerships, logo-wall theater, motion without narrative purpose.
- Never describe the result as award-winning or Awwwards-recognized without verifiable evidence.

## 7. Validate before handoff

- Run the production build and fix every failure.
- Check desktop and mobile sizes when browser validation is requested or needed to resolve a blocker.
- Verify keyboard navigation, visible focus, touch behavior, content without JavaScript, static media fallbacks, and reduced-motion behavior.
- Confirm only one smooth-scroll engine is installed and initialized, ScrollTrigger integration is correct, and all animation and WebGL resources clean up.
- Search source and rendered output for placeholders, copied reference identity, unsupported claims, misleading logos, uncredited media, and inaccessible split text.
- Report: the style system used, asset sources, motion stack, Three.js decision, validation performed, and remaining limitations.
