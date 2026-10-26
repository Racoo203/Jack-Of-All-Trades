---
title: "Maximax Criterion"
domain: "Optimization & Control"
course: "Stochastic Optimization"
level: BSc
status: drafted
confidence: 0
tags: [decision-analysis, stochastic-optimization]
---
## Definition
Under [[Decision Making Under Uncertainty]], the **Maximax criterion** (optimistic approach) assumes the best possible state of nature will occur for whichever alternative is chosen: for each alternative, take its *best-case* payoff, then pick the alternative whose best case is best overall,
$$
a^\star = \arg\max_{a_i} \max_{s_j} v(a_i, s_j).
$$
It is the mirror image of the [[Wald Criterion]] (which takes the worst case of each row); together they bound the range of "reasonable" recommendations an unweighted criterion can give.

## Properties
### Worked example: newsvendor (strawberry boxes)
Using the payoff table from [[Laplace Criterion]], the row maxima are $132, 143, 154, 165$, so Maximax picks $a_4$ (offer 15 boxes — the only way to realize the best-case payoff of \$165, achieved only if demand also happens to be 15).

### Worked example: farmer's land allocation
Given four land-allocation decisions $d_1,\dots,d_4$ with profits varying by scenario (regular/good/bad year), the optimistic approach takes the maximum profit achievable by each decision across scenarios and picks the largest of those maxima — in the course's worked table this selects $d_2$, "the decision that can lead to the best of the results."

## See also
[[Decision Making Under Uncertainty]], [[Wald Criterion]], [[Laplace Criterion]], [[Savage Criterion]]
