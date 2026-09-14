---
name: better-interface
description: Run one consolidated, evidence-based interface review across accessibility, layout, writing, typography, color, and UI polish by routing to each better-* skill and merging their findings into a single ranked table with a Block/Approve verdict. Use when asked to review, audit, or critique a screen, flow, feature, or whole repository's interface quality. For reviewing a branch, pull request, or uncommitted change, direct the developer to run interface-review.
---

# Better Interface

A cross-discipline review. This skill **routes** the interface to each domain skill, collects their evidence, and consolidates one ranked verdict.

Orchestration is all it owns. Accessibility rules belong to **better-accessibility**, structure to **better-layout**, copy to **better-writing**, type to **better-typography**, color to **better-colors**, polish and motion to **better-ui**. Never duplicate or override their rules here.

Change-scoped review (uncommitted work, branches, pull requests) belongs to **interface-review**, which resolves the scope and classifies findings before handing back.

## Evidence, not taste

Press hard on escalation triggers; leave deliberate project choices alone - both pull the same way. A trigger is a failure whatever the style guide says; a density, radius, or voice you merely dislike is not a finding. The bar for reporting is evidence. The bar for **Approve** is that you actually inspected what you claim. A short report from a real inspection beats a long padded one.

## Principles

### 1. Resolve the scope

Infer the screen, flow, feature, or repository from the request and workspace, and state it. Cover all of it in every domain, including empty, loading, error, and narrow-width states where they exist. **At most 15 findings.**

If the scope is too big to inspect credibly, narrow to one complete flow - the one the request centers on, or else the entry path every user passes through. State the boundary and what it excluded. Never imply uninspected surfaces were reviewed.

### 2. Changes go to interface-review

A request naming a branch, PR, commit range, or uncommitted changes is a change review. Say so and ask the developer to run **interface-review** (it's developer-invoked only). Don't resolve change scopes here.

When interface-review hands back, it supplies the scope, a status per finding, and the change-scoped format. Severity, ranking, the cap, and the verdict still come from here - and cover `Introduced` and `Regression` findings only.

### 3. Recon before judgment

Identify framework, styling system, component library, tokens, supported viewports, and any preview or test command. Write every fix in the project's idiom - no finding should amount to "adopt a different stack".

Read what the project says about its own interface: CONTRIBUTING, coding standards, AGENTS.md, CLAUDE.md, design-system docs, Storybook docs, UI ADRs. Name what you found (or that there was none). Documents decide **where** a finding is reported, not whether it's dropped - "it's in the style guide" doesn't retire a finding. When a guideline or shared token is the cause, report it once against that source, listing the affected components.

### 4. Domain skills are the source of truth

Confirm each owning skill is available, load it, and complete each domain before consolidating. Review in this order so foundations aren't hidden by polish:

1. better-accessibility
2. better-layout
3. better-writing
4. better-typography
5. better-colors
6. better-ui

Take each domain's principles, references, and verification checks; replace its standalone severity, format, and verdict with the ones here. If an owner is unavailable, mark that domain **Not reviewed**, name the skill, and continue - don't reconstruct its rules from memory or claim holistic coverage. When two skills seem to cover one issue, assign it to the owner of the underlying rule and mention side effects in **Why**. Report it once.

### 5. Require evidence

Every finding cites `path/to/file:line` and shows the current implementation. Don't report a code finding from appearance alone, or a visual finding from source alone when runtime behavior decides it.

### 6. Rank by user impact

- **HIGH** - blocks a task, misleads, hides content or controls, risks data loss, or is a repeated systemic failure.
- **MEDIUM** - meaningfully harms comprehension, efficiency, adaptability, or consistency.
- **LOW** - isolated polish with little task impact.

Within a severity, rank by reach and by how much one fix buys - a token or shared-component fix outranks the same symptom in one leaf.

**Escalation triggers** - once the owning skill confirms one, it's HIGH on sight, however minor the surface:

- Interactive control with no accessible name.
- Keyboard-reachable control with no visible focus indicator.
- Control or path reachable by pointer but not keyboard.
- Motion or autoplay ignoring `prefers-reduced-motion`.
- Content or control clipped, overlapped, or unreachable at 320px width or 200% zoom.
- Body or control text whose rendered contrast fails its required ratio.
- State or meaning carried by color alone.
- Destructive action without confirmation, undo, or distinct treatment.
- Truncated content with no way to reach the full value.
- Content reachable only past a scroll edge or behind a disclosure with no visible cue.
- An error naming no way to recover.
- A semantic color used against its meaning (danger hue on a non-destructive action).
- A state change carried by motion alone, leaving no color, icon, or label when animation doesn't run.

Triggers rank above everything. If more fire than the cap allows, list them first and say how many were cut - a cap may shorten a report, never hide a blocker. Triggers set severity, not rules: the owning skill decides whether the symptom exists. In a change review, a confirmed `Regression` against a trigger is HIGH even where the pre-existing equivalent would be MEDIUM.

### 7. Propose the cheapest fix

When several fixes work, take the earliest that does:

1. **Delete** - a separator space already carries, animation on a high-frequency action, ARIA a native element makes redundant, a ramp nothing uses.
2. **Use the platform** - native element, native control, the browser's focus ring.
3. **Reuse the project** - an existing token, spacing step, motion curve.
4. **Correct the value** - the exact easing, radius, gap, or contrast pair the owning skill specifies.
5. **Add** - a new token, wrapper, media query, or ARIA the platform can't supply.

A step-5 fix where step 1 was available is itself a finding - report the deletion.

### 8. Consolidate systemic findings

One root cause, one row, listing every confirmed location. Never pad toward the cap; few or no findings is a valid result.

### 9. Verify what you can

Run the safe, relevant checks the project provides. Inspect the rendered interface when runtime behavior or visual judgment matters, and record the exact command or interaction and its result. A check you couldn't run is **Not verified** - never a finding.

### 10. Read-only by default

Reviews don't edit source unless the developer also asks for fixes. If they do, use the report as the change scope and rerun verification afterward.

## Before you finish

| Mistake | Fix |
| --- | --- |
| Six disconnected domain reports | One ranked findings table |
| Visual claim inferred from source only | Inspect the rendered state, or mark Not verified |
| Silent coverage gaps | Show which domains and states were inspected |
| Missing owner treated as covered | Mark the domain Not reviewed and name the skill |
| Every legacy issue in a touched file reported | At most three pre-existing findings, in their own section |
| Pre-existing issue blocking a change review | Keep pre-existing out of the cap and the verdict |
| Domain marked Clear when the change never touched it | "Not reviewed: no evidence in the change scope" |

## Output

Use [review-format.md](review-format.md): scope and coverage, findings table, verification, verdict. A review isn't finished until it's reported in that format.
