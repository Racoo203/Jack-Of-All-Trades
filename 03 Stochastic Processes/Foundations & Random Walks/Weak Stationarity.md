---
title: Weak Stationarity
domain: Stochastic Processes
course: Stochastic Processes
unit: Foundations & Random Walks
level: MSc
status: seeding
confidence: 0
tags: [seeding]
---
## Definition
A [[Stochastic Process|stochastic process]] $\{X_t : t \in T\}$ is weakly stationary if:
- $\mu_X(t) = \mu_X$,
- $C_X(t_1, t_2) = C(t_2 - t_1)$, with $t_1, t_2 \in T$, and
- $E[|X_t|^2] < \infty, t \in T$.

That is: 1. The [[Mean Function|mean function]] is constant; 2. The [[Autocovariance function|autocovariance]] of the process is a function of the time differences, and; 3. The second moments are finite at any time.