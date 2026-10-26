---
title: "Laplace Criterion"
domain: "Optimization & Control"
course: "Stochastic Optimization"
level: BSc
status: drafted
confidence: 0
tags: [decision-analysis, stochastic-optimization]
---
## Definition
Under [[Decision Making Under Uncertainty]], the **Laplace criterion** (equal-likelihood / principle of insufficient reason) treats all $n$ states of nature as equally likely — since none are actually known, assign each probability $1/n$ — and picks the alternative with the best average payoff:
$$
a^\star = \arg\max_{a_i} \frac{1}{n}\sum_{j=1}^n v(a_i, s_j) \qquad (\text{or } \arg\min \text{ for a cost table}).
$$
It is the only one of the four classical criteria that uses every entry of the payoff table (Wald and Maximax use only one entry per row; Savage uses a transformed table).

## Properties
### Equivalence to expected value with a uniform prior
The Laplace criterion is exactly [[Decision Making Under Risk|expected-value decision-making]] under the specific (assumed, not observed) prior $P(s_j) = 1/n$ for all $j$ — it converts a decision "under uncertainty" into one "under risk" by an assumption of ignorance rather than of evidence.

### Worked example: newsvendor (strawberry boxes)
A store can offer 12, 13, 14, or 15 boxes of strawberries against demand of 12, 13, 14, or 15 boxes, with profit table

| Oferta \ Demanda | 12 | 13 | 14 | 15 |
|---|---|---|---|---|
| 12 | 132 | 132 | 132 | 132 |
| 13 | 125 | 143 | 143 | 143 |
| 14 | 118 | 136 | 154 | 154 |
| 15 | 111 | 129 | 147 | 165 |

Row averages are $132, 138.5, 140.5, 138$, so the Laplace criterion picks $a_3$ (offer 14 boxes), value $140.5$ — different from Wald's recommendation of $a_1$ on the same table (see [[Wald Criterion]]).

## See also
[[Decision Making Under Uncertainty]], [[Wald Criterion]], [[Maximax Criterion]], [[Savage Criterion]], [[Decision Making Under Risk]]
