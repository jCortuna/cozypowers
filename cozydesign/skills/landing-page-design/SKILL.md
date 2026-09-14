---
name: landing-page-design
description: A complete system for high-converting landing pages - intake, page structure, layout choice, conversion copywriting, SEO/AEO - plus a strict visual system (type scale, spacing tokens, nested radius, backgrounds, hero rules, icons, fluid motion, content realism, states, ship requirements, and a mandatory tagline-reveal section). Use whenever building, editing, styling, reviewing, or writing copy for a landing page, marketing site, or marketing section, including choosing sections, headlines, CTAs, fonts, sizes, spacing, radii, backgrounds, icons, or transitions for one.
---

# Landing Page Design

A landing page is not a homepage. A homepage serves many intents; a landing page wins exactly one:

**one offer → one audience → one primary action.**

**Part A** decides what the page says and how it's structured. **Part B** is the visual system. Finish A before touching B.

**Precedence.** Rules here beat framework defaults. The developer's explicit instructions beat rules here. If the developer has chosen a brand spec or a named style recipe (see the web-design-engineer skill), that governs Part B's font, color, and hero-treatment choices; Part A, the spacing/type-scale discipline, content realism, states, and ship requirements still apply.

---

# Part A - Strategy and structure

## A1. Intake

Collect what's missing **in one batch** (not one question at a time):

- **Purpose:** the ONE primary action (trial, demo, purchase, waitlist, download); exactly what the offer gives them; what counts as a conversion.
- **Audience:** the ideal customer; the problem they're solving; their top three objections (why they don't convert today); traffic source (ads, search, social, email); what they already know on arrival.
- **Proof and assets:** logos, testimonials, numbers, case studies; screenshots, demo video, GIFs; guarantees, refund and cancellation terms.
- **Constraints:** voice (casual/professional); direction (minimal editorial, playful 3D, glass UI...); mobile priority.

If an answer isn't available, assume something reasonable, state it in one line, and keep going. Don't stall.

## A2. Page structure

**Above the fold (required)**
1. Headline - the outcome plus the audience
2. Subheadline - how, with specifics
3. Primary CTA - verb + what they get
4. One proof signal - logo strip, stat, or short testimonial
5. Hero visual - product screenshot or video, or strong illustration

**Middle (the argument)**
6. Problem → solution
7. Three to five outcome-driven benefits
8. How it works in three steps
9. Social proof - testimonials or a case study

**Bottom (objections)**
10. FAQ - six to twelve questions
11. Risk reversal - trial, cancel anytime, guarantee
12. Final CTA - identical to the top one

The **tagline reveal** (B11) goes in the middle argument, typically after the hero or after benefits.

## A3. Choose a layout (and say why)

| Type | Use when |
| --- | --- |
| **A. Classic hero + sections** | The product is understandable from a hero screenshot. Most common. |
| **B. Long-form story** | Visitors need educating and skepticism overcome. |
| **C. Minimal conversion** | High-intent traffic (e.g. email to known users) or a small offer (download, waitlist). |
| **D. Comparison** | Search intent is about alternatives ("X vs Y", "best for"); usually SEO-led. |

## A4. Conversion rules

- **Match the message to the source.** Ad traffic sees the ad's headline, promise, and visual tone in the hero.
- **One obvious next step.** One primary CTA; nothing competing above the fold.
- **Benefits first.** Features say what it does; benefits say what that means for them.
- **Be specific.** Not "save time and streamline" but "cut weekly reporting from 4 hours to 15 minutes".
- **Reduce risk** with at least one of: free trial, free plan, no card required, cancel anytime, money-back guarantee.
- **Objections are a section, not a footnote.** Move the FAQ up for high-friction offers. Put proof right beside the claim it supports.

## A5. Copy

- **Headline formulas:** "{Outcome} without {pain}" · "The {category} for {audience}" · "Ship {result} in {time}".
- **Subheadline:** one or two sentences - what it is, who it's for.
- **CTA:** verb + what they get ("Start free trial", "Book a demo", "Get the checklist"). Never "Learn more" or "Submit".
- **Benefit bullets:** bold benefit, then proof or detail - e.g. **Faster iteration**: three layout variants in one click.
- B1's copy rules (no hyphens in copy, no orphans) apply here too.

## A6. Build order

