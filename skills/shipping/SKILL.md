---
name: shipping
description: Verify finished work and land it cleanly - the final gate before merge or deploy. Use this skill whenever implementation appears complete, all plan tasks are done, or the developer says "done", "ship it", "merge", "deploy", "push to staging", or asks "are we finished?". Never declare work complete without running this skill; completion claims require evidence.
---

# Shipping

"It should work" is not a shipping criterion. This skill converts *probably done* into *demonstrably done*, and then lands the work without leaving mess behind. A solo developer has no release manager; this checklist is the release manager.

## 1. Verify with evidence

Run each of these and look at the actual output - do not assume:

- **Full test suite** passes. Not just the tests near the change - all of them.
- **Lint / typecheck / build** pass with the project's real commands.
- **Manual smoke test** of the user-visible behavior, exercised the way a player would hit it. For multiplayer features, that means more than one client.
- **The interface holds up**, if the change is user-visible: run the pre-delivery
  checklist from the **designing-interfaces** skill (`references/pro-rules.md` for
  app UI, `references/quick-reference.md` §1-3 for web). Contrast, touch targets,
  focus states and safe areas are shipping criteria, not polish.
- **The plan is honest**: every task marked done actually happened; every "no test: <reason>" is still defensible.

Anything red stops shipping. Fix it (via **systematic-debugging** if the cause isn't obvious) or explicitly descope it with the developer - never quietly ship around it.

## 2. Review the whole diff

Read the complete branch diff (`git diff main...HEAD`) top to bottom, as a skeptical outside reviewer:

- Leftovers: debug logging, commented-out code, TODOs that should be tasks, stray files.
- Scope creep: changes that no task in the plan asked for.
- Secrets and keys: nothing sensitive committed, ever.
- Naming check: no internal-only terms, legacy names, or placeholder copy in anything player-visible.

## 3. Land it

Present the developer with the options and a recommendation - do not choose unilaterally:

1. **Merge/push to the integration branch** (e.g. `staging`) - the default for finished work.
2. **Open a PR** instead - when the developer wants a written record or a second look before merge.
3. **Park the branch** - work is sound but shouldn't land yet; leave a `docs/plans/` note saying exactly how to resume.
4. **Discard** - the experiment failed; delete the branch and record the lesson in the design doc.

If the project has automation that triggers on push (CI, changelog/release-notes drafting, deploy previews), name what will fire before pushing, and after pushing, check that it succeeded - a red pipeline discovered three days later costs ten times what it costs now. Where a bot drafts release notes or changelogs as a PR, review that draft for accuracy and player-facing naming before it publishes.

## 4. Clean up

- Delete merged local and remote branches; remove worktrees if used.
- Update the plan document status to shipped, with the merge commit or PR link.
- Close the loop in one sentence to the developer: what shipped, what was descoped, what follow-ups were noted.
