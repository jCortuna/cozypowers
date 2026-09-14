---
name: video-to-superprompt
description: Turn a reference video (a site walkthrough, app recording, motion demo, or scroll capture) into an extremely detailed, builder-ready prompt that captures its layout, typography, color, motion, scroll behavior, assets, WebGL, and section-by-section sequence - for faithful recreation or as inspiration. Use when the developer provides, links, or points to a video and asks to analyze its design or animation, or to write a prompt, brief, or article that recreates the page, app, interaction, or motion system.
---

# Video to Superprompt

Convert a reference video into one paste-ready prompt detailed enough that someone could rebuild the experience **without ever seeing the video**. Default output is a single prompt unless the developer asks for an article, asset pack, or implementation brief.

## Workflow

### 1. Locate the source

Accept local files, uploads, URLs, browser-visible video, or media already in the repo. If the video is referenced but you can't access it, **ask for the exact file or URL** - never invent what it shows. If exact recreation is the goal and there's a live page or source code behind the video, inspect that too; code is more precise than frames.

### 2. Inspect it technically

You read a video through still frames. Get its facts and a good frame set:

- Duration, dimensions, frame rate, and size (e.g. `ffprobe`, if available).
- Representative frames (e.g. `ffmpeg` at one frame per second into a scratch folder) - but favor **timeline beats** over uniform thumbnails: start, middle, end, and every visible transition. For long or scroll-heavy captures, sample densely around transitions.
- If no frame-extraction tool is available, ask the developer for screenshots at key timestamps plus a short description of the motion between them.

Note what you can and can't observe; motion between frames is inference - label it as such.

### 3. Analyze in layers

- **Story** - purpose, emotional arc, section order, how each beat hands off to the next.
- **Layout** - viewport framing, grids, sticky zones, cards, media, overlays, margins, navigation, footer.
- **Motion** - reveal timing, easing, parallax, masks, pinning, scroll scrubbing, hover/tap states, ambient loops, camera moves.
- **Visual design** - typography, palette, surfaces, borders, shadows, texture, icons, image and video treatment.
- **Rebuild mechanics** - which primitive produces each effect: CSS or native APIs, IntersectionObserver, Web Animations API, GSAP ScrollTrigger, Lenis, Motion, Three.js/WebGL, canvas, `video.currentTime` scrubbing, carousels.
- **Accessibility and performance** - reduced motion, mobile behavior, touch and keyboard, lazy loading, video preload, pixel-ratio caps, static fallbacks.

### 4. Plan the assets

Produce an **asset map**: exact URLs when supplied, local filenames when used, clearly marked placeholder names when assets must still be made. If generated media is needed, write separate prompts for image plates, video clips, WebGL/canvas elements, posters, sprites, masks, and textures. If the developer named specific models or APIs, keep those names exactly, and keep image prompts separate from video prompts.

### 5. Write the superprompt

- One fenced `text` block, paste-ready (unless another format is requested).
- Open with **what to build** and the **reference boundary**: exact recreation or inspired adaptation.
- Cover: asset map, brand and content, global design language, layout rules, section-by-section anatomy, motion system, scroll system, video behavior, WebGL behavior, responsive rules, accessibility and performance, anti-patterns.
- For **every major section**: purpose, layout, visual details, animation, interaction, scroll behavior, implementation choice, reduced-motion fallback.
- Translate taste into instructions. Ban phrases like "make it beautiful", "similar animation", "nice transitions".

Use the structure in [template.md](template.md). Delete sections that don't apply, but never drop section-by-section motion detail.

### 6. Verify before finalizing

- Every asset path or URL in the prompt exists or is explicitly marked as a placeholder.
- Extracted frames are non-empty and actually representative.
- When producing a repo artifact (article, brief), follow the workspace's conventions and keep changes narrowly scoped.

## Output modes

- **Prompt only** - the prompt, optionally preceded by a short asset map.
- **Article** - a `content.md` with frame evidence, a manifest, and the prompts, following the repo's article conventions.
- **Implementation brief** - the prompt plus a build plan and QA checklist.
- **Asset-generation pack** - prompts split into backgrounds, video clips, sprites/WebGL, posters, and the final page prompt.

## Quality bar

- Long enough to rebuild the interaction blind.
- Preserves the video's sequence, pacing, and notable quirks.
- Names exact mechanisms: pinned section, scrubbed timeline, `video.currentTime`, parallax layer, opacity reveal, transform, mask, shader, particle field, hover state, carousel physics.
- Always specifies mobile and reduced-motion behavior.
- Calls out what to avoid - generic landing-page sections, decorative blobs, mismatched stock media, autoplay video where scroll-scrubbing is required, text overlapping media.

## Example

Observations like:

```text
0-4s   quiet editorial hero
4-10s  title splits apart while the image scales up
10-16s three cards pin and stack
16-20s the final card lifts away to uncover the footer
```

become a prompt whose outline covers: the visual system and type; section-by-section structure; the exact motion chronology; the likely primitives (sticky pinning, scroll-linked scale, stacked sticky cards); responsive and reduced-motion behavior; and an asset list with acceptance checks.
