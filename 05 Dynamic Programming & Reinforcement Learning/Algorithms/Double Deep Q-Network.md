---
title: Double Deep Q-Network
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
unit: Algorithms
level: MSc
status: drafted
confidence: 0
tags: [reinforcement-learning, deep-rl, algorithms, off-policy]
---
## Definition
Double DQN corrects a specific bias in [[Algorithms/Deep Q-Network|DQN]] caused by using the *same* network to both **select** the greedy next action and **evaluate** its value: $\max_aQ(s',a,w)$ systematically overestimates the true value, because any positive estimation noise in $Q(s',\cdot,w)$ is preferentially selected by the $\max$ operator (a form of the general statistical fact that $\mathbb E[\max_a X_a] \ge \max_a \mathbb E[X_a]$ under noisy estimates $X_a$).

Double DQN decouples selection from evaluation using two parameter vectors, $w$ (online network) and $\hat w$ (a second/target network):
$$l = \left(r + \gamma\, Q\!\left(s', \arg\max_{a'}Q(s',a',w),\ \hat w\right) - Q(s,a,\hat w)\right)^2.$$
The **action is chosen** by the online network $w$, but its **value is evaluated** using the other network $\hat w$ — so overestimation bias in one network is not self-reinforcing, since it would need to be shared by both networks simultaneously to bias the target.

## Properties
### Relation to ordinary DQN
Double DQN reuses exactly the machinery of [[Algorithms/Deep Q-Network|DQN]] (experience replay, periodic synchronisation between online and target parameters) and changes only the *target computation* — a minimal, low-cost modification that empirically reduces overoptimistic value estimates and the resulting policy instability, without altering the network architecture or training loop otherwise.

### Why decoupling removes the bias
If selection and evaluation used the *same* noisy estimate, the action chosen would be biased toward whichever action's noise happened to be largest — and that same noisy estimate would then also be used to *report* the target value, compounding the error. Using an independent (or at least differently-updated) second estimate for evaluation means the action selected by $w$ is unlikely to also be the maximally-noisy action under $\hat w$, so the systematic overestimation largely cancels.

## See also
[[Algorithms/Deep Q-Network]], [[Algorithms/Q-learning]], [[Nonlinear Functional Approximation]], [[Deep Reinforcement Learning]]
