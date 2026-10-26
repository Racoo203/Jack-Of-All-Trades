---
title: State value function
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: drafted
confidence: 0
tags: [reinforcement-learning, mdp, value-functions]
---
## Definition
The state-value function of a state $s$ under policy $\pi$, denoted $v_\pi(s)$, is the expected [[Discount factor|return]] starting in $s$ and following $\pi$ thereafter:
$$v_\pi(s) := \mathbb E_\pi[G_t \mid S_t = s] = \mathbb E_\pi\left[\sum_{k=0}^\infty \gamma^k R_{t+k+1} \,\middle|\, S_t=s\right].$$
The **optimal** state-value function is the pointwise maximum over all policies: $v_*(s) = \max_\pi v_\pi(s)$.

## Properties
### Bellman equation for $v_\pi$
$v_\pi$ decomposes into immediate reward plus discounted value of the successor state:
$$v_\pi(s) = \mathbb E_\pi[R_{t+1}+\gamma v_\pi(S_{t+1})\mid S_t=s] = \sum_a \pi(a\mid s)\sum_{s',r}p(s',r\mid s,a)\left[r+\gamma v_\pi(s')\right].$$
This is the [[Bellman equation]] for $v_\pi$ — see that note for the full derivation and the optimality version.

### Relation to the action-value function
$$v_\pi(s) = \sum_a \pi(a\mid s)\, q_\pi(s,a), \qquad v_*(s) = \max_{a\in\mathcal A(s)} q_{\pi^*}(s,a).$$
So $v_\pi$ is precisely the $\pi$-weighted average of $q_\pi$ over actions — this identity is what lets [[Dynamic programming|policy improvement]] go back and forth between the two representations.

### Uniqueness
In a finite MDP, the Bellman equation for $v_\pi$ has a **unique** solution whenever $\gamma<1$, or the task is episodic with finite $T$ — see [[Infinite & Finite Time Horizon]]. Under full knowledge of $p$ and $\pi$, this is a linear system with $|\mathcal S|$ equations and $|\mathcal S|$ unknowns; in practice it is solved iteratively rather than directly (see [[Dynamic programming]]).

## Examples
In the special-states Gridworld (Lecture 2) under the equiprobable random policy with $\gamma=0.9$, $v_\pi$ is highest near states A and B (which yield $+10$/$+5$ on leaving) and lowest near the grid edges (where actions leaving the grid incur $-1$ and no movement).

## See also
[[Action value function]], [[Bellman equation]], [[Markov Decision Process]], [[Discount factor]], [[Value Iteration Equation]]
