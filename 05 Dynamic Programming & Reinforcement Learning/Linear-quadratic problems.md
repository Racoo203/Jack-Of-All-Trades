---
title: Linear-quadratic problems
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: seeding
confidence: 0
tags: [reinforcement-learning, optimal-control, theory]
---
## Definition
<!-- UNVERIFIED: check against a dedicated optimal-control/LQR reference (e.g. Bertsekas, "Dynamic Programming and Optimal Control"); not covered in the MA338 slide decks -->
A **linear-quadratic (LQ) problem** is a continuous-state, continuous-action optimal control problem with **linear** state transitions and a **quadratic** cost (equivalently, negative reward). The discrete-time formulation: state $x_t\in\mathbb R^n$, control $u_t\in\mathbb R^m$,
$$x_{t+1} = Ax_t + Bu_t + w_t,$$
with $w_t$ i.i.d. (often Gaussian) noise, and cost to minimise over a horizon $T$
$$J = \mathbb E\left[\sum_{t=0}^{T-1}\left(x_t^\top Q x_t + u_t^\top R u_t\right) + x_T^\top Q_T x_T\right],$$
with $Q,Q_T\succeq 0$ and $R\succ 0$ symmetric matrices. LQ problems are the continuous-state analogue of a finite [[Markov Decision Process]]: solvable exactly by [[Dynamic programming|dynamic programming]]/backward induction, but where the linear-quadratic structure yields a **closed-form** optimal policy — the [[Linear-quadratic regulator (LQR)|LQR]] — rather than requiring an iterative numerical solve over a discretised state space.

## Properties
### Why the LQ structure is special
Because the transition is linear and the cost is quadratic, the optimal value function at every stage remains exactly quadratic in the state: $v_t(x) = x^\top P_t x + \text{const}$, for some positive semi-definite matrix $P_t$ computed by a backward **Riccati recursion**. This is a rare case in RL/control where dynamic programming's value function has a closed algebraic form rather than needing tabulation or approximation — see [[Linear-quadratic regulator (LQR)]] for the recursion itself.

### Relation to the Bellman equation
The LQ Bellman equation is structurally identical to the discrete [[Bellman equation]] — $v_t(x) = \min_u\left[x^\top Qx + u^\top Ru + \mathbb E[v_{t+1}(Ax+Bu+w)]\right]$ — with the $\max$ of the RL convention replaced by a $\min$ (cost minimisation rather than reward maximisation), and continuous $x,u$ in place of discrete $s,a$. The continuous-time limit of this recursion is the [[Hamilton-Jacobi-Bellman equation]].

## See also
[[Linear-quadratic regulator (LQR)]], [[Hamilton-Jacobi-Bellman equation]], [[Multi-agent LQ]], [[Dynamic programming]], [[Bellman equation]]
