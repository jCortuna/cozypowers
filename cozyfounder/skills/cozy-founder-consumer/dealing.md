# Dealing the persona cards

How `cozy-founder-consumer` turns `founder/customer.json` into one card per buyer.
There is no script and no randomness: the deal is a fixed rule, so the same
customer file, the same panel size and the same **stride** always give the same
cards. That is what lets `cozy-founder-offer` re-test a new offer on the same
buyers.

## Inputs

- n = panel size (20 by default; 100 only after the user confirms the cost).
- The `segments` (each with `share` and `income` [low, high]), `behaviours` (each
  with `share` and `how`), `objections`, optional `habits`, optional `age`
  [low, high] (default [25, 45]).
- k = the stride: the smallest whole number **7 or above that shares no factor
  with n** (7 for n = 20 and n = 100). A different k gives a fresh deal; record
  whichever k was used.

## Step 1: quotas (largest remainder)

For the segments: raw count = n × share ÷ (sum of shares). Give each segment the
whole part of its raw count. Hand the units still missing, one each, to the
segments with the largest fractional parts. The counts must add up to n exactly.
Do the same for the behaviours.

Example, n = 20, shares 0.45 / 0.40 / 0.15: raw 9.0 / 8.0 / 3.0 → 9 / 8 / 3.

## Step 2: the two lists

- **Segment list**: every segment repeated by its count, in file order (positions
  0 to n − 1).
- **Behaviour list**: the same for behaviours.

## Step 3: one card per position i = 0 .. n − 1

| field | rule |
| --- | --- |
| id | `P` + (i + 1) zero-padded to three digits: P001, P002 ... |
| name | the (i + 1)th name in the list below |
| segment | segment list[i] |
| behaviour | behaviour list[(i × k) mod n], with its `how` line |
| income | for the j-th card (from 0) of a segment that has c cards: low + (high − low) × (j + 0.5) ÷ c, rounded to the nearest 1,000 |
| age | age_low + round((age_high − age_low) × (((i × k) mod n) + 0.5) ÷ n) |
| objection | objections[i mod number of objections] |
| habit | habits[(i × 3) mod number of habits], or none if there are no habits |

The stride spreads every behaviour across every segment, so no segment ends up
made only of deal hunters.

## Step 4: write and show

Write `founder/panel/personas.md`: a line with n and k, then one table row per
card (`id | name | age | segment | income | behaviour | objection | habit`).
Before running anything, show the user the segment and behaviour counts so they
can see the panel is shaped like their customer.

## Names

Use in this order, wrapping round with a " 2" suffix if n exceeds 100:

Ana, Ben, Carla, Dev, Elif, Farid, Gina, Hiro, Imani, Jonas, Kavya, Leo, Mariam,
Nate, Olu, Paz, Quentin, Rin, Samir, Tala, Umar, Vera, Wen, Xavi, Yasmin, Zane,
Abby, Bruno, Cleo, Dante, Esther, Femi, Greta, Hassan, Ida, Joel, Kemi, Lars,
Mona, Nikhil, Oona, Pierre, Rahel, Silas, Tomoko, Ugo, Vivian, Wade, Ximena,
Yosef, Zola, Aiden, Bianca, Cyrus, Dalia, Emre, Flor, Gideon, Hanna, Isaac,
Jia, Kofi, Luz, Milo, Nadia, Otto, Priya, Rafael, Sunny, Theo, Uma, Viktor,
Willa, Yara, Zeke, Amira, Boris, Celia, Dmitri, Erin, Faisal, Gemma, Hugo, Ines,
Jasper, Kira, Luca, Mei, Noor, Oscar, Petra, Reza, Sofia, Tariq, Una, Vito,
Wren, Yuki, Zainab, Arlo
