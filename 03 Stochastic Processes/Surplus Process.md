---
title: Surplus Process
domain: Stochastic Processes
course: Stochastic Processes
unit: Foundations & Random Walks
level: MSc
status: seeding
confidence: 0
tags: [seeding]
---
## Definition
The surplus process $\{U_t, t \geq 0\}$ (also known as the **Cramér–Lundberg model**) models the capital of an insurance company over time as claims of unpredictable size arrive at unpredictable times. Individual claims $X_1, X_2, \dots$ are assumed [[Independent and Identically Distributed (i.i.d)|i.i.d.]], and $\{N_t, t \geq 0\}$ (a [[Counting Process|counting process]], typically a [[Poisson Process|Poisson process]]) denotes the number of claims up to time $t$. The insurer's random surplus at time $t$ is
$$
U_t = u + ct - \sum_{i=1}^{N_t} X_i
$$
where $u$ is the initial capital and $c$ is the (fixed) premium income per unit time.

## Properties
### Purpose
The surplus process is used to assess an insurer's risk of insolvency — e.g. by studying the probability that $U_t$ ever falls below $0$ (ruin), a continuous-state, continuous-time analogue of the discrete [[Gambler's Ruin|gambler's ruin]] problem.

## See also
- [[Counting Process]]
- [[Poisson Process]]
- [[Gambler's Ruin]]
