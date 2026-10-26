---
title: Action value function
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: drafted
confidence: 0
tags: [reinforcement-learning, mdp, value-functions]
---
## Definition
The action-value function of taking action $a$ in state $s$ under policy $\pi$, denoted $q_\pi(s,a)$, is the expected [[Discount factor|return]] starting from $s$, taking action $a$, and thereafter following $\pi$:
$$q_\pi(s,a) := \mathbb E_\pi[G_t\mid S_t=s, A_t=a] = \mathbb E_\pi\left[\sum_{k=0}^\infty \gamma^kR_{t+k+1}\,\middle|\, S_t=s,A_t=a\right].$$
The **optimal** action-value function is $q_*(s,a) = \max_\pi q_\pi(s,a)$.

## Properties
### Bellman equation for $q_\pi$
$$q_\pi(s,a) = \mathbb E_\pi[R_{t+1}+\gamma v_\pi(S_{t+1})\mid S_t=s,A_t=a] = \sum_{s',r}p(s',r\mid s,a)\left[r+\gamma\sum_{a'}\pi(a'\mid s')q_\pi(s',a')\right].$$

### Why $q$ matters more than $v$ for control
Under [[Dynamic programming]] with known $p$, $q_\pi(s,a) = \sum_{s',r}p(s',r\mid s,a)[r+\gamma v_\pi(s')]$ can be computed *from* $v_\pi$ directly — but this requires knowing $p$. Once $p$ is unknown ([[Monte Carlo Learning]], [[Temporal-Difference Learning]]), $q_\pi$ must be estimated **directly**, since there is no way to convert a learned $v_\pi$ into an implied policy without a model. This is precisely why model-free control methods (SARSA, Q-learning, MC control) all target $q$ rather than $v$: with $q_*(s,a)$ in hand, the optimal policy follows immediately as $\pi^*(s) = \arg\max_a q_*(s,a)$, with no model needed at all.

### Bellman *optimality* equation
$$q_*(s,a) = \sum_{s',r}p(s',r\mid s,a)\left[r+\gamma\max_{a'}q_*(s',a')\right].$$
See [[Bellman equation]] for the full statement (including the $v_*$ version) and its role in deriving [[Dynamic programming|value iteration]].

## Examples
In the SARSA-vs-Q-learning worked example from Lecture 5 (3×2 gridworld with terminal reward $+10$ at node 6), $Q(s,a)$ values are given per state-action pair in a table and updated by hand after a single sampled transition — a canonical exam-style exercise (see the MOC's Exam focus section).

## See also
[[State value function]], [[Bellman equation]], [[Algorithms/SARSA]], [[Algorithms/Q-learning]], [[Markov Decision Process]]
