---
description: Score a claim's correctness and completeness against one source, and nothing else
---

Use the **validating-claims** skill from the cozypowers plugin.

Take the source and claim I give (usually `<source> -- <claim>`, where the source is a file path, a URL, or pasted text). If either is missing or ambiguous, ask me - don't choose a source yourself. Then dispatch the isolated judge exactly as the skill describes, with only the procedure, the claim, and the source - no hints or context of your own - and relay its report unchanged: verdict, correctness and completeness scores, the statement table with verbatim quotes, omissions, and arithmetic. Any view of your own goes in a separate, clearly labelled section.
