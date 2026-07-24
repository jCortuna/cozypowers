---
name: test-driven-development
description: Enforce the RED-GREEN-REFACTOR cycle when implementing any logic - new functions, game rules, validation, state changes, bug fixes. Use this skill whenever writing or modifying code that has behavior worth being correct, whenever fixing a bug, or whenever the developer mentions tests, TDD, or "make sure this works". If code was written before its test, this skill says to delete it and start with the test.
---

# Test-Driven Development

Tests written after the code pass because they describe what the code *does*, not what it *should do*. Tests written first are the only proof the test can fail - and a test that cannot fail is decoration. For a solo developer with no QA department, the test suite **is** the QA department.

## The cycle

**RED** - Write one small failing test for the next bit of behavior.
- Run it. **Watch it fail.** Confirm it fails for the right reason (assertion failed), not the wrong one (import error, typo, wrong setup).
- If it passes immediately, the test is broken or the behavior already exists. Investigate before proceeding.

**GREEN** - Write the *minimum* code to make that test pass.
- Not the elegant general solution. The minimum. Generality gets earned by the next test that demands it.
- Run the test. Watch it pass. Run the whole suite. Watch everything pass.

**REFACTOR** - With everything green, clean up: names, duplication, structure. Run the suite again.

**COMMIT** - Small, working, tested. Then back to RED for the next behavior.

## The hard rule

If implementation code exists before its test: **delete the implementation, write the test, then rewrite the code.** Yes, really. Rewriting takes minutes; the certainty that the test genuinely exercises the behavior lasts the lifetime of the project. Do not keep the code and retrofit a test around it.

## What deserves a test (solo-dev pragmatism)

- **Always**: game rules and move validation, scoring, state machines, data transforms, anything multiplayer-synchronized, bug fixes (regression test first - watch it fail on the broken code, then fix).
- **Usually**: API handlers, non-trivial UI logic (reducers, hooks).
- **Skip honestly**: pure copy changes, static config, throwaway prototypes explicitly labeled as such. Skipping silently is not allowed; write "no test: <reason>" in the commit or plan.

## Anti-patterns to refuse

- Tests with no assertions, or assertions like `expect(result).toBeDefined()` that pass for almost any behavior.
- Mocking so much that the test exercises the mocks, not the code.
- Changing the test to match buggy output ("the test was wrong" requires evidence, not convenience).
- Writing ten tests up front, then implementing for an hour. One test, one behavior, one pass at a time.
- Marking work complete while any test is failing or skipped without a written reason.
