---
title: "Mean Recurrence Time"
domain: "Optimization & Control"
course: "Stochastic Optimization"
level: BSc
status: drafted
confidence: 0
tags: [markov-chains, stochastic-optimization]
---
## Definition
For a [[Recurrent State|recurrent]] state $j$ of a [[Discrete-Time Markov Chain]], the **mean recurrence time** (also: mean time of first return, $\mu_j$) is the expected number of steps for the chain to return to $j$ for the first time, given that it starts in $j$:
$$
\mu_j = E[T_j \mid X_0 = j], \qquad T_j = \min\{n \ge 1 : X_n = j\}.
$$
$j$ is **positive recurrent** if $\mu_j < \infty$ and **null recurrent** if $\mu_j = \infty$ (only possible on an infinite state space).

## Properties
### Mean recurrence time from the stationary distribution
For an [[Ergodic Markov Chain|ergodic]] chain on a finite state space with [[Stationary Distribution]] $\pi$, every state is positive recurrent and
$$
\mu_j = \frac{1}{\pi_j}.
$$
*Sketch.* By the ergodic theorem for Markov chains, the long-run fraction of time the chain spends in state $j$ equals $\pi_j$. By a renewal-reward argument, visits to $j$ form a renewal process with inter-visit time $T_j$, so the long-run fraction of time in $j$ also equals $1/E[T_j] = 1/\mu_j$ (each "cycle" between consecutive visits has expected length $\mu_j$, and exactly one of those steps is spent "in" $j$). Equating the two expressions for the long-run frequency gives $\pi_j = 1/\mu_j$.

This is exactly what the course calls "a direct byproduct of the steady-state probabilities": once $\pi$ is known (by solving $\pi = \pi P$, or via [[Spectral Decomposition of a Transition Matrix]]), every mean recurrence time follows by inversion — no separate first-step analysis is needed.

### Worked example: two-machine repair shop
For the machine-shop chain with states $X_n \in \{0, 1, 2\}$ (number of working machines) and transition probabilities built from a failure rate $\alpha$ and repair rate $\beta$ (see [[Discrete-Time Markov Chain]] for the transition matrix), once the stationary distribution $\pi = (\pi_0, \pi_1, \pi_2)$ is solved for, the mean recurrence time of "both machines down" ($X_n = 0$) is $\mu_0 = 1/\pi_0$ — the expected number of hours between consecutive visits to a fully-down shop.

## Examples
For the elevator chain of [[Spectral Decomposition of a Transition Matrix]], $\pi = (8/17, 4/17, 5/17)$ for (Bajo, Piso 1, Piso 2), so the mean recurrence times are $\mu_{\text{Bajo}} = 17/8 = 2.125$, $\mu_{\text{Piso 1}} = 17/4 = 4.25$, $\mu_{\text{Piso 2}} = 17/5 = 3.4$ trips.

## See also
[[Ergodic Markov Chain]], [[Recurrent State]], [[Stationary Distribution]], [[Spectral Decomposition of a Transition Matrix]]
