---
name: shaping-specs
description: Turn a feature idea into a structured spec before planning or implementation begins. Use this whenever the user proposes a new feature, describes something they want built, or asks to "spec out," "shape," or "scope" an idea — this runs before writing-plans or executing-plans, not after. Automatically reads any project-level standards/ and product/ directories and folds relevant conventions and mission context into the spec, so planning never starts from a blank page. Produces a dated spec folder the user reviews and approves before anything gets planned or built.
---

# Shaping specs

Turns a raw feature idea into a written spec the user approves before any planning or code gets written. This runs *before* writing-plans — a shaped spec becomes writing-plans' starting point instead of a bare feature request.

## When this runs

- The user runs `/spec`, or
- The user describes a new feature and no spec exists for it yet

If a spec folder already exists for the feature under discussion, offer to revise it rather than starting fresh.

## Procedure

### 1. Gather context automatically

Before asking the user anything, check the current project root for:

- `standards/` — skim `standards/index.yml` if it exists; otherwise scan subfolder names. Read only what's plausibly relevant to this feature, not everything.
- `product/mission.md` and `product/roadmap.md` — read in full if present. These are meant to stay short.

Neither is a hard dependency. If they don't exist, proceed without them.

### 2. Ask the shaping questions

Interview the user briefly — don't ask what the conversation has already answered:

- What problem does this solve, and for whom?
- What's explicitly out of scope?
- Any constraints — technical, design, timeline?
- How will you know it's done?

### 3. Draft the spec folder

Create `specs/YYYY-MM-DD-feature-slug/` containing:

- `plan.md` — problem, goal, scope, out-of-scope, open questions
- `shape.md` — the concrete approach: what gets built, key decisions, sequencing
- `standards.md` — the specific standards pulled in step 1, so the spec stays self-contained even if `standards/` changes later
- `references.md` — links to related specs, product docs, or external references

### 4. Present for approval

Summarize the draft — don't dump the full files into chat — and get explicit confirmation before writing anything to disk. Once approved, let the user know the spec is ready to hand to `/plan`.

## Handoff

Don't auto-invoke `/plan`. State that the spec folder is ready and let the user decide when to move forward.
