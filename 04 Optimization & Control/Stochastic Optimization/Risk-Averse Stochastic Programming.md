---
title: "Risk-Averse Stochastic Programming"
domain: "Optimization & Control"
course: "Stochastic Optimization"
level: BSc
status: drafted
confidence: 0
tags: [stochastic-programming, stochastic-optimization]
---
## Definition
The plain [[Two-Stage Stochastic Programming|two-stage recourse objective]] $\min_x c^\top x + \sum_s p_s q_s^\top y_s$ optimizes only the *expected* cost, and so is indifferent between two plans with the same mean cost even if one has much higher variability — it "does not adequately account for risk," which is inappropriate whenever the decision-maker is risk-averse. A **risk-averse (mean-risk) stochastic program** augments the expected-cost objective with a penalty on unfavorable deviation from the mean, controlled by a risk-aversion weight $w \ge 0$:
$$
\min_x \; \underbrace{c^\top x + \sum_s p_s q_s^\top y_s}_{\text{expected cost}} \;+\; w \cdot \underbrace{\sum_s p_s \left[\max\!\big(0,\; q_s^\top y_s - \overline{q^\top y}\big)\right]}_{\text{penalty on above-average-cost scenarios}},
$$
where $\overline{q^\top y} = \sum_s p_s\, q_s^\top y_s$ is the expected cost. Larger $w$ means greater risk aversion; $w=0$ recovers the plain (risk-neutral) two-stage program.

## Properties
### The penalty term is nonlinear
Because the penalty term involves $\max(0, \cdot)$ of a quantity that is itself a function of the decision variables, the mean-risk objective is **non-linear**, and solving it in practice requires heuristics rather than the linear-programming machinery sufficient for the risk-neutral extensive form. Varying $w$ traces out a family of solutions the decision-maker can choose among (a risk/return trade-off curve), rather than a single "correct" answer.

### Worked example: international sourcing under uncertainty
A firm selects a subset of internationally located suppliers $i \in \{1,\dots,m\}$ to serve plants $j \in \{1,\dots,n\}$, facing supplier fixed costs $f_i$, shipping costs $c_{ij}$, supplier capacities $b_i$, and scenario-dependent demand $d_{js}$ and exchange rates $e_{is}$ (with scenario probability $p_s$). **Design variables** (which suppliers to use) are first-stage and fixed once and for all — switching suppliers later is too costly given setup costs; **control variables** (how much to ship from each selected supplier to each plant) are second-stage, chosen per scenario subject to demand-satisfaction and capacity constraints. Because currency and demand risk make the plain expected-cost objective inadequate, the model instead penalizes scenarios whose shipping cost exceeds the *average* shipping cost — this is exactly the risk being avoided — with the weight $w$ tunable to the decision-maker's risk tolerance; the model is also formulated with **finite** supplier capacity (harder than the more common infinite-capacity assumption in the literature), citing Dantzig's 1955 "Linear Programming Under Uncertainty" as the origin of treating optimization parameters as uncertain rather than deterministic.

## See also
[[Two-Stage Stochastic Programming]], [[Value of the Stochastic Solution]], [[Decision Making Under Risk]]
