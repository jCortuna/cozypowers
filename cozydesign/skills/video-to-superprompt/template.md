# Superprompt template

Paste-ready structure. Remove sections that don't apply; keep per-section motion detail.

```text
Build [the exact thing] based on the supplied reference video. Treat the video as [exact recreation / visual and motion inspiration only]. It should feel [tone], using [domain-specific visual language].

ASSET MAP
- Reference video: [path or URL]
- Background images: [URLs or PLACEHOLDER names]
- Scroll-scrubbed videos: [URLs or PLACEHOLDER names]
- Posters / sprites / textures / WebGL assets: [URLs or PLACEHOLDER names]

BRAND AND CONTENT
- Name:
- Core headline:
- Supporting copy:
- Navigation:
- CTA:
- Footer:

GLOBAL DESIGN SYSTEM
- Visual style:
- Typography (families, weights, sizes, tracking):
- Colors (hex by role):
- Layout grid and spacing:
- Image and video treatment:
- Texture / surface / shadow rules:
- Explicit anti-patterns:

MOTION SYSTEM
- Overall feel:
- Easing curves and durations:
- Reveal rules:
- Scroll rules:
- Hover / tap / focus states:
- Ambient loops:
- Reduced-motion behavior:

SECTION 1: [name]
- Purpose:
- Layout:
- Visual details:
- Animation:
- Interaction:
- Scroll behavior:
- Implementation notes:
- Reduced-motion fallback:

SECTION 2: [name]
- (same fields)

[Repeat for every visible beat, in video order.]

VIDEO AND SCROLL IMPLEMENTATION
- Scroll-scrubbed video: pin a sticky section and map scroll progress to video.currentTime.
- Videos: muted, playsinline, appropriate preload, object-fit cover, no controls unless playback is user-facing.
- Precise pinned timelines: GSAP ScrollTrigger or a requestAnimationFrame loop.

WEBGL / THREE.JS
- Only for real particles, 3D, shaders, or canvas scenes.
- Cap pixel ratio, reduce density on mobile, pause when hidden or offscreen, provide a static fallback.

RESPONSIVE
- Desktop:
- Tablet:
- Mobile:
- Safe areas and text-overlap constraints:

ACCESSIBILITY AND PERFORMANCE
- prefers-reduced-motion:
- Keyboard and focus:
- Lazy loading / preloading:
- Video and poster fallbacks:
- Performance caps:

SUCCESS CHECK
- First viewport must show:
- During scroll:
- At the final section:
- The build fails if:
```
