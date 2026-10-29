---
name: cozy-founder-offer
description: Build an offer that is easy to say yes to. List every obstacle the buyer faces, turn each into part of the offer, keep what is valuable and cheap to deliver, add honest bonuses, an affordable guarantee, true urgency and a clear name, score it on perceived value and re-test it on the same simulated buyer panel. Use when asked to improve an offer, why people won't buy, what to include, bonuses or a guarantee, or after the panel shows people passing.
---

# cozy-founder-offer

Most businesses sell a product. Good ones sell an offer: the product plus
everything that makes buying it an easy yes. The method is the Offers lens in
`lenses.md` of the `cozy-founder-board` skill folder; present it as a published
framework applied by you, never as anyone's words.

## Step 1: read what is known

- `founder/idea.md` and `founder/pitch.md`: what is sold today.
- `founder/panel/results.md`: why buyers pass, in their words. Every top objection
  should be answered by something in the offer.
- `founder/numbers.json`: what each extra costs, so the stack stays profitable.
- `founder/board.md`: the board's conditions.

## Step 2: the obstacle list

Every obstacle between the buyer and the result they want, in the buyer's words:
before buying (doubt, price, effort to switch), during (waiting, learning,
inconvenience), after (does it last, what if it fails). Aim for 15 to 30. Start
from panel objections and competitor complaints.

## Step 3: solve, trim, stack

Turn each obstacle into a solution (a feature, a service, a guarantee, a format).
Score each for value to the buyer (1 to 5) and cost to deliver (1 to 5, from the
CFO numbers). Keep high value, low cost. Stack what is left:

- **The core**: the thing itself, described by its outcome, not its ingredients.
- **Bonuses**: two or three, each removing one specific objection.
- **The guarantee**: what happens if it does not deliver. Cost it at a realistic
  claim rate with the CFO calculation before promising it.
- **Urgency or scarcity**: only if true (a launch week, a genuinely limited first
  batch). Never a fake countdown or "only 3 left".
- **The name**: a clear, specific name for the offer, not the company.

## Step 4: score it

Before and after, 1 to 10 each: size of the result, belief it will happen, time to
the result, effort and sacrifice asked. Say which part of the stack moves which
score.

## Step 5: re-test it

Save the old pitch as `founder/pitch-v1.md` and the new one as `founder/pitch.md`
(sanitised as in `cozy-founder-consumer` step 2). Run `cozy-founder-consumer` on
the **same customer file, panel size and stride k**, so the same buyers see the
new offer. Report the buy rate before and after and which objections dropped. If
nothing moved, say so: the problem may be the market or the price, not the offer.

## Rules

- Every promise must be deliverable and affordable; check costs with the CFO.
- No fake reviews, testimonials, scarcity, discounts or "as seen on".
- Follow the user's market's advertising and consumer-protection rules for
  guarantees and claims, health claims especially. Not legal advice.

## Output

`founder/offer.md` (obstacle list, the stack and its costs, the scores, the
re-test result) and the updated `founder/pitch.md`. Next: `cozy-founder-cfo` to
re-run the numbers with the stack, then `cozy-founder-marketing`.
