# Van Westendorp by hand

The price-sensitivity calculation `cozy-founder-pricing` performs. There is no
script: build the table below in `founder/pricing-curve.md` so every percentage
can be re-counted.

## Inputs

One row per respondent with four prices: too cheap (a), a bargain (b), getting
expensive (c), too expensive (d). Sources, best first:

1. A real survey CSV with columns `too_cheap, cheap, expensive, too_expensive`.
2. The panel ledger `founder/panel/ledger.md` (last four columns).

Drop a row, and count it as dropped, if any of the four is missing, not a
positive number, or out of order (a ≤ b ≤ c ≤ d must hold). You need at least 5
complete rows; with fewer, stop and say so.

## Step 1: the price grid

From the lowest "too cheap" to the highest "too expensive". Step size: $0.25 if
that span is $20 or less, $1 up to $100, otherwise one fortieth of the span
rounded to a round number. Include every grid price.

## Step 2: four percentages at each grid price p

With N = the number of complete rows:

| curve | share of rows where | direction |
| --- | --- | --- |
| TC(p) too cheap | a ≥ p | falls as p rises |
| CH(p) a bargain | b ≥ p | falls |
| EX(p) expensive | c ≤ p | rises |
| TE(p) too expensive | d ≤ p | rises |

Also write the two complements: NOT-CH(p) = 100% − CH(p) and NOT-EX(p) = 100% −
EX(p).

Tip for counting: sort each of the four columns once. Then, at each p, the count
is how many sorted values sit on the right side of p, read straight off the
sorted list.

## Step 3: the four points

Each point is where a rising curve first meets a falling one:

| point | rising curve | falling curve | meaning |
| --- | --- | --- | --- |
| PMC, marginal cheapness | NOT-CH | TC | below this, too many think it is too cheap to be good |
| PME, marginal expensiveness | TE | NOT-EX | above this, too many will not buy |
| OPP, optimal price | TE | TC | as many say too cheap as too expensive |
| IPP, indifference price | EX | CH | as many say bargain as expensive |

To find it: walk down the grid and compute gap = rising − falling at each price.
The crossing lies between the last price where gap ≤ 0 and the first where gap ≥
0. Interpolate: price = p1 + (p2 − p1) × (−gap1) ÷ (gap2 − gap1). If the gap is
exactly 0 at a grid price, that price is the point. If it never crosses, report
"n/a" for that point.

**The acceptable range is PMC to PME.**

## Step 4: write it up

`founder/pricing-curve.md` holds: N and the number dropped; the grid table with
all six columns; the four points; the acceptable range; the median of each of the
four answers; and, if a current price was given, whether it sits inside, below or
above the range.

## Sanity checks

- PMC ≤ OPP and IPP ≤ PME should hold. If not, re-count; if it still fails, say
  the answers are too scattered to trust.
- Spot-check two grid rows by recounting from the raw rows.
- The points are precise to about one grid step; report them as such, not to
  the cent.
- Simulated answers choose what to test, never the final price.
