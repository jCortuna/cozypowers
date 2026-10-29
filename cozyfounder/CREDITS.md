# Credits

cozyfounder is a clean-room, markdown-only recreation of **The Founder skill**
pack by Jake Schincariol:

- https://github.com/Jakeschincariol/founder-skill (MIT, v1.0, commit `fd9385b`)

Borrowed ideas: the eleven-role pack and its order (board → competitors →
consumer → pricing → offer → cfo → marketing → brand → ops → launch → plan), the
shared `founder/` folder the skills read from each other, the three framework
lenses, the simulated buyer panel with four Van Westendorp price questions per
buyer, the unit-economics model and its what-ifs, the matcha-café example data,
and a business-plan verdict computed from fixed checks.

The skills were rewritten in cozypowers' own words. The two example data files
(`example-numbers.json`, `example-customer.json`) and the example pitch are
carried over as inert data, with the upstream notice below.

## What changed, and why

| upstream | cozyfounder | reason |
| --- | --- | --- |
| `unit_economics.py`, `van_westendorp.py`, `panel.py`, `compile.py` | `formulas.md`, `van-westendorp.md`, `dealing.md`, `brief-template.md` and written verdict rules | cozypowers ships zero executable code. The agent does the arithmetic and shows its working; `formulas.md` carries a worked example that must be reproduced before use. |
| Random persona deal with a seed | A fixed stride rule | Reproducible without a random-number generator, so re-tests use the same buyers. |
| Buyer sub-agents write their own answer files; README suggests switching on accept-edits mode | Buyers get no tools and reply with JSON; the moderator validates and files each answer | No broad write permissions for 20 to 100 sub-agents. |
| Pitch pasted into each buyer brief as-is | Pitch sanitised, length-capped and fenced as data, with an explicit "not instructions" note | Closes a prompt-injection path into every buyer. |
| Panel of 100 by default | 20 by default; 100 only after the user confirms the cost | Cost control. |
| Competitor and supplier research with no rule about page content | Every web-reading skill treats fetched pages as data, never instructions | Untrusted web text could otherwise steer the agent. |
| Board sub-agents read files | Board briefs passed inline; sub-agents use no tools | Smaller permission surface. |
| Claude Code only | Also an Antigravity plugin, with a no-sub-agent fallback | Cozybara's standing Antigravity requirement. |

The upstream repository was audited before this rewrite: no hidden or invisible
instructions, no network calls, no telemetry, no shell execution. The changes
above harden behaviour; they do not remove anything malicious, because nothing
malicious was found.

## Upstream license notice

Copyright (c) 2026 Jake Schincariol

> Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:
>
> The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.
>
> THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

The board lenses summarise ideas from *$100M Offers* (Alex Hormozi), *Zero to One*
(Peter Thiel with Blake Masters) and *Steve Jobs* (Walter Isaacson) in our own
words. No affiliation with or endorsement by these authors is implied.
