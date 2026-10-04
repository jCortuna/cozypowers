---
description: Build with the least code that correctly does the job - climb the ponytail ladder first
---

Use the **ponytail** skill from the cozypowers plugin.

Take the task I describe. If it starts with `lite`, `full`, or `ultra`, use that level; otherwise use full. Read the code the change touches first, then for everything you're about to write, climb the ladder - does it need to exist, does the codebase already do it, stdlib, native platform feature, installed dependency, one line - and write new code only at the bottom. Never cut validation at trust boundaries, data-loss error handling, security, accessibility, or the tests the plan calls for. Mark deliberate shortcuts with a one-line `ponytail:` comment, and in your report name the rung you took for each piece.
