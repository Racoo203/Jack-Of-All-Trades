---
title: Sample Complexity
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: seeding
confidence: 0
tags: [reinforcement-learning, theory]
---
## Definition
<!-- UNVERIFIED: check against a dedicated RL-theory reference; not covered in the MA338 slide decks -->
**Sample complexity** measures how many samples (interactions with the environment) an algorithm needs to guarantee a value-function or policy estimate within a specified accuracy $\epsilon$ of the truth, with probability at least $1-\delta$ ("Probably Approximately Correct", PAC). Two related but distinct notions appear in the literature and are worth distinguishing:

- **Sample complexity of a value estimate** (batch/statistical sense): how many i.i.d. samples of a fixed policy are needed to estimate $v_\pi(s)$ to within $\epsilon$ — a question of statistical estimation, answered by concentration inequalities (Hoeffding, Bernstein).
- **[[Sample Complexity of Exploration|Sample complexity of exploration]]** (online/PAC-MDP sense): how many *time steps* an online learning algorithm can take a non-$\epsilon$-optimal action before its policy is guaranteed $\epsilon$-optimal with probability $1-\delta$ — the standard PAC-MDP framework of Kakade (2003) and Strehl, Li & Littman (2009).

## Properties
### Hoeffding-based bound for value estimation
For a bounded reward-return in $[0,R_{\max}]$, averaging $n$ i.i.d. samples of $G_t$ gives, by Hoeffding's inequality,
$$\Pr\left[|\hat v_\pi(s) - v_\pi(s)| > \epsilon\right] \le 2\exp\left(-\frac{2n\epsilon^2}{R_{\max}^2}\right),$$
so $n = O\!\left(\frac{R_{\max}^2}{\epsilon^2}\ln\frac{1}{\delta}\right)$ samples suffice for $\epsilon$-accuracy with confidence $1-\delta$ — the same $1/\epsilon^2$ scaling underlying [[Rate of Convergence|Monte Carlo's $O(1/\sqrt n)$ rate]].

### PAC-MDP sample complexity of exploration
For tabular MDPs, algorithms such as [[Algorithms/R-MAX|R-MAX]] and [[Algorithms/Model-based Interval Estimation (MBIE)|MBIE]] guarantee sample complexity polynomial in $S$ (states), $A$ (actions), the horizon or $1/(1-\gamma)$, and $1/\epsilon$ — the central PAC-MDP result is that a small number of "mistake" steps (where the current policy is not yet $\epsilon$-optimal) suffices before near-optimal behaviour is reached almost everywhere, in contrast to guaranteeing this at *every* step (which regret bounds effectively do).

## See also
[[Sample Complexity of Exploration]], [[Mean-square Sample Complexity]], [[Regret Analysis]], [[Algorithms/R-MAX]], [[Algorithms/Model-based Interval Estimation (MBIE)|MBIE]]
