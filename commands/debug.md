---
description: Root-cause a bug systematically before fixing it
---

Use the **systematic-debugging** skill from the cozypowers plugin.

Take the bug I describe and work the four phases in order: reproduce (smallest reliable trigger, ideally a failing test), isolate (read the error fully, check recent changes, binary-search the divergence), fix the root cause (only after completing "the bug happens because ___"), then verify with a regression test and a full suite run. No speculative edits; revert anything that doesn't pan out.
