---
title: Deterministic & Stochastic policies
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: drafted
confidence: 0
tags: [reinforcement-learning, foundations]
---
## Definition
A **policy** $\pi$ is a function that takes a state and returns the probability of selecting each possible action. If the agent follows $\pi$ at time $t$, then $\pi(a\mid s)$ is the probability of $A_t=a$ given $S_t=s$. This is the general (**stochastic**) case.

A **deterministic policy** is the special case where, for each state $s$, one action is taken with probability 1: $\pi(s)$ denotes that single action directly (an abuse of notation reusing $\pi$ for both the distribution and, when deterministic, the action itself).

## Properties
### An optimal deterministic policy always exists in finite MDPs
For any finite MDP, there exists a policy $\pi^*$ that is better than or equal to every other policy at every state ($v_{\pi^*}(s) \ge v_\pi(s)\ \forall s,\pi$), and it can always be chosen to be deterministic: $\pi^*(s) = \arg\max_a q^*(s,a)$. This is why [[Dynamic programming]], [[Monte Carlo Learning]], and tabular [[Temporal-Difference Learning]] all target a deterministic greedy policy as their end goal.

### When stochastic policies are genuinely necessary
Despite the above, [[Policy-based|policy-gradient methods]] deliberately parametrise *stochastic* policies (e.g. softmax over action preferences, or a Gaussian over continuous actions). This is not merely for exploration during learning — it is because:
- Real problems are frequently **not fully observable**, especially once [[Nonlinear Functional Approximation|function approximation]] collapses distinct underlying states into the same represented state; in such cases the *optimal* policy given the available information may genuinely need to be stochastic.
- In adversarial/game settings (e.g. rock-paper-scissors-lizard-Spock), a deterministic policy is always exploitable by the opponent; the game-theoretically optimal policy is a specific randomisation.
- All the policy evaluation/improvement machinery developed for deterministic policies in [[Dynamic programming]] and [[Monte Carlo Learning]] carries over to stochastic policies without modification (the policy improvement theorem holds for stochastic $\pi,\pi'$ as stated).

## See also
[[Policy-based]], [[Value-based]], [[Dynamic programming]], [[Policy Gradient Theorem]], [[Multi-armed bandits]]
