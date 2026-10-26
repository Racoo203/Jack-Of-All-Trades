---
title: "Decision Making Under Uncertainty"
domain: "Optimization & Control"
course: "Stochastic Optimization"
level: BSc
status: drafted
confidence: 0
tags: [decision-analysis, stochastic-optimization]
---
## Definition
A decision problem is set up as a **payoff matrix** $v(a_i, s_j)$ over a finite set of **alternatives** (actions) $a_1,\dots,a_m$ that the decision-maker controls, and a finite set of **states of nature** $s_1,\dots,s_n$ representing the uncertain conditions the decision-maker does not control. Decision-making is **under uncertainty** when no probabilities $P(s_j)$ are assumed known or assigned to the states of nature — only the payoff table itself is used. (Contrast [[Decision Making Under Risk]], where the $P(s_j)$ are known.)

Each row of the table is one alternative; each column is one state of nature; the entry $v(a_i, s_j)$ is the payoff (profit, cost, utility) of choosing $a_i$ when $s_j$ turns out to be true.

## Properties
### The criteria disagree by design
Four criteria are used to reduce the payoff table to a single recommended alternative: [[Laplace Criterion]] (equal likelihood), [[Wald Criterion]] (pessimistic, maximin/minimax), [[Maximax Criterion]] (optimistic), and [[Savage Criterion]] (minimax regret). Because they encode different attitudes toward risk and different implicit weightings of the states of nature, they can — and routinely do — recommend *different* alternatives for the same payoff table; this disagreement is the pedagogical point, not a bug. There is no criterion that dominates the others; the choice of criterion is itself a modeling decision reflecting the decision-maker's risk posture.

### Worked example (shared across all four criteria)
A weather-dependent production decision: an alternative $a_i \in \{$Botas, Zapatos, Sandalias$\}$ (boots, shoes, sandals) against states of nature $s_j \in \{$Frío, Normal, Cálido$\}$ (cold, normal, hot), with payoff table (profit in €)

| | Frío | Normal | Cálido |
|---|---|---|---|
| Botas | 60,000 | 15,000 | 2,500 |
| Zapatos | 5,000 | 30,000 | 10,000 |
| Sandalias | -5,000 | 7,500 | 50,000 |

is carried through [[Laplace Criterion]], [[Wald Criterion]], [[Maximax Criterion]], and [[Savage Criterion]] to show all four answers on one table.

## See also
[[Laplace Criterion]], [[Wald Criterion]], [[Maximax Criterion]], [[Savage Criterion]], [[Decision Making Under Risk]], [[Expected Opportunity Loss]]
