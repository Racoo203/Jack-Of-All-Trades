---
title: Spatial Homogeneity
domain: Stochastic Processes
course: Stochastic Processes
unit: Foundations & Random Walks
level: MSc
status: seeding
confidence: 0
tags: [seeding]
---
## Definition
A [[Random Walk|random walk]] $\{S_n, n \in T\}$ is spatially homogeneous if, for all $n > m \geq 0$ and $a, b, k \in \mathbb{Z}$ such that $Pr(S_m = a) \neq 0$ and $Pr(S_m = a + b) \neq 0$,
$$
Pr(S_n = k \mid S_m = a) = Pr(S_n = k + b \mid S_m = a + b)
$$
Informally: the probability of moving between two states over a given number of steps depends only on the *distance* between the states, not on their absolute position.

## Properties
### Proof for a random walk
Let $S_n = S_0 + \sum_{t=1}^n X_t$ with the $X_t$ [[Independent and Identically Distributed (i.i.d)|i.i.d.]]. For the left-hand side,
$$
Pr(S_n = k \mid S_m = a) = Pr\left(S_m + \sum_{t=m+1}^{n} X_t = k \;\middle|\; S_m = a\right) = Pr\left(\sum_{t=m+1}^{n} X_t = k - a\right)
$$
For the right-hand side,
$$
Pr(S_n = k + b \mid S_m = a + b) = Pr\left(S_m + \sum_{t=m+1}^{n} X_t = k + b \;\middle|\; S_m = a + b\right) = Pr\left(\sum_{t=m+1}^{n} X_t = k - a\right)
$$
Both sides reduce to the same expression, so they are equal. The proof only uses the i.i.d. structure of the increments, so it holds for *any* random walk, not only the [[Simple Random Walk|simple]] one.

### Interpretation
For example, in the [[Gambler's Ruin|gambler's ruin]] setting, the probability of a gambler's fortune increasing from 10 to 12 in two steps coincides with the probability of an increase from 100 to 102 in two steps — both equal $p^2$.

## See also
- [[Random Walk]]
- [[Time Homogeneity]]
- [[Simple Random Walk]]
