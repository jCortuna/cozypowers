---
name: brainstorming
description: Refine a rough idea into an approved design before any code is written. Use this skill BEFORE starting any creative or constructive work - new features, new components, new games or game mechanics, behavior changes, refactors with user-visible effects, or anything where the developer says "let's build", "add", "I want", "can we make", or describes an idea. If the request is a genuine one-line fix (typo, obvious bug), skip this skill; for everything else, start here.
---

# Brainstorming

Turn a rough idea into a design the developer has actually approved, before a single line of code exists. Code written before the idea is understood is code that gets rewritten - and for a solo developer, every rewrite comes straight out of evenings and weekends.

## The process

### 1. Understand before proposing

Ask questions to uncover what the developer really wants. Ask **one question at a time** - a wall of questions gets skimmed and half-answered. Prefer multiple-choice or yes/no questions when they fit; open questions when they don't.

Focus questions on:
- **Purpose**: What problem does this solve? Who hits this problem, and when?
- **Scope**: What is the smallest version that would be genuinely useful? What is explicitly out of scope?
- **Constraints**: Existing code it must play nicely with, performance limits, deadlines, platform quirks.
- **Success**: How will we know it works? What would make the developer say "yes, that's it"?

Check the current state of the codebase first if it's available - questions grounded in what actually exists are worth double.

### 2. Explore alternatives

Before settling, sketch **2-3 different approaches** with honest trade-offs. Lead with the one you'd recommend and say why. A solo developer has no architecture review board - this step is that board.

Prefer boring, simple designs. YAGNI ruthlessly: challenge any feature or flexibility that isn't needed *now*. Complexity is a loan taken against future maintenance time, and there is exactly one maintainer.

### 3. Present the design in sections

Once direction is agreed, present the design **one section at a time**, each short enough to read in under a minute: overview, then data/state changes, then behavior, then edge cases, then testing approach. After each section, pause for a yes/adjust before continuing. Never dump a full design document in one message and ask "thoughts?"

### 4. Save the design

After approval, write the design to `docs/designs/YYYY-MM-DD-<topic>.md` in the project (create the directory if needed) and commit it. Future sessions - and future Claude instances - start from this document instead of re-litigating decisions.

## Rules of engagement

- Do not write implementation code during brainstorming. Illustrative pseudocode or a type signature is fine; working code is not.
- If the developer answers a question with "I don't know", propose a sensible default and mark it as an assumption in the design doc.
- If mid-brainstorm the idea turns out to be a bad one, say so plainly and suggest what to do instead. A killed bad idea is a successful brainstorm.
- When the design is approved, hand off to the **writing-plans** skill.
