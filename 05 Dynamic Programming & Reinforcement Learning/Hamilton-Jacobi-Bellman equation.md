---
title: Hamilton-Jacobi-Bellman equation
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: seeding
confidence: 0
tags: [reinforcement-learning, optimal-control, theory]
---
## Definition
<!-- UNVERIFIED: check against a dedicated stochastic-control reference (e.g. Fleming & Soner); not covered in the MA338 slide decks -->
The Hamilton–Jacobi–Bellman (HJB) equation is the **continuous-time** analogue of the discrete [[Bellman equation]]: it is the partial differential equation the optimal value function $V(x,t)$ of a continuous-time control problem must satisfy. For a controlled diffusion $dx_t = f(x_t,u_t)dt+\sigma(x_t,u_t)dW_t$ with running cost $c(x,u)$ and terminal cost $g(x)$, the value function
$$V(x,t) = \min_{u(\cdot)}\ \mathbb E\left[\int_t^Tc(x_s,u_s)\,ds+g(x_T)\ \middle|\ x_t=x\right]$$
satisfies
$$-\frac{\partial V}{\partial t} = \min_u\left[c(x,u)+f(x,u)^\top\nabla_xV + \frac{1}{2}\mathrm{tr}\left(\sigma\sigma^\top\nabla_x^2V\right)\right], \qquad V(x,T)=g(x).$$

## Properties
### Derivation intuition: the continuous limit of dynamic programming
Discretising time into steps of size $\Delta t$, the discrete Bellman equation $V(x,t)=\min_u\left[c(x,u)\Delta t+\mathbb E[V(x+\Delta x,t+\Delta t)]\right]$ becomes, after a first/second-order Taylor expansion of $V$ in $\Delta x,\Delta t$ and taking $\Delta t\to 0$, exactly the HJB PDE above — the drift term $f(x,u)^\top\nabla_xV$ comes from the first-order (deterministic) part of the state change, and the diffusion term $\frac{1}{2}\mathrm{tr}(\sigma\sigma^\top\nabla_x^2V)$ from the Itô correction due to the stochastic (Brownian) part. This mirrors exactly how [[Discount factor|the discrete Bellman equation]] arises from the one-step recursion $G_t=R_{t+1}+\gamma G_{t+1}$, just taken to a continuum limit.

### Special case: linear-quadratic-Gaussian control
When $f$ is linear and $c$ is quadratic (the continuous-time analogue of [[Linear-quadratic problems]]), the HJB equation again admits a closed-form quadratic solution $V(x,t)=x^\top P(t)x$, with $P(t)$ satisfying a continuous-time (differential, rather than discrete recursive) Riccati equation — the direct continuous-time counterpart of the discrete Riccati recursion in [[Linear-quadratic regulator (LQR)]].

### Relation to RL
The HJB equation underlies **continuous-time RL** and is the theoretical bridge between classical stochastic optimal control and modern RL for continuous-control problems (e.g. robotics, quantitative finance — portfolio optimisation problems are frequently posed in HJB form). Numerically solving HJB directly suffers the same curse of dimensionality as discrete DP; RL-style function approximation (see [[Nonlinear Functional Approximation]]) is one route to approximate HJB solutions in high dimensions without discretising the full state space.

## See also
[[Linear-quadratic regulator (LQR)]], [[Linear-quadratic problems]], [[Bellman equation]], [[Dynamic programming]]
