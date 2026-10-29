# CFO formulas

The calculation `cozy-founder-cfo` performs by hand. There is no script: you do
every step yourself and **show the working** in `founder/cfo.md`, so the user can
re-check any line with a calculator.

## Inputs (from `founder/numbers.json`)

| symbol | field | meaning |
| --- | --- | --- |
| P | `price` | price of one unit, before tax |
| V | sum of `variable[].cost` | direct cost of ONE unit |
| F | sum of `fixed_monthly[].cost` | costs paid every month regardless of sales |
| S | sum of `startup[].cost` | one-off spend before opening |
| D | `days_per_month` | selling days in a month (30 if not given) |
| Q | `plan_per_day` | units a day once running |
| r1..r12 | `ramp_per_day` | units a day in each month of year 1 (if absent, every month = Q) |
| K | `capacity_per_day` | most units a day you can physically sell (optional) |

Validate before calculating. Stop and ask, never fill in, if: `price` is missing
or not above zero; a `cost` is not a number; neither `plan_per_day` nor
`ramp_per_day` is given; `ramp_per_day` does not have exactly 12 numbers. If
`plan_per_day` is absent, Q = r12.

## Step 1: one unit

- Contribution **C = P − V**.
- Contribution share **C% = C ÷ P**.

## Step 2: the margin that matters

- Break-even per day **B = F ÷ (C × D)**. Report it rounded **up** to a whole
  unit. If C ≤ 0, break-even is "never".
- Margin at plan **M = (C − F ÷ (Q × D)) ÷ P**. Report as a whole percent.

## Step 3: year 1, month by month

Start with cumulative = −S. For each month m = 1..12:

1. units = r_m × D
2. revenue = units × P
3. profit = units × C − F
4. cumulative = previous cumulative + profit

Then:

- Year 1 revenue = sum of the 12 revenues.
- Year 1 operating profit **Y = sum of the 12 profits**.
- Year 1 after startup = Y − S.
- Payback month = the first month where cumulative ≥ 0 (else "not within year 1").
- **Cash needed** = the deepest point the cumulative reaches, as a positive
  number, counting −S itself as the starting point: cash = −min(−S, every
  monthly cumulative).

Keep cents in every intermediate step; round only when writing the table
(money to whole dollars, percentages to whole percents).

## Step 4: the what-ifs

Re-run steps 1 to 3 three more times and report margin at plan, break-even per
day and Y for each:

| scenario | change |
| --- | --- |
| Price −10% | P × 0.9 |
| Volume −20% | Q × 0.8 and every r_m × 0.8 |
| Unit costs +15% | V × 1.15 |

Volume does not change break-even (B does not depend on Q); if your table shows
it moving, you made an error.

## Step 5: red flags

Flag each that is true:

- C ≤ 0: every unit loses money before rent and salaries.
- K is given and B > K: break-even is above capacity.
- K is given and Q > K: the plan is above capacity.
- Y < 0: year 1 loses money on operations.
- No payback month: the startup spend is not earned back in year 1.

## Step 6: check your own arithmetic

Before writing the report, run these three cross-checks and fix anything that
fails:

1. C × D × B should come out at roughly F (within one unit's contribution × D).
2. The month-12 cumulative should equal Y − S exactly.
3. At least one month's line, recomputed from scratch, must match your table.

Record in `founder/cfo.md` that the three checks passed.

## Worked example (the matcha café in `example-numbers.json`)

P = 6.50; V = 0.92 + 0.38 + 0.24 + 0.20 = 1.74; F = 15,500 + 11,040 = 26,540;
S = 8,400 + 6,900 + 4,250 + 1,850 + 2,380 + 1,500 = 25,280; D = 30; Q = 383;
K = 600.

- C = 6.50 − 1.74 = **4.76**; C% = 73%.
- B = 26,540 ÷ (4.76 × 30) = 26,540 ÷ 142.80 = 185.85 → **186 cups a day**.
- M = (4.76 − 26,540 ÷ 11,490) ÷ 6.50 = (4.76 − 2.3098) ÷ 6.50 = **38%**.
- Month 1: 140 × 30 = 4,200 cups; revenue $27,300; profit 4,200 × 4.76 −
  26,540 = −$6,548; cumulative −25,280 − 6,548 = −$31,828.
- Month 2: 5,100 cups; profit 24,276 − 26,540 = −$2,264; cumulative −$34,092
  (the lowest point, so **cash needed = $34,092**).
- Months 3 to 12 continue the same way; cumulative first turns positive in
  **month 8** ($10,729).
- **Y = $93,926** on $563,160 revenue; after startup $68,646.
- What-ifs: price −10% → 31%, 216 a day, $37,610; volume −20% → 29%, 186 a
  day, $11,445; unit costs +15% → 34%, 197 a day, $71,313.
- No red flags.

If your hand-run of this example does not reproduce these numbers, stop and find
the error before you calculate the user's business.
