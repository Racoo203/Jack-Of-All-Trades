---
title: "Value of the Stochastic Solution"
domain: "Optimization & Control"
course: "Stochastic Optimization"
level: BSc
status: drafted
confidence: 0
tags: [stochastic-programming, stochastic-optimization]
---
## Definition
In [[Two-Stage Stochastic Programming]], the **value of the stochastic solution** (VSS) measures how much better the true stochastic program's solution (RP) is than the naive plan obtained by solving the problem once with expected/average parameters (EEV) and then evaluating that fixed plan's actual expected performance across the real scenarios:
$$
VSS = RP - EEV \quad(\text{maximization}), \qquad VSS = EEV - RP \quad(\text{minimization}),
$$
using whichever sign convention keeps $VSS \ge 0$ for the problem's own objective sense. VSS answers "what does explicitly modeling the uncertainty (recourse) buy me, over just plugging in expected values?" — as opposed to [[Expected Value of Perfect Information|EVPI]], which answers "what would knowing the future buy me, over modeling the uncertainty at all?"

## Properties
### VSS vs. EVPI measure different things
$$
EVPI = \text{(perfect information)} - RP, \qquad VSS = RP - EEV,
$$
so together they decompose the full "value of modeling" spectrum: perfect information $\ge$ stochastic solution (RP) $\ge$ expected-value solution (EEV). The course stresses that in most real applications no perfect forecast is available, which is exactly why VSS — the payoff from using the stochastic model *at all*, relative to the naive deterministic shortcut — is usually the more actionable of the two numbers.

### Worked example: the farmer's problem
Using the three profit figures from [[Two-Stage Stochastic Programming]]: the stochastic solution (RP) achieves \$108,390/year in expectation; the expected-value solution (EEV) — always planting the areas that would be optimal *if* the average yield always occurred — achieves only \$107,240/year when its fixed plan is actually evaluated against the three real scenarios. Hence
$$
VSS = 108{,}390 - 107{,}240 = \$1{,}150 \text{ per year}.
$$
This \$1,150 is "the loss from not considering the random variations" — i.e., exactly what is lost by planning with a single expected-yield scenario instead of the full three-scenario recourse model.

## See also
[[Two-Stage Stochastic Programming]], [[Expected Value of Perfect Information]], [[Decision Making Under Risk]]
