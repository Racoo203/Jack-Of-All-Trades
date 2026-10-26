---
title: Time Homogeneity
domain: Stochastic Processes
course: Stochastic Processes
unit: Foundations & Random Walks
level: MSc
status: seeding
confidence: 0
tags: [seeding]
---
## Definition
A [[Random Walk|random walk]] $\{S_n, n \in T\}$ is time homogeneous if, for every $n, m > 0$,
$$
Pr(S_n = k \mid S_0 = a) = Pr(S_{m+n} = k \mid S_m = a)
$$
Informally: the probability of moving between two states over a given number of steps does not depend on *when* the clock starts — only on the number of steps elapsed.

## Properties
### Proof for a random walk
Let $S_n = S_0 + \sum_{t=1}^n X_t$ with the $X_t$ [[Independent and Identically Distributed (i.i.d)|i.i.d.]]. For the left-hand side,
$$
Pr(S_n = k \mid S_0 = a) = Pr\left(S_0 + \sum_{t=1}^{n} X_t = k \;\middle|\; S_0 = a\right) = Pr\left(\sum_{t=1}^{n} X_t = k - a\right)
$$
For the right-hand side,
$$
Pr(S_{m+n} = k \mid S_m = a) = Pr\left(S_m + \sum_{t=m+1}^{m+n} X_t = k \;\middle|\; S_m = a\right) = Pr\left(\sum_{t=m+1}^{m+n} X_t = k - a\right)
$$
Since the $X_t$ are i.i.d., $\sum_{t=1}^{n} X_t$ and $\sum_{t=m+1}^{m+n} X_t$ (both sums of $n$ i.i.d. terms) have the same distribution, so the two probabilities coincide. As with [[Spatial Homogeneity]], the proof holds for any random walk, not only the [[Simple Random Walk|simple]] one.

## See also
- [[Random Walk]]
- [[Spatial Homogeneity]]
- [[Simple Random Walk]]
