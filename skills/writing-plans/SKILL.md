---
name: writing-plans
description: Turn an approved design into a step-by-step implementation plan with small, verifiable tasks. Use this skill whenever a design exists (from brainstorming or provided by the developer) and implementation is about to begin, or when the developer says "make a plan", "how should we build this", or "break this down". Never begin multi-file implementation work without a written plan.
---

# Writing Plans

Write the plan as if it will be executed by an enthusiastic engineer with no project context, no judgment, and a suspicious attitude toward testing. If the plan only works because the person executing it is clever, it is not a plan - it is a hope. This matters doubly for a solo developer: the "person executing it" is often a future session with none of today's context.

## Plan structure

Save plans to `docs/plans/YYYY-MM-DD-<topic>.md`. Use this template:

```markdown
# Plan: <topic>

**Design:** link to the design doc
**Branch:** <branch name>

## Task 1: <verb phrase, e.g. "Add move validation for Spelunker pawns">
- Files: exact paths to create or modify
- Test first: the specific failing test to write, with its file path
- Change: what to implement, concretely (code sketches welcome)
- Verify: the exact command(s) to run and what output means success
- Commit: suggested commit message

## Task 2: ...
```

## What makes a task right-sized

- Each task should take **2-15 minutes** and end in a passing test suite and a commit. If a task needs the word "and" twice in its title, split it.
- Every task names **exact file paths**. "Update the relevant components" is not a plan.
- Every task with logic starts with a test (see the **test-driven-development** skill). Tasks that cannot be tested (pure config, copy changes) say so explicitly and name their manual verification step instead.
- Order tasks so the code compiles and tests pass after **every** task, not just the last one. No "it'll all come together in task 9".

## Checkpoints

Insert an explicit **CHECKPOINT** line after every 3-5 tasks: a natural pause to review the diff, reconsider, or stop for the day. Solo development happens in stolen hours; a plan must be resumable at any checkpoint by someone with zero short-term memory of the work.

## Rules of engagement

- Present the plan for approval before executing it. Note anything you're unsure about rather than hiding it in confident prose.
- If during planning you discover the design has a hole, stop and return to **brainstorming** for that specific hole - do not quietly design in the plan.
- When approved, hand off to the **executing-plans** skill.
