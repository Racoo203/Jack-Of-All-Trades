---
title: "Expected Value of Perfect Information"
domain: "Optimization & Control"
course: "Stochastic Optimization"
level: BSc
status: drafted
confidence: 0
tags: [decision-analysis, stochastic-optimization]
---
## Definition
Under [[Decision Making Under Risk]], the **expected value of perfect information** (EVPI; called **VEIP** in the course's Spanish notation) measures how much a decision-maker should be willing to pay to know, in advance, exactly which state of nature will occur.

It is computed in two steps. First, the **expected value with perfect information** (ECPI / VECIP) assumes the decision-maker learns $s_j$ *before* choosing, so a (possibly different) best alternative can be chosen for each state:
$$
ECPI = \sum_{j=1}^n \left(\max_{a_i} v(a_i, s_j)\right) P(s_j).
$$
Then
$$
EVPI = ECPI - E(a^\star), \qquad E(a^\star) = \max_{a_i} E(a_i)
$$
is the gap between the (unattainable) clairvoyant expectation and the best achievable EMV without foreknowledge — see [[Decision Making Under Risk]] for $E(a_i)$.

## Properties
### $EVPI = EOL$ at the optimal alternative
The [[Expected Opportunity Loss]] of the EMV-optimal alternative equals EVPI exactly — both measure the same gap, from opposite directions (one from the clairvoyant benchmark down, the other from the regret table up). This is a useful accuracy check when computing both.

### Worked example: dress shop
María Rojas is choosing between a small store, medium store, or no store, against a market that is good/regular/bad with $P = (0.2, 0.5, 0.3)$ and profit table

| | Bueno | Regular | Malo |
|---|---|---|---|
| Pequeña | 75,000 | 25,000 | -40,000 |
| Mediana | 100,000 | 35,000 | -60,000 |
| Ninguna | 0 | 0 | 0 |

$E(A_1) = 15{,}500$, $E(A_2) = 19{,}500$, $E(A_3) = 0$, so $a^\star = A_2$ (medium store). The clairvoyant benchmark takes the column maxima: $ECPI = (100{,}000)(0.2)+(35{,}000)(0.5)+(0)(0.3) = 37{,}500$. Hence
$$
EVPI = 37{,}500 - 19{,}500 = 18{,}000.
$$
Raúl should not pay more than \$18,000 for a perfect market forecast.

### Worked example: the farmer's problem
In the two-stage stochastic program of [[Two-Stage Stochastic Programming]], the wait-and-see profit (average of the three scenario-optimal profits, \$115,406/year) minus the stochastic-program's expected profit (\$108,390/year) gives $EVPI = \$7{,}016$/year — the value of knowing the year's yield conditions before planting.

## See also
[[Decision Making Under Risk]], [[Expected Opportunity Loss]], [[Two-Stage Stochastic Programming]], [[Value of the Stochastic Solution]]
