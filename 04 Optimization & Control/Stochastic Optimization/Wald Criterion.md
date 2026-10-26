---
title: "Wald Criterion"
domain: "Optimization & Control"
course: "Stochastic Optimization"
level: BSc
status: drafted
confidence: 0
tags: [decision-analysis, stochastic-optimization]
---
## Definition
Under [[Decision Making Under Uncertainty]], the **Wald criterion** (pessimistic / conservative approach) assumes nature is adversarial: for each alternative, look only at its *worst-case* payoff across all states of nature, then pick the alternative whose worst case is best.

For a **profit** table (maximize):
$$
a^\star = \arg\max_{a_i} \min_{s_j} v(a_i, s_j) \qquad \text{("maximin")}.
$$
For a **cost** table (minimize):
$$
a^\star = \arg\min_{a_i} \max_{s_j} v(a_i, s_j) \qquad \text{("minimax")}.
$$
Both forms guarantee the best possible worst case — hence "pessimistic": the decision-maker plans for the least favorable state of nature actually occurring.

## Properties
### Worked example: newsvendor (strawberry boxes)
Using the payoff table from [[Laplace Criterion]], the row minima are $132, 125, 118, 111$, so Wald picks $a_1$ (offer only 12 boxes — guaranteed profit of \$132 regardless of demand), even though it never has the highest payoff in any single column.

### Worked example: sizing a summer camp (cost table)
A camp's cost table over four possible camp sizes $a_1,\dots,a_4$ and four attendance levels $s_1,\dots,s_4$ gives row maxima (worst-case costs) $25, 23, 21, 30$ (in thousands of dollars); Wald (minimax, since this is a cost table) picks $a_3$ at \$21k — the size whose worst-case cost is smallest.

## See also
[[Decision Making Under Uncertainty]], [[Laplace Criterion]], [[Maximax Criterion]], [[Savage Criterion]]
