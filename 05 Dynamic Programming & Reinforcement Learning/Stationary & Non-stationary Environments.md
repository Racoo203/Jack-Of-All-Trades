---
title: Stationary & Non-stationary Environments
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: drafted
confidence: 0
tags: [reinforcement-learning, foundations]
---
## Definition
An RL problem is **stationary** if the true underlying values — the action-value function $q_*(a)$ in a bandit, or the dynamics $p(s',r\mid s,a)$ in an MDP — do not change over time. It is **non-stationary** if these true values *do* change over time (e.g. reward probabilities drifting).

## Properties
### Non-stationarity is the common case
Most problems studied in this module fall into the non-stationary category. In such cases it makes sense to weight recent rewards more heavily than long-past ones. The standard tool is a **constant step-size** $\alpha \in (0,1]$ in the incremental update:
$$Q_{n+1} = Q_n + \alpha[R_n - Q_n],$$
which can be shown (unrolling the recursion) to equal
$$Q_{n+1} = (1-\alpha)^nQ_1 + \sum_{i=1}^n \alpha(1-\alpha)^{n-i}R_i, \qquad (1-\alpha)^n + \sum_{i=1}^n\alpha(1-\alpha)^{n-i}=1,$$
i.e. an **exponentially recency-weighted average**: the weight on $R_i$ decays geometrically in $n-i$ (how long ago it was observed), since $1-\alpha \le 1$.

### Convergence conditions on the step size
Let $\alpha_n(a)$ be the step size used after the $n$-th selection of action $a$. A classical stochastic-approximation result states: if $\sum_{n=1}^\infty \alpha_n(a) = \infty$ and $\sum_{n=1}^\infty \alpha_n(a)^2 < \infty$, then $Q_n \to q_*(a)$ with probability 1.
- The first condition ensures the steps are large enough to eventually overcome any initial conditions or fluctuations.
- The second ensures the steps eventually become small enough for convergence.
- The sample-average choice $\alpha_n(a) = 1/n$ satisfies both — hence sample-averaging converges — but a **constant** $\alpha$ does *not* satisfy the second condition, so constant step-size estimates never fully converge; they keep adapting (which is exactly the desired behaviour in a genuinely non-stationary environment, but means the estimate remains permanently biased by its initial value, see [[Multi-armed bandits]]).
- Variable step sizes are uncommon in RL in general (they adapt poorly to non-stationary cases, which are the norm), though they appear naturally in some other domains (e.g. certain stochastic-approximation problems in finance).

## Examples
A market-share estimation problem where consumer preferences genuinely drift over time is a canonical non-stationary bandit: sample-averaging (which weights all past observations equally) is the wrong tool, since it becomes increasingly insensitive to recent changes as $n$ grows.

## See also
[[Multi-armed bandits]], [[Stationary & Non-stationary Policies]], [[Asymptotic Convergence]], [[Rate of Convergence]]
