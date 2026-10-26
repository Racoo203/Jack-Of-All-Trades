---
title: "Expected Opportunity Loss"
domain: "Optimization & Control"
course: "Stochastic Optimization"
level: BSc
status: drafted
confidence: 0
tags: [decision-analysis, stochastic-optimization]
---
## Definition
Under [[Decision Making Under Risk]], the **expected opportunity loss** (EOL; called **POE**, "Pérdida de Oportunidad Esperada", in the course) is the expectation, over the known state probabilities, of the regret table used in the [[Savage Criterion]]:
$$
EOL(a_i) = \sum_{j=1}^n r(a_i, s_j)\, P(s_j), \qquad r(a_i, s_j) = \max_{a_k} v(a_k, s_j) - v(a_i, s_j),
$$
and the recommended alternative minimizes it, $a^\star = \arg\min_i EOL(a_i)$. This is the "under risk" counterpart of Savage's minimax regret: Savage takes a worst-case over the regret row, EOL takes an expectation.

## Properties
### Equivalence with the EMV criterion and with EVPI
Because $r(a_i, s_j) = \max_{a_k}v(a_k,s_j) - v(a_i,s_j)$, we have $EOL(a_i) = ECPI - E(a_i)$ (see [[Expected Value of Perfect Information]] for $ECPI$), which is decreasing in $E(a_i)$ — so minimizing EOL and maximizing EMV always select the **same** alternative, and at that alternative, $EOL(a^\star) = ECPI - E(a^\star) = EVPI$.

### Worked example: dress shop
Building the regret table from [[Expected Value of Perfect Information]]'s payoff table (subtract each column's max):

| | Bueno | Regular | Malo |
|---|---|---|---|
| Pequeña | 25,000 | 10,000 | 40,000 |
| Mediana | 0 | 0 | 60,000 |
| Ninguna | 100,000 | 35,000 | 0 |

With $P=(0.2,0.5,0.3)$: $EOL(A_1) = 22{,}000$, $EOL(A_2)=18{,}000$, $EOL(A_3)=37{,}500$. The minimum, $EOL(A_2)=18{,}000$, matches $EVPI=18{,}000$ from [[Expected Value of Perfect Information]] exactly, and $A_2$ (medium store) is the same alternative EMV picked.

### Worked example: mutual funds
For the three-fund allocation of [[Decision Making Under Risk]] with $P=(0.1,0.5,0.4)$, the opportunity-loss matrix
$$
R = \begin{bmatrix} 0.00 & 0.00 & 0.22 \\ 0.15 & 0.02 & 0.00 \\ 0.03 & 0.00 & 0.10 \end{bmatrix} \implies EOL = Rp = \begin{bmatrix}8.8\%\\2.5\%\\4.3\%\end{bmatrix},
$$
so $EOL$ is minimized by the speculative fund (2.5%) — the same fund EMV favored in [[Decision Making Under Risk]].

## See also
[[Savage Criterion]], [[Decision Making Under Risk]], [[Expected Value of Perfect Information]]
