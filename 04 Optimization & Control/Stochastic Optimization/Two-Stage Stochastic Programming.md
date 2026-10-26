---
title: "Two-Stage Stochastic Programming"
domain: "Optimization & Control"
course: "Stochastic Optimization"
level: BSc
status: drafted
confidence: 0
tags: [stochastic-programming, stochastic-optimization]
---
## Definition
A **two-stage stochastic program** splits decision variables into **first-stage** decisions $x$, which must be fixed *before* the uncertainty resolves, and **second-stage (recourse) decisions** $y_s$, which are chosen *after* a scenario $s$ (with known probability $p_s$) is observed and can therefore react to it. Writing the uncertainty as a finite set of scenarios $s = 1,\dots,S$, the **extensive form** (also: deterministic equivalent) states the whole two-stage problem as one ordinary optimization problem, with one full copy of the second-stage variables and constraints per scenario, coupled only through the shared first-stage variables and an expected-cost (or expected-profit) objective:
$$
\min_x\; c^\top x + \sum_{s=1}^{S} p_s\, q_s^\top y_s \quad \text{s.t.} \quad Ax \le b,\quad T_s x + W y_s \le h_s \;\; \forall s,\quad x, y_s \ge 0.
$$
This is "extensive" because it writes out the second-stage variables explicitly for *every* scenario, rather than leaving the recourse decision implicit.

## Properties
### Worked example: the farmer's problem
A farmer plants wheat, corn, and beets on 500 hectares. First-stage variables $x_1, x_2, x_3$ are hectares planted of each crop; second-stage variables $w_i$ (tons sold), $y_i$ (tons bought) depend on the year's yield, which the farmer does not control. Yields are modeled with three equally-likely scenarios ($p_s = 1/3$): above-average, average, below-average (±20% of the mean yield 2.5/3/20 tons/hectare for wheat/corn/beets). The extensive form is
$$
\min\; 150x_1+230x_2+260x_3 - \tfrac13\sum_{s=1}^3\big(170w_{1s}-238y_{1s}+150w_{2s}-210y_{2s}+36w_{3s}+10w_{4s}\big)
$$
subject to the land constraint $x_1+x_2+x_3\le 500$, per-crop balance constraints (e.g. $2.5x_1+y_1-w_1\ge 200$ tons of wheat needed for cattle feed, repeated per scenario with the scenario-specific yield), and a sugar-beet quota that only allows the first 6,000 tons to sell at the favorable \$36/ton price (excess at \$10/ton). Solving gives first-stage areas that hedge across all three scenarios, with expected profit \$108,390/year — worse than any single scenario's own optimum, but the best achievable *without* knowing which scenario will occur.

### First-stage decisions are "here-and-now"; second-stage are "wait-and-see"
The planting areas $(x_1,x_2,x_3)$ must be the same across every scenario row of the extensive form (they are decided before the weather is known); the buy/sell quantities $w_{is}, y_{js}$ are indexed by scenario $s$ because they can legitimately differ once the yield is observed. This first/second-stage split is what makes the model "stochastic programming with recourse" rather than either a fully deterministic LP or a set of independent scenario LPs.

### Comparing three planning philosophies
The farmer's example is used to contrast three ways of handling the uncertainty, quantified by [[Expected Value of Perfect Information]] and [[Value of the Stochastic Solution]]:
- **Perfect information**: choose the scenario-optimal areas *after* observing the scenario — average profit \$115,406/year (unattainable in practice; the benchmark for EVPI).
- **Stochastic solution (recourse problem, RP)**: solve the extensive form above once, fixing $x$ before the scenario is known — \$108,390/year.
- **Expected-value solution (EEV)**: plan the areas assuming the *average* yield will occur (i.e., solve a deterministic LP with expected yields, as in [[Decision Making Under Risk]]'s "solución de valor esperado"), then evaluate that fixed plan's average profit across the three scenarios — \$107,240/year, the worst of the three.

## See also
[[Decision Making Under Risk]], [[Expected Value of Perfect Information]], [[Value of the Stochastic Solution]], [[Risk-Averse Stochastic Programming]]