Hero → benefits → how it works → proof → FAQ → final CTA. Build section by section; never regenerate the whole page per iteration - it keeps control and keeps diffs reviewable.

## A7. SEO and answer engines

- **Noindex** ad-only campaign pages and time-bound offers.
- **Index** evergreen offers where search intent matches the promise: clear title and meta description, internal links from home and feature pages, FAQ in plain question-and-answer form (with FAQ schema where appropriate).

## A8. Pitfalls

Too many CTAs above the fold · vague value props ("streamline", "optimize") · feature lists with no outcomes · proof buried at the bottom · mobile layouts that hurt readability · no clear next step.

---

# Part B - Visual system

Every visual value resolves through these rules - nothing ad hoc.

## B1. Typography

- **Fonts:** Geist, Manrope, or Poppins (Geist Mono only where monospace is functionally needed - code, data, numeric UI). **Not** Inter, Roboto, Arial, Open Sans, or Helvetica.
- **One typeface per site** unless asked to pair.
- **No italics** anywhere in the interface. **No ultra-bold** (900/black) - cap at semibold/bold.
- **No hyphens inside copy** - headings, body, labels. Rewrite the phrase.
- **No orphans** - a single word never sits alone on the last line: `text-wrap: balance` on headings, `text-wrap: pretty` on body.

**Type scale - Tailwind's default steps only.** No arbitrary sizes (`text-[19px]`, `22px`, `1.4rem`). Snap off-scale sizes to the **nearest step below**, taking that step's line height too.

| Class | Size | Line height |
| --- | --- | --- |
| `text-xs` | 12px | 16px |
| `text-sm` | 14px | 20px |
| `text-base` | 16px | 24px |
| `text-lg` | 18px | 28px |
| `text-xl` | 20px | 28px |
| `text-2xl` | 24px | 32px |
| `text-3xl` | 30px | 36px |
| `text-4xl` | 36px | 40px |
| `text-5xl` | 48px | 1 |
| `text-6xl` | 60px | 1 |
| `text-7xl` | 72px | 1 |
| `text-8xl` | 96px | 1 |
| `text-9xl` | 128px | 1 |

Adjust tracking or line height only *within* what the matched step provides, so scale-snapping and custom line heights never fight.

**Buttons:** main buttons `text-base` semibold; smaller header buttons `text-sm` semibold.

## B2. Spacing - these values only

`0 · 2 · 4 · 8 · 12 · 16 · 24 · 32 · 40 · 48 · 64 · 80 · 96` (px). Nothing between, nothing beyond.

Main buttons: 8px vertical, 12px horizontal padding.

## B3. Corner radius

Tailwind radius values only. **Nested radius:** when a shape sits inside another with a gap under 32px, `inner = outer − gap` - applied only if the result is greater than 2 (otherwise leave the inner shape square/unchanged). Example: `rounded-2xl` (16px) card with 8px padding → inner element 8px (`rounded-lg`).

## B4. Borders and backgrounds

- Never a border on only one side of a card - all four sides or none.
- **Backgrounds are flat** - no background gradients.
- **Dark-mode backgrounds only:** `#000000` · `#181818` · `#1F1F1F` · `#272727` · `#313131` · `#131209`.

## B5. Hero

- **Heading color** - the one permitted gradient, on text only: dark theme `#FFFFFF` → `#9B9B9B` left to right; light theme `#000000` → `#666666`.
- Heading and subheading **max-width 680px**.
- Insert line breaks where the thought breaks - never mid-phrase.

## B6. Icons

Phosphor, Solar, or Iconamoon. Not Material Icons/Symbols.

## B7. Motion - fluid, physical

No default transitions. Motion should suggest mass and spring through custom curves, e.g. `duration-700 ease-[cubic-bezier(0.32,0.72,0,1)]`.

**Fluid island nav**
- Closed: a floating glass pill detached from the top - `mt-6 mx-auto w-max rounded-full`.
- Hamburger: the lines rotate and translate into an X (`rotate-45` / `-rotate-45`, absolutely positioned) - they never just vanish.
- Open: a screen-filling heavy-glass overlay - `backdrop-blur-3xl` with `bg-black/80` or `bg-white/80`.
- Links: masked stagger - `translate-y-12 opacity-0` → `translate-y-0 opacity-100`, delayed per item (100, 150, 200ms...).

