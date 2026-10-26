---
title: Stationary Increments
domain: Stochastic Processes
course: Stochastic Processes
unit: Foundations & Random Walks
level: MSc
status: seeding
confidence: 0
tags: [seeding]
---
## Definition
A [[Stochastic Process|stochastic process]] $\{X_t : t \in T\}$ is said to have stationary increments, if for any $s,t \in T$, then $X_t - X_s$ and $X_{t-s}$ have the same probability distribution.

## Example
Assume $S_t$ models a stock price at time $t$. If $X_t = \log S_t$ then we see $X_{t+s} - X_t = \log S_{t+s} - \log S_t = \log (S_{t+s} / S_t)$.  