---
title: Differential Sharpe ratio
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: seeding
confidence: 0
tags: [reinforcement-learning, finance, theory]
---
## Definition
<!-- UNVERIFIED: check against Moody & Saffell (2001), "Learning to Trade via Direct Reinforcement"; not covered in the MA338 slide decks — belongs to Raúl's own RL-in-finance reading rather than the taught module -->
The differential Sharpe ratio is an **online, recursively-updatable** approximation to the Sharpe ratio, designed so that a trading/portfolio RL agent can receive a well-defined *per-step* reward proportional to risk-adjusted return, rather than only being able to evaluate risk-adjustment retrospectively over a completed trading period (the ordinary Sharpe ratio requires a return-series mean and standard deviation, both batch statistics).

## Properties
### Why the ordinary Sharpe ratio is unsuitable as a per-step RL reward
The Sharpe ratio $S=\bar R/\sigma_R$ is a ratio of a sample mean to a sample standard deviation over a *window* of returns — it is not naturally decomposable into a sum of per-step contributions the way [[Reward function|RL rewards]] must be (since RL maximises $\sum_t\gamma^kR_{t+k+1}$, an additive quantity, not a mean/variance ratio). Directly using end-of-episode Sharpe ratio as a sparse terminal reward discards the step-by-step [[Reward function|reward-shaping]] information that makes credit assignment tractable for [[Temporal-Difference Learning|TD-style]] or fine-grained policy-gradient methods.

### The differential/exponential-moving construction
Moody & Saffell (2001) derive an incremental update: maintain exponentially-weighted moving estimates of the first and second moments of returns, $A_t$ and $B_t$ (updated each step via $A_t=A_{t-1}+\eta\Delta A_t$, $B_t=B_{t-1}+\eta\Delta B_t$ for a decay/adaptation rate $\eta$), and define the **differential Sharpe ratio** as the first-order Taylor expansion of the Sharpe ratio's sensitivity to the incremental change in these moving moments at step $t$:
$$D_t \approx \frac{B_{t-1}\Delta A_t - \tfrac12 A_{t-1}\Delta B_t}{(B_{t-1}-A_{t-1}^2)^{3/2}}.$$
$D_t$ can be computed at every single time step from purely local, online-updatable statistics, making it usable directly as a per-step RL reward signal — unlike the batch Sharpe ratio.

### Relevance to `investment-automation`
This is the standard risk-adjusted per-step reward used in direct-RL trading agents (the "REINFORCE RL allocation agent" referenced in Raúl's `investment-automation` project), typically paired with an [[Ensemble of Identical Independent Evaluators (EIIE)|EIIE]]-style policy architecture, as an alternative or complement to a batch mean-CVaR objective evaluated only at rebalancing points.

## See also
[[Ensemble of Identical Independent Evaluators (EIIE)]], [[Reward function]], [[Algorithms/REINFORCE]], [[Performance Evaluation]]
