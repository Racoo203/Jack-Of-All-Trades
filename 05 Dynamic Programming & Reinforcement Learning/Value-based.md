---
title: Value-based
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: drafted
confidence: 0
tags: [reinforcement-learning, foundations]
---
## Definition
A **value-based** method solves an RL problem *indirectly*: it estimates a [[State value function|state]] or [[Action value function|action]] value function ($v_\pi$ or $q_\pi$, approaching $v_*$ or $q_*$), and derives a policy from it by acting greedily — $\pi(s) = \arg\max_a q(s,a)$. The policy itself is not represented explicitly; it is implicit in the value function. [[Dynamic programming]], [[Monte Carlo Learning]], [[Temporal-Difference Learning]] (SARSA, Q-learning) are all value-based.

This contrasts with [[Policy-based]] methods, which parametrise and optimise the policy directly without necessarily computing a value function.

## Properties
### Why value-based works
Once the optimal value function ($v_*$ or $q_*$) is known, finding the optimal policy is easy: act greedily with respect to it (one-step lookahead for $v_*$, direct $\arg\max$ for $q_*$ — no model needed in the latter case). This is the organising idea behind essentially every tabular method in Part I of the module (see the "Key idea" in [[Dynamic programming]]).

### Limitations
- Requires the value function to be representable/learnable to useful accuracy; with [[Nonlinear Functional Approximation|function approximation]], value-based methods are exposed to the Deadly Triad (bootstrapping + approximation + off-policy) and can diverge.
- Deterministic greedy policies derived from a value function struggle in genuinely stochastic-optimal-policy settings (e.g. rock–paper–scissors variants, partially observable environments) — see [[Deterministic & Stochastic policies]].
- Action selection via $\arg\max_a q(s,a)$ does not scale naturally to continuous or high-dimensional action spaces, unlike policy-based methods.

## See also
[[Policy-based]], [[State value function]], [[Action value function]], [[Dynamic programming]], [[Temporal-Difference Learning]]
