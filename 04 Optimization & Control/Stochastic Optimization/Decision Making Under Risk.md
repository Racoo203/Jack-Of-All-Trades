---
title: "Decision Making Under Risk"
domain: "Optimization & Control"
course: "Stochastic Optimization"
level: BSc
status: drafted
confidence: 0
tags: [decision-analysis, stochastic-optimization]
---
## Definition
Decision-making is **under risk** (as opposed to [[Decision Making Under Uncertainty]]) when probabilities $P(s_j)$ are known or assigned to each state of nature $s_j$. The standard criterion is the **expected monetary value (EMV)**: pick the alternative maximizing (for profits) or minimizing (for costs) the expectation of the payoff row,
$$
E(a_i) = \sum_{j=1}^n v(a_i, s_j)\,P(s_j), \qquad a^\star = \arg\max_i E(a_i).
$$
In matrix form, with $M$ the payoff matrix (alternatives as rows) and $p$ the column vector of state probabilities, $E = Mp$.

## Properties
### Worked example: matrix form (investment choice)
Three investments (conservative, speculative, contracyclical) against three economic scenarios (improves / stable / worsens) with prior $p = (0.1, 0.5, 0.4)^\top$ and payoff matrix (in millions)
$$
M = \begin{bmatrix} 30 & 5 & -10 \\ 40 & 10 & -30 \\ -10 & 0 & 15 \end{bmatrix} \implies E(A) = Mp = \begin{bmatrix}1.5\\-3\\5\end{bmatrix},
$$
so the contracyclical investment ($E(A_3) = \$5$M) is preferred under this prior. Re-running with $p=(0.1,0.3,0.6)^\top$ still favors $A_3$ ($\$8$M); with $p=(0.1,0.7,0.2)^\top$ the ranking flips and the speculative investment $A_2$ becomes best ($\$5$M) — the EMV recommendation is sensitive to the assumed probabilities, unlike the criteria in [[Decision Making Under Uncertainty]].

### Decomposing a per-unit expectation
When a payoff is a product of a state-independent factor and a state-dependent one — e.g. $\text{Ingreso Neto} = \frac{\text{Ingreso Neto}}{\text{Bushel}} \cdot \frac{\text{Bushel}}{\text{Hectárea}} \cdot \text{Hectáreas}$ — only the state-dependent factor needs to go inside the expectation:
$$
E(\text{Ingreso Neto}_i) = \left(\frac{\text{Ingreso Neto}}{\text{Bushel}}\right)_i \cdot E\left[\left(\frac{\text{Bushel}}{\text{Hectárea}}\right)_i\right] \cdot \text{Hectáreas},
$$
since the per-bushel income and the planted area don't depend on the weather state, only the yield per hectare does.

## See also
[[Decision Making Under Uncertainty]], [[Expected Value of Perfect Information]], [[Expected Opportunity Loss]], [[Two-Stage Stochastic Programming]]