**Scroll reveals** - nothing appears statically on load. Entering the viewport: `translate-y-16 blur-md opacity-0` → `translate-y-0 blur-0 opacity-100` over 800ms+. Use IntersectionObserver or Motion's `whileInView`. **Never** a raw `window.addEventListener('scroll')` - it causes continuous reflow and wrecks mobile performance.

Always provide a `prefers-reduced-motion` path that shows final states.

## B8. Content realism

Generated-page tells to eliminate:

- No Lorem Ipsum - write real draft copy.
- No "John Doe" - diverse, realistic names.
- No placeholder brands ("Acme Corp", "Nexus", "SmartFlow") - believable contextual names.
- No suspiciously round numbers (`99.99%`, `50%`, `$100.00`) - organic ones (`47.2%`, `$99.00`).
- No AI clichés: "elevate", "seamless", "unleash", "next-gen", "game changer", "delve", "tapestry", "in the world of".
- Sentence case headings, not Title Case.
- Active voice ("We couldn't save your changes").
- No exclamation marks in success messages, no "Oops!" in errors - be direct ("Connection failed. Try again.").
- Unique avatars per person; varied post dates.
- Never present invented testimonials, metrics, or logos as real proof - use clearly marked placeholders until the developer supplies the real thing.

## B9. States

Every interactive element ships with:

- **Hover** - background shift, slight scale, or translate
- **Active** - `scale(0.98)` or `translateY(1px)`
- **Focus** - a visible focus ring (required)
- **Loading** - skeletons shaped like the real layout, not spinners
- **Empty** - a composed getting-started view, never a blank panel
- **Error** - inline and specific, never `alert()`

No dead links: a `#` button is either wired up or visibly disabled. Navigation marks the current page.

## B10. Ship requirements

Privacy and terms links in the footer · a custom branded 404 · client-side validation for email format and required fields · skip-to-content link · cookie consent where required · branded favicon · `<title>`, meta description, `og:image`, social tags · alt text on meaningful images · semantic `nav/main/article/aside/section` · a way back from every page.

## B11. Tagline reveal section (mandatory)

One large-type section stating the core benefit, separate from the hero and further down the page as its own moment.

- **Copy:** at least two lines; a real benefit statement in the A5 voice, not a generic section heading.
- **Type:** `text-4xl` to `text-6xl` depending on line count; max width like the hero; meaningful line breaks.
- **Animation:** words start muted (roughly 25-35% of the base text color's opacity) and, as the section scrolls into view, each word individually transitions to full color in reading order as it crosses a trigger line - never the whole block at once, never a linear fade (use the B7 curve). Implement with per-word IntersectionObserver or a single `requestAnimationFrame`-throttled scroll handler. Reduced motion: show full color immediately.

---

# Output format (new pages)

Before writing code, return in order:

1. **Page outline** - sections and order
2. **Hero copy** - headline, subheadline, CTA, proof line
3. **Benefits** - three to five, outcome-driven
4. **How it works** - three steps
5. **FAQ** - six to twelve Q&As
6. **SEO / AEO** - index or noindex; title and meta if indexed
7. **Layout** - A, B, C, or D, and why

Then build section by section (A6).

---

# Checklist

**Strategy**
- [ ] One offer, one audience, one primary action
- [ ] No competing CTAs above the fold
- [ ] Specific numbers, not vague verbs
- [ ] At least one risk reversal
- [ ] Proof beside the claim it supports
- [ ] Layout type chosen deliberately

**Visual**
- [ ] One approved typeface, no italics, no ultra-bold
- [ ] No hyphens in copy, no orphans
- [ ] Every size on the type scale; every spacing value from the token list
- [ ] Nested radii follow the formula
- [ ] No one-sided card borders, no background gradients
- [ ] Hero heading/subheading capped at 680px with meaningful breaks
- [ ] Icons from Phosphor, Solar, or Iconamoon
- [ ] Custom curves on every transition; scroll reveals via IntersectionObserver; reduced-motion path
- [ ] Tagline reveal present, 2+ lines, words activating one at a time

**Content and ship**
- [ ] No lorem, placeholder brands, AI clichés, or round fake numbers
- [ ] Hover, active, focus, loading, empty, error states
- [ ] No dead links; current nav item marked
- [ ] 404, legal links, validation, favicon, meta tags, alt text
