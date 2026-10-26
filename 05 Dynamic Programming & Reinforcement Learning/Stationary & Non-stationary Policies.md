---
title: Stationary & Non-stationary Policies
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: drafted
confidence: 0
tags: [reinforcement-learning, foundations]
---
## Definition
A policy $\pi$ is **stationary** if it does not depend explicitly on the time step $t$: $\pi(a\mid s)$ is the same function whether it is queried at $t=0$ or $t=100$. A policy is **non-stationary** (or time-dependent) if it is indexed by $t$: $\pi_t(a\mid s)$.

## Properties
### Optimal policies in infinite-horizon discounted MDPs are stationary
For an infinite-horizon (or discounted, [[Infinite & Finite Time Horizon]]) MDP with time-homogeneous dynamics $p(s',r\mid s,a)$, there always exists an optimal policy that is stationary and deterministic — because the future looks identical from any given state $s$ regardless of *when* $s$ is visited, so there is never a reason to act differently at the same state at different times. This underlies why value functions $v_\pi(s)$, $q_\pi(s,a)$ in this module are written without a time index: the policy being evaluated is assumed stationary.

### Finite-horizon problems generally require non-stationary policies
In a finite-horizon MDP with a fixed deadline $T$, the *same* state visited with 1 step remaining versus 10 steps remaining can warrant genuinely different optimal actions (e.g. a risk-averse action near the deadline, a more exploratory one early on). The optimal policy is then indexed by remaining time-to-go, i.e. non-stationary — this is exactly the structure exploited by backward induction / finite-horizon dynamic programming.

## See also
[[Infinite & Finite Time Horizon]], [[Deterministic & Stochastic policies]], [[Markov Decision Process]], [[Dynamic programming]]
