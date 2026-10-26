---
title: "Savage Criterion"
domain: "Optimization & Control"
course: "Stochastic Optimization"
level: BSc
status: drafted
confidence: 0
tags: [decision-analysis, stochastic-optimization]
---
## Definition
Under [[Decision Making Under Uncertainty]], the **Savage criterion** (minimax regret) first transforms the payoff table into a **regret** (opportunity loss) table, then applies a Wald-style minimax to the *regrets* rather than to the raw payoffs.

For a profit table, the regret of choosing $a_i$ when $s_j$ occurs is how much worse that choice was than the best alternative would have been, had $s_j$ been known in advance:
$$
r(a_i, s_j) = \max_{a_k} v(a_k, s_j) - v(a_i, s_j) \ge 0.
$$
(For a cost table, flip the sign: $r(a_i,s_j) = v(a_i,s_j) - \min_{a_k} v(a_k, s_j)$.) The recommended alternative minimizes the worst-case regret:
$$
a^\star = \arg\min_{a_i} \max_{s_j} r(a_i, s_j).
$$

## Properties
### Regret is always nonnegative, and zero along the column optimum
By construction, every column of the regret table contains at least one $0$ — the alternative that was actually best for that state of nature has no regret there. This makes the regret table a useful diagnostic: a row with many small regrets is a "robust" choice even if it's never the single best.

### Worked example: newsvendor (strawberry boxes)
Converting the payoff table of [[Laplace Criterion]] into a regret table (subtracting each column's max from every entry) gives row maxima $33, 22, 14, 21$; Savage picks $a_3$ (offer 14 boxes, worst-case regret \$14) — agreeing with Laplace here but not with Wald ($a_1$) or Maximax ($a_4$) on the same underlying data, illustrating [[Decision Making Under Uncertainty]]'s point that the four criteria need not agree.

### Relationship to Expected Opportunity Loss
Savage's regret table is the same object [[Expected Opportunity Loss|EOL]] is built on; the difference is that Savage takes a *worst-case* (minimax) summary of the regret row, while EOL takes an *expectation* over known probabilities $P(s_j)$ — i.e. Savage is the "under uncertainty" analogue of the "under risk" EOL criterion.

## See also
[[Decision Making Under Uncertainty]], [[Wald Criterion]], [[Laplace Criterion]], [[Maximax Criterion]], [[Expected Opportunity Loss]]
