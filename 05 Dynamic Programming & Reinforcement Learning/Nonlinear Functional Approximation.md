---
title: Nonlinear Functional Approximation
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: drafted
confidence: 0
tags: [reinforcement-learning, function-approximation]
---
## Definition
Nonlinear function approximation drops the linearity assumption of [[Linear MDPs & Linear Functional Approximation|linear FA]]: $v(s,w)$ (or $q(s,a,w)$) can be any differentiable, non-linear parametric function of $w$ — most importantly, neural networks (see [[Deep Reinforcement Learning]]). It buys much richer representational power (features no longer need to be hand-designed to be linearly related to the value function) at the cost of the strong convergence guarantees linear FA enjoys.

## Properties
### The Deadly Triad
Algorithms combining all three of the following can **diverge**:
1. **Bootstrapping** — updates depend on existing estimates (e.g. $v(S_{t+1},w)$), not purely on rewards/returns.
2. **Function approximation** — value functions represented approximately rather than in a table.
3. **Off-policy learning** — trajectories sampled from a policy different from the one being evaluated/improved (e.g. Q-learning's implicit greedy target vs. an $\epsilon$-greedy behaviour policy).

This combination is the **Deadly Triad**. Crucially, **Deep Q-learning satisfies all three simultaneously** by construction (it bootstraps via $\max_aQ(s',a,w)$, uses a neural network, and is off-policy) — which is exactly why naively combining Q-learning with a neural network is unstable, and why [[Algorithms/Deep Q-Network|DQN]]'s specific engineering (experience replay, target networks) exists.

### A worked divergence example (linear approximation, off-policy)
Even *linear* approximation can diverge off-policy. Consider a semi-gradient TD(0) off-policy update with importance-sampling ratio $\rho_t=\pi(A_t\mid S_t)/b(A_t\mid S_t)$:
$$w_{t+1}=w_t-\alpha_t\rho_t\left[R_{t+1}+\gamma v(S_{t+1},w_t)-v(S_t,w_t)\right]\nabla v(S_t,w_t).$$
On a minimal two-state chain where the only available action from the first state makes $\rho_t=1$ (both target and behaviour policy assign probability 1), a feature choice with $v(s,w_t)=w_t$, $v(s',w_t)=2w_t$ gives
$$w_{t+1} = w_t+\alpha_t\left[0+\gamma(2w_t)-w_t\right]\cdot 1 = w_t+\alpha_t(2\gamma-1)w_t.$$
For $w_t>0$ and $\gamma>\tfrac12$: $w_t\to\infty$ — **divergence**, despite linear approximation and $\rho_t=1$ throughout. (Compare the *on-policy*, constant-step-size analogue, which is stable: $w_{t+1}=w_t+\alpha[2\gamma-3]w_t$, and $-1\le 2\gamma-3<0$ for all $\gamma\in[0,1]$, so $w_t\to 0$.)

### Alternative update rules
The **Bellman residual gradient** update targets the *square* of the TD error directly, minimising $[r_{t+1}+\gamma v(s_{t+1},w_t)-v(s_t,w_t)]^2$:
$$w_{t+1} = w_t + \alpha\left[r_{t+1}+\gamma v(s_{t+1},w_t)-v(s_t,w_t)\right]\nabla\left[v(s_t,w_t)-\gamma v(s'_{t+1},w_t)\right].$$
This acts as a smoothing procedure rather than a pure prediction method, generally performs *worse* than ordinary semi-gradient TD, and requires an **independent** second sample $s'_{t+1}$ (potentially different from $s_{t+1}$), which rules out fully online use. Batch methods and experience replay (see [[Deep Reinforcement Learning]]) are the alternatives actually used in practice.

### Convergence facts by combination
- MC with **nonlinear** approximation always converges — but possibly only to a *local* optimum.
- MC with **linear** approximation converges to the *global* optimum $w_{MC}$.
- TD(0) with **linear** approximation converges to $w_{TD}\ne w_{MC}$ in general (biased but typically faster/lower-error — see [[Linear MDPs & Linear Functional Approximation]]).
- Off-policy semi-gradient TD(0), even under linear approximation, **can diverge** (worked example above).

## See also
[[Linear MDPs & Linear Functional Approximation]], [[Deep Reinforcement Learning]], [[Algorithms/Deep Q-Network]], [[Algorithms/Q-learning]], [[On-policy & Off-policy]]
