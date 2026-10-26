---
title: "Linear-quadratic regulator (LQR)"
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: seeding
confidence: 0
tags: [reinforcement-learning, optimal-control, theory]
---
## Definition
<!-- UNVERIFIED: check against a dedicated optimal-control/LQR reference; not covered in the MA338 slide decks -->
The Linear-Quadratic Regulator is the closed-form optimal policy for a [[Linear-quadratic problems|linear-quadratic control problem]]: $x_{t+1}=Ax_t+Bu_t+w_t$, cost $\sum_t(x_t^\top Qx_t+u_t^\top Ru_t)$. The optimal control is a **linear state-feedback law**:
$$u_t^* = -K_tx_t,$$
for a time-varying gain matrix $K_t$ computed from a backward Riccati recursion.

## Properties
### Riccati recursion (derivation sketch)
Assume the optimal cost-to-go at stage $t+1$ is quadratic: $v_{t+1}(x) = x^\top P_{t+1}x$. Substituting into the Bellman equation $v_t(x) = \min_u\left[x^\top Qx+u^\top Ru+\mathbb E[(Ax+Bu+w)^\top P_{t+1}(Ax+Bu+w)]\right]$ (dropping the noise term, which contributes only an additive constant independent of $u$ under zero-mean $w_t$) and differentiating with respect to $u$:
$$\frac{\partial}{\partial u}\left[u^\top Ru + (Ax+Bu)^\top P_{t+1}(Ax+Bu)\right] = 2Ru+2B^\top P_{t+1}(Ax+Bu) = 0$$
$$\Rightarrow u_t^* = -\underbrace{(R+B^\top P_{t+1}B)^{-1}B^\top P_{t+1}A}_{K_t}x_t.$$
Substituting $u_t^*$ back confirms $v_t(x)=x^\top P_tx$ is quadratic too, with the backward **discrete-time Riccati recursion**
$$P_t = Q + A^\top P_{t+1}A - A^\top P_{t+1}B(R+B^\top P_{t+1}B)^{-1}B^\top P_{t+1}A, \qquad P_T = Q_T.$$
This closes the induction: the quadratic-value-function ansatz is self-consistent at every stage, which is exactly why LQ problems admit an exact closed-form solution where general MDPs do not.

### Infinite-horizon LQR
As $T\to\infty$ (with a stabilisable/detectable system), $P_t$ converges to a constant $P^\infty$ solving the **Algebraic Riccati Equation** $P=Q+A^\top PA-A^\top PB(R+B^\top PB)^{-1}B^\top PA$, giving a single time-invariant gain $K^\infty$ and a **stationary** optimal policy $u^*=-K^\infty x$ — directly paralleling [[Stationary & Non-stationary Policies|why infinite-horizon MDPs admit stationary optimal policies]] while finite-horizon ones generally require time-varying ones.

### Relation to RL
LQR is the standard benchmark/special case for testing RL algorithms in continuous control, because its optimal policy and value function are known in closed form — allowing exact evaluation of an RL algorithm's convergence rate and asymptotic bias against ground truth, unlike most RL benchmarks where the optimum itself is unknown.

## See also
[[Linear-quadratic problems]], [[Hamilton-Jacobi-Bellman equation]], [[Multi-agent LQ]], [[Value Iteration Equation]]
