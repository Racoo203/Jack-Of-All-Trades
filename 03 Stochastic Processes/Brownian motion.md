---
title: Brownian motion
domain: Stochastic Processes
course: Stochastic Processes
unit: Foundations & Random Walks
level: MSc
status: seeding
confidence: 0
tags: [seeding]
---
## Definition
A [[Stochastic Process|stochastic process]] $\{B_t, t \geq 0\}$ is called a (standard) Brownian motion if:
1. $B_0 = 0$, and $B_t$ is continuous as a function of $t$;
2. it has [[Independent Increments|independent increments]]: $B_{t_1}, (B_{t_2} - B_{t_1}), \dots, (B_{t_k} - B_{t_{k-1}})$ are independent random variables, for any $0 < t_1 < t_2 < \dots < t_k$;
3. every increment is normally distributed with mean zero and variance equal to the length of the interval: $B_{t+s} - B_t \sim N(0, s)$ for all $t, s \geq 0$.

## Properties
### Relation to other processes
Brownian motion can be viewed as a continuous-time, continuous-state analogue of the [[Simple Random Walk|simple random walk]] — both are processes built from independent increments, with Brownian motion arising (informally) as a scaling limit of a symmetric random walk as the step size and time increment shrink together.

A standard Brownian motion is also a [[Martingale|martingale]], since $E[|B_t|] < \infty$ and $E[B_{t+s} \mid \mathcal{F}_t] = B_t$ by the independent, zero-mean increments.

### Geometric Brownian motion
Exponentiating a (linearly-drifted) Brownian motion produces [[Geometric Brownian Motion|geometric Brownian motion]], the standard model for asset prices in continuous time.

## See also
- [[Independent Increments]]
- [[Martingale]]
- [[Geometric Brownian Motion]]
- [[Simple Random Walk]]
