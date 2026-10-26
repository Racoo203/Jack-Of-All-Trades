---
title: Rate of Convergence
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: drafted
confidence: 0
tags: [reinforcement-learning, convergence, theory]
---
## Definition
While [[Asymptotic Convergence]] asks *whether* an estimator eventually reaches its target, **rate of convergence** asks *how quickly*: how the estimation error (e.g. $|Q_n(a)-q_*(a)|$, or RMS value-function error) shrinks as a function of the number of samples/updates $n$. This is what [[Performance Evaluation]]'s empirical learning curves are measuring when comparing algorithms at fixed sample budgets.

## Properties
### Sample-average bandit estimation: $O(1/\sqrt{n})$
For i.i.d. bounded (or sub-Gaussian) rewards, the sample-average estimator $Q_n(a)$ has standard deviation $O(1/\sqrt{N_n(a)})$ around $q_*(a)$ by the Central Limit Theorem — the canonical "square-root" rate for Monte Carlo-style averaging that recurs throughout statistics.

### n-step TD: an intermediate $n$ is empirically fastest
On the 19-state random-walk benchmark, neither TD(0) ($n=1$) nor MC ($n=\infty$) achieves the lowest RMS error for a fixed number of episodes; intermediate values of $n$ (and, for eligibility-trace methods, intermediate $\lambda$) converge fastest. This is a genuinely empirical claim documented via the learning-curve comparisons referenced in [[Performance Evaluation]] — there is no closed-form rate derived in the module's slides for the general $n$-step case.

### Linear TD(0) vs. linear MC under function approximation
Although TD(0) converges to a different (generally biased) fixed point $w_{TD}\ne w_{MC}$ (see [[Asymptotic Convergence]]), $w_{TD}$ is preferred in practice precisely because it is reached **faster** and with **smaller prediction error** than the unbiased $w_{MC}$ target — a rate/bias trade-off, not merely a convergence-point difference.

### Eligibility traces close the gap between forward and backward views
The trace-decay parameter $\lambda$ interpolates continuously between TD(0)'s fast-but-biased updates and MC's slow-but-unbiased ones; SARSA($\lambda$) has been shown empirically (Mountain Car) to learn **significantly faster** than any single fixed-$n$ n-step SARSA variant, because it effectively blends many $n$-step returns simultaneously rather than committing to one.

## See also
[[Asymptotic Convergence]], [[Performance Evaluation]], [[Algorithms/SARSA(lambda)]], [[Sample Complexity]]
