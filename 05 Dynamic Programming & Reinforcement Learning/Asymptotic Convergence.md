---
title: Asymptotic Convergence
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: drafted
confidence: 0
tags: [reinforcement-learning, bandits, convergence]
---
## Definition
An estimator or algorithm exhibits **asymptotic convergence** if, as the number of updates/samples $n \to \infty$, it approaches the true target value (with probability 1, or in expectation, or in distribution, depending on the mode of convergence stated). This note collects the convergence results that recur throughout the module's tabular and approximate methods, without regard to *how fast* convergence happens (see [[Rate of Convergence]] for that).

## Properties
### Sample-average bandit estimation
By the Law of Large Numbers, $Q_n(a) \to q_*(a)$ almost surely as $N(a)\to\infty$ — see [[Multi-armed bandits]].

### Robbins–Monro conditions (general stochastic approximation)
For the general incremental update $Q_{n+1} = Q_n + \alpha_n[R_n - Q_n]$, convergence to $q_*$ with probability 1 holds iff
$$\sum_{n=1}^\infty \alpha_n = \infty \quad\text{and}\quad \sum_{n=1}^\infty \alpha_n^2 < \infty.$$
$\alpha_n = 1/n$ satisfies both (sample-average case); constant $\alpha$ satisfies neither, so does not converge in the strict sense (though it remains useful, indeed preferable, in non-stationary settings — see [[Stationary & Non-stationary Environments]]).

### Iterative Policy Evaluation (Dynamic Programming)
The Bellman-equation update $v_{k+1}(s) = \sum_a\pi(a\mid s)\sum_{s',r}p(s',r\mid s,a)[r+\gamma v_k(s')]$ has $v_\pi$ as its unique fixed point, and $\{v_k\}\to v_\pi$ as $k\to\infty$, provided $\gamma<1$ or the task is episodic with $T<\infty$ (see [[Dynamic programming]]).

### Monte Carlo and TD(0) under linear function approximation
Under linear approximation $v(s,w)=x(s)^\top w$: MC (via the update $w_{t+1}-w_t = -\alpha_t\mathbb E_\pi[(G_t-v(S_t,w_t))^2]$) converges to the unique fixed point $w_{MC}=\mathbb E[x_tx_t^\top]^{-1}\mathbb E[G_tx_t]$ — the **global optimum** of the mean-squared prediction error. TD(0) converges to a *different* fixed point $w_{TD}=\mathbb E[x_t(x_t-\gamma x_{t+1})^\top]^{-1}\mathbb E[R_{t+1}x_t]$, which coincides with $w_{MC}$ only when $\gamma=0$; in general $w_{TD}$ is close to but not exactly the global optimum, yet is preferred in practice for its smaller prediction error and faster convergence (see [[Deep Reinforcement Learning]] for the full derivation and proof sketch).

### Where convergence breaks down
Nonlinear (neural-network) MC always converges, but only to a *local* optimum. Semi-gradient off-policy TD(0) under linear approximation can **diverge** — the Deadly Triad of bootstrapping + function approximation + off-policy learning (see [[Nonlinear Functional Approximation]] and [[Deep Reinforcement Learning]] for the explicit divergence example).

## See also
[[Rate of Convergence]], [[Stationary & Non-stationary Environments]], [[Deep Reinforcement Learning]], [[Nonlinear Functional Approximation]]
