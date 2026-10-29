---
name: cozy-founder-plan
description: "Compile the founder pack into a business plan, summary and one-pager with a verdict from fixed checks: Profitable, Not yet or Incomplete. Use to write the plan or ask if it's profitable."
---

# cozy-founder-plan

The last step. One document a founder can act on, or hand to a partner or a
lender, built only from what the pack found.

## Step 1: the verdict

The verdict is decided by these checks, using the numbers already in
`founder/cfo.md` (recalculate from `founder/numbers.json` with the
`cozy-founder-cfo` formulas if `cfo.md` is missing or older than the numbers
file) and `founder/panel/results.json`:

| # | check | passes when |
| --- | --- | --- |
| 1 | Each unit earns money | contribution per unit > 0 |
| 2 | Year 1 makes money | year 1 operating profit > 0 |
| 3 | Break-even fits | break-even per day ≤ capacity (only if a capacity was given) |
| 4 | Enough buyers buy | panel buy rate ≥ 25% (only if the panel ran) |

- No numbers at all → **Incomplete**. Offer `cozy-founder-cfo`.
- Every applicable check passes → **Profitable**.
- Any applicable check fails → **Not yet**, listing each failing check with its
  number.

If the user wants a different buy-rate bar, use it and state the bar and the
reason in the plan. Never write Profitable by judgement, and never round a
failing number into a passing one. If the panel did not run, say the verdict
rests on numbers alone.

## Step 2: the summary

Write `founder/summary.md`, half a page, plain words:

- What the business is and who it is for, in two sentences.
- The verdict and the three numbers behind it (margin, break-even, year 1).
- Where the buyer panel and the board agreed, and where they disagreed.
- The biggest risk and what will be done about it.
- What the founder needs to start (cash from the CFO, the first test from launch).
- The one thing to do this week.

If the verdict is Not yet, lead with what has to change and which skill changes
it. Never soften a failing check.

## Step 3: compile

Write `founder/business-plan.md` in this order: title (the name from the first
heading of `founder/idea.md`); **Verdict** with each check marked pass or fail and
its number; a key-numbers table (price, margin at plan, break-even, year 1
operating profit, startup spend, cash needed, payback month, panel result); then
one section per file that exists, with its own top heading removed and its other
headings demoted one level:

| section | file |
| --- | --- |
| The idea | `idea.md` |
| Summary | `summary.md` |
| Board | `board.md` |
| Competition | `competitors.md` |
| Buyer panel | `panel/results.md` |
| Pricing | `pricing.md` |
| Offer | `offer.md` |
| Numbers | `cfo.md` |
| Marketing | `marketing.md` |
| Brand | `brand.md` |
| Operations | `ops.md` |
| Launch plan | `launch.md` |

Copy sections across as they are; do not rewrite them. Then a **Not done yet**
list naming each missing section and the skill that fills it. Do not fill a
missing section from guesses. End with: the panel is simulated buyers and the
numbers are projections from the inputs; confirm demand with real customers and
costs with real quotes. Not financial, legal or tax advice.

## Step 4: the one-pager

Write `founder/one-pager.md` for someone deciding in two minutes: the problem, the
customer, the offer and price, the key-numbers table, the evidence (panel result,
competitor gap, any real test), what the money is for, and the ask. Use the same
numbers as the plan, exactly.

## Output

`founder/summary.md`, `founder/business-plan.md`, `founder/one-pager.md`. Give the
user the verdict in one line and the one thing to do this week. If they want a PDF
or a deck, offer to export it, keeping the markdown as the source of truth.
