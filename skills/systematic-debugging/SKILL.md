---
name: systematic-debugging
description: Find the root cause of a bug before writing any fix. Use this skill the moment anything behaves unexpectedly - a failing test, an error message, a stack trace, "it works locally but not deployed", flaky behavior, or the developer saying "bug", "broken", "weird", or "why is this happening". Especially use it when the temptation is to try a quick change and see if it helps - that temptation is the trigger.
---

# Systematic Debugging

Guessing feels fast and is slow. Every "let me just try changing this" that doesn't work adds noise to the crime scene, and three guesses in, nobody remembers what the original symptom even was. Root cause first, fix second - always.

## Phase 1: Reproduce

Get a reliable reproduction before anything else.

- Reduce it to the smallest trigger: fewest steps, smallest input, ideally a failing test. A bug captured in a test is already half fixed - and once fixed, stays fixed.
- If it only reproduces in one environment (production, one browser, multiplayer with 3+ players), record exactly what differs. The difference list *is* the suspect list.
- If it's intermittent, look for the classic culprits first: timing/race conditions, shared state between tests, uninitialized values, network order. Never "fix" flakiness by adding sleeps - find the actual event to wait on.

## Phase 2: Isolate

Locate where reality diverges from expectation.

- **Read the error properly.** The full message, the actual line, the whole stack trace. An embarrassing fraction of debugging time is spent not reading the answer that was already on screen.
- **Check recent changes first**: `git diff`, `git log`, and if needed `git bisect`. The bug is usually in the code most recently touched, not in the framework.
- **Binary-search the path**: find a point where the data is still correct and a point where it's wrong; split the interval with logs or a debugger until the divergence sits in one function.
- **State assumptions and test them one at a time.** "The event fires before render" - does it? Verify, don't assume. Each verified assumption shrinks the search space by half.

## Phase 3: Fix the cause, not the symptom

- Before writing the fix, be able to complete the sentence: "The bug happens because ___." If the sentence can't be completed, return to Phase 2.
- Fix at the source of the wrongness, not where the wrongness became visible. A null-check at the crash site that leaves upstream code producing nulls is a symptom patch - the bug will resurface wearing a different stack trace.
- One deliberate change at a time. If a fix doesn't work, **revert it** before trying the next idea. Never accumulate speculative edits.

## Phase 4: Verify and lock the door

- Confirm the original reproduction now behaves correctly - not just that the error message went away.
- Add the regression test (per **test-driven-development**: watch it fail on the pre-fix code if feasible, then pass on the fix).
- Run the full suite: verify the fix broke nothing else.
- Spare thirty seconds for: "Can this same root cause bite anywhere else?" Fix siblings now while the context is loaded - it will never be this cheap again.

## Escalation rule

After three failed root-cause hypotheses, stop digging in the same hole. Step back and question a layer of assumptions deeper: the environment, the dependency versions, the test itself, the reproduction. Say plainly to the developer: "Here's what I've ruled out, here's what I now suspect." Honest uncertainty beats confident thrashing.
