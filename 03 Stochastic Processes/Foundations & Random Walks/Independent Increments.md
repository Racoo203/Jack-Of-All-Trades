---
title: Independent Increments
domain: Stochastic Processes
course: Stochastic Processes
unit: Foundations & Random Walks
level: MSc
status: seeding
confidence: 0
tags: [seeding]
---
Independent increments are a property of stochastic processes. Many canonical processes (e.g. [[Poisson Process|the Poisson process]], [[Brownian motion]]) have this property by definition or construction.

## Definition
Let $\{X_t : t \in T\}$ be a [[Stochastic Process|stochastic process]]. It has independent increments if, for any $t_1 < t_2 < \dots < t_n$ with $t_1, \dots, t_n \in T$,
$$
X_{t_1},\ (X_{t_2} - X_{t_1}),\ \dots,\ (X_{t_n} - X_{t_{n-1}})
$$
are [[Stochastic Independence|independent]] [[Random Variable|random variables]].

## Examples
Under the efficient market hypothesis, the process of log-returns $X_t = \log S_t$ of a stock price $S_t$ is assumed to have independent increments.

## See also
- [[Stochastic Process]]
- [[Stationary Increments]]
- [[Poisson Process]]
- [[Brownian motion]]
