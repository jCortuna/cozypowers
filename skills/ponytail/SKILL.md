---
name: ponytail
description: Write the least code that correctly does the job - before adding any function, file, class, dependency, abstraction, or config, climb a seven-rung ladder (does it need to exist, does the codebase already do it, stdlib, native platform feature, installed dependency, one line, then the minimum) and stop at the first rung that holds. Use this skill whenever you are about to write or change code, implement a plan task, add a feature, helper, wrapper, or dependency, or when the developer says "ponytail", "keep it minimal", "YAGNI", "less code", "don't over-engineer", or "simplest thing". Applies even when not invoked by name - every implementation step is a ponytail step.
---

# Ponytail

Think like the laziest senior developer in the room: the one who has maintained enough code to know that every line written is a line someone has to read, test, and fix later - and for a solo developer, that someone is always you. The best code is the code you never wrote. The second best is the code someone else already wrote and tested.

**brainstorming** applies YAGNI to the *design*. This skill applies it to the *keyboard*, at the moment code is about to be written.

## 1. Read before you write

Before climbing, read the code the change touches and its immediate neighbours: the module, its imports, the helpers next door, the project's dependency manifest. Most over-building happens because the agent didn't look - it writes a `formatDate` helper three files away from the one that already exists.

## 2. Climb the ladder

For each piece of code you are about to add, ask in order, and **stop at the first rung that holds**:

1. **Does it need to exist?** Is someone actually asking for this now? Configurability nobody requested, "future-proof" layers, unused options, speculative error types - skip them.
2. **Does the codebase already do it?** Reuse the existing helper, component, type, or pattern - even if you'd have written it slightly differently.
3. **Does the standard library do it?** Language built-ins before anything hand-rolled: `Array.prototype.toSorted`, `structuredClone`, `itertools`, `pathlib`, `Intl.DateTimeFormat`.
4. **Does the platform do it natively?** The browser, OS, framework, or database feature: `<dialog>`, CSS `:has()`, `<input type="date">`, a SQL constraint instead of app-side checks, the framework's router instead of a custom one.
5. **Does an installed dependency do it?** Check the manifest before writing a utility. Do **not** add a new dependency to avoid writing ten lines - a new dependency is more code, not less.
6. **Can it be one line?** A clear one-liner beats a five-line function called once. Clarity wins over cleverness - a one-liner nobody can read is not a saving.
7. **Write the minimum that works.** No abstraction until the second real use. No interface with one implementation. No config for a value that has never changed.

When a rung above "write it" is taken, say which one in a few words in your report ("used the existing `slugify` in `utils/text.ts`"). That makes the choice visible and reviewable.

## 3. Never cut these

Minimal means minimal *correct* code. These are part of the minimum, never trimmed to save lines:

- **Input validation at trust boundaries** - anything from users, the network, files, or other services.
- **Error handling that prevents data loss or corruption** - saves, migrations, payments, game state.
- **Security measures** - auth checks, escaping, parameterised queries, secret handling.
- **Accessibility basics** - labels, keyboard access, focus, contrast, alt text.
- **Tests the plan calls for** - **test-driven-development** still applies; ponytail shrinks the code under test, not the tests.

If the ladder seems to point at removing one of these, the ladder is being misread.

## 4. Mark shortcuts honestly

When you take a deliberate shortcut - a hard-coded value, a known edge case left for later, a naive algorithm that's fine at today's sizes - mark it where it lives:

```js
// ponytail: O(n²) scan; fine below ~500 players, revisit if lobbies grow
```

One line: what was skipped, and the condition under which it stops being fine. An unmarked shortcut is a hidden bug; a marked one is a decision. **shipping** lists every `ponytail:` comment on the branch before landing, so "later" doesn't quietly become "never".

Do not mark things that aren't shortcuts. Simple code that fully does the job needs no apology.

## 5. Levels

Default is **full**. The developer can change it for a task or a session (`/ponytail lite ...`, or "ponytail ultra for this one"):

| Level | Behaviour |
|---|---|
| **lite** | Build what was asked as normal, but name the lazier alternative in one line when one exists, and let the developer choose. |
| **full** | Climb the ladder on everything you write. The default. |
| **ultra** | Full, plus: look for code to *delete* before adding any, and question requirements that look speculative before building them - ask, don't silently drop. |

No level overrides section 3, and none overrides an approved plan or spec: if the ladder says a planned item shouldn't exist, raise it at the next checkpoint instead of skipping it.

## Signs you've stepped off the ladder

- Writing a helper without having searched for an existing one.
- Adding a dependency, a config option, a base class, a factory, or a generic parameter for a single use.
- "In case we need it later", "for flexibility", "to make it extensible".
- A diff that is noticeably larger than the task's description implies.
- Wrapping a library call in a function that only forwards its arguments.

## Why there is no hook

The upstream idea is usually installed with a SessionStart hook that injects these rules into every session; without it, independent testing found the copied skill never switched itself on. cozypowers ships no executable code, so this skill relies instead on its own description, on **executing-plans** climbing the ladder before every implementation step, and on the CLAUDE.md snippet in the README. That is weaker than a hook. If you want it every time, use `/ponytail` or add the snippet.
