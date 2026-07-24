---
name: executing-plans
description: Execute a written implementation plan task-by-task with self-review and checkpoints. Use this skill whenever a plan document exists and the developer says "go", "execute", "start building", "continue the plan", or resumes work in a new session on an existing plan. Also use it when tempted to freestyle beyond the plan - this skill is the antidote.
---

# Executing Plans

Work the plan. Not the plan you wish existed, not the improvements you thought of along the way - the plan the developer approved. Discipline here is what lets a solo developer trust hours of autonomous work.

## The loop

For each task, in order:

1. **Read the task fully** before touching anything.
2. **Test first** where the task has one: write the failing test, run it, watch it fail for the right reason (see **test-driven-development**).
3. **Implement** the minimal change the task describes.
4. **Verify**: run the task's verification commands. All green, including previously passing tests.
5. **Self-review the diff** before committing. Read it as a skeptical reviewer: Does it match the task spec? Is anything in the diff *not* required by the task? Debug prints, commented-out code, drive-by "improvements" - remove them.
6. **Commit** with the task's message. One task, one commit.
7. **Mark the task done** in the plan file (change `## Task N` to `## ✅ Task N`), so any future session can see exactly where things stand.

## Checkpoints

At each CHECKPOINT in the plan, stop and report: tasks completed, anything that deviated from plan and why, and the current state of the tests. Wait for the developer's go-ahead before continuing. Do not blow through checkpoints because things are going well - checkpoints exist precisely for when things *seem* to be going well.

## When reality disagrees with the plan

- **Small surprises** (a function has a different signature, a file moved): adapt, and note the deviation in the plan file.
- **Real surprises** (the approach doesn't work, a task reveals a design flaw, a change would ripple further than planned): **stop**. Report what was found and propose options. Never silently redesign mid-execution - that is how a 15-minute task becomes a 2-hour mystery refactor.
- **Bugs found along the way** that are unrelated to the plan: note them in the report at the next checkpoint. Do not fix them now unless they block the current task.

## Rules of engagement

- Never mark a task complete on the strength of "it should work". Evidence over claims: verification commands must actually run and actually pass.
- If a test fails and the cause isn't obvious within a couple of minutes, switch to the **systematic-debugging** skill rather than shotgun-editing.
- When the last task is done, hand off to the **shipping** skill.
