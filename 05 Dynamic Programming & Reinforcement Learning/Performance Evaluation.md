---
title: Performance Evaluation
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: drafted
confidence: 0
tags: [reinforcement-learning, foundations]
---
## Definition
Performance evaluation in RL concerns how the quality of an estimate (a value function, or a policy) is measured against ground truth, and how learning curves are compared across algorithms/hyperparameters. Two recurring evaluation devices appear throughout the module:

1. **Prediction error metrics**, e.g. root-mean-square (RMS) error between an estimated value function and the true one, averaged across states and independent runs — used to compare [[Temporal-Difference Learning|TD]] vs. [[Monte Carlo Learning|MC]], or different values of $n$ in n-step methods and $\lambda$ in eligibility-trace methods.
2. **Cumulative/average reward curves**, e.g. total reward per episode (averaged across many independent runs) as a function of training episodes — used to compare control algorithms (SARSA vs. Q-learning, REINFORCE vs. REINFORCE-with-baseline).

## Properties
### On-policy vs off-policy objectives for value-function fitting
When fitting a parametric value function (see [[Linear MDPs & Linear Functional Approximation]]), performance is measured by the sampled Mean Square Error on the *visited* trajectory:
$$J(w) = \sum_k \left[v_\pi(x_k) - \hat v(\tilde x_k, w)\right]^2.$$
This works cleanly for **on-policy prediction**. The **off-policy** case is materially harder — mismatched sampling distributions increase divergence risk — and is generally avoided unless explicitly required (see [[Nonlinear Functional Approximation]] on the Deadly Triad).

### Empirical comparisons in this module
- **n-step TD vs. TD(0) vs. MC** on a 19-state random walk: RMS error, averaged over the first 10 episodes and 100 repetitions, as a function of step size $\alpha$, for various $n$. The consistent finding: *intermediate* $n$ (neither $n=1$ nor $n=\infty$) performs best — the empirical justification for n-step methods existing at all.
- **SARSA($\lambda$) vs. n-step SARSA** on Mountain Car: eligibility-trace methods with intermediate $\lambda$ learn faster than any single fixed $n$-step method.
- **Deep SARSA on Atari** (Seaquest, Breakout): average-score learning curves exhibiting drastic performance *dips* even while trending toward convergence — an empirical illustration of the instability introduced by function approximation (the Deadly Triad), motivating experience replay/target networks in [[Deep Reinforcement Learning|DQN]].

## See also
[[Asymptotic Convergence]], [[Rate of Convergence]], [[Regret Analysis]], [[Sample Complexity]]
