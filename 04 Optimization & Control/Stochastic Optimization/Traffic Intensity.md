---
title: "Traffic Intensity"
domain: "Optimization & Control"
course: "Stochastic Optimization"
level: BSc
status: drafted
confidence: 0
tags: [queueing-theory, stochastic-optimization]
---
## Definition
For a [[Queueing System]] with arrival rate $\lambda$ and per-server service rate $\mu$, the **traffic intensity** (or offered load) is
$$
\sigma = \frac{\lambda}{\mu}.
$$
For a single-server system this doubles as the long-run **server utilization**: the fraction of time the server is busy, $\rho = \sigma$. For an $s$-server system, utilization per server is $\rho = \sigma/s = \lambda/(s\mu)$.

## Properties
### Stability requires $\sigma < 1$ (or $\rho < 1$) for infinite-capacity systems
When the system has infinite capacity (no blocking), a steady-state distribution exists only if the traffic intensity per server is strictly less than 1 — otherwise the queue grows without bound. Finite-capacity systems (see [[M-M-1-N Queue]], [[M-M-s-N Queue]]) always have a well-defined steady state regardless of $\sigma$, since customers are blocked/turned away rather than queuing indefinitely.

### Utilization with blocking
For a finite-capacity single-server system, the *effective* fraction of time the server is busy is $\rho = \hat\lambda/\mu = \sigma(1-\sigma^N P_0)$, using the [[M-M-1-N Queue|effective arrival rate]] $\hat\lambda$ rather than the nominal $\lambda$, since not every arriving customer actually enters the system.

## See also
[[Queueing System]], [[Kendall's Notation]], [[Little's Law]], [[M-M-1 Queue]], [[M-M-s Queue]]
