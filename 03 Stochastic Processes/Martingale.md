---
title: Martingale
domain: Stochastic Processes
course: Stochastic Processes
unit: Foundations & Random Walks
level: MSc
status: seeding
confidence: 0
tags: [seeding]
---
## Definition
A [[Stochastic Process|stochastic process]] $\{X_t, t = 0, 1, \dots\}$ is a martingale if, for $t = 0, 1, \dots$,
1. $E[|X_t|] < \infty$, and
2. $E[X_{t+1} \mid X_0, X_1, \dots, X_t] = X_t$.

## Properties
### "Fair game" interpretation
If $X_t$ is thought of as a player's fortune at time $t$ in a game played repeatedly, the second condition states that, given the entire history of play, the expected fortune after playing one more round equals the fortune before playing it. A martingale therefore captures the notion of a game being *fair*: on average, a player neither gains nor loses by continuing to play. (This intuition also motivates related concepts such as the [[Optional stopping theorem|optional stopping theorem]] and [[Stopping time|stopping times]], which formalize when this "fairness" is preserved even at random — not just fixed — times.)

Although motivated by games of chance, martingale theory has applications far beyond this context, including in mathematical finance (e.g. arbitrage-free pricing) and in the analysis of other stochastic processes.

### Examples of martingales
A [[Geometric Brownian Motion|geometric Brownian motion]] with drift $\mu = 0$ is a continuous-time martingale (as well as a standard [[Brownian motion]]).

## See also
- [[Stopping time]]
- [[Optional stopping theorem]]
- [[Brownian motion]]
- [[Geometric Brownian Motion]]
