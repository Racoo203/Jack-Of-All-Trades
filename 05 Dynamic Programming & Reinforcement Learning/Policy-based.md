---
title: Policy-based
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: drafted
confidence: 0
tags: [reinforcement-learning, foundations, policy-gradient]
---
## Definition
A **policy-based** method parametrises the policy directly, $\pi(a\mid s,\theta) \approx \pi(a\mid s)$ with parameter vector $\theta \in \mathbb{R}^d$, and optimises $\theta$ directly against an objective $J(\theta)$ measuring policy quality (e.g. $J(\theta) = v_{\pi_\theta}(s_0)$), typically via gradient ascent — see the [[Policy Gradient Theorem]]. This is a *direct* approach to control, contrasted with the *indirect* [[Value-based|value-based]] route of estimating $q_\pi$ and acting greedily.

## Properties
### Advantages
- Targets the true objective (the policy) directly rather than as a byproduct of a value function.
- Extends naturally to high-dimensional and continuous action spaces (e.g. a Gaussian policy over $a \in \mathbb{R}$ — see [[Policy Gradient Theorem]]).
- Can represent genuinely **stochastic** optimal policies, which value-based greedy policies cannot (relevant whenever the environment is not fully observable, or in adversarial/game settings, e.g. rock-paper-scissors-lizard-Spock, where the optimal policy is uniform-random).
- Values can be hard to interpret in complex dynamics even when the corresponding policy is comparatively simple and converges quickly (e.g. the gridworld of [[Dynamic programming]], where the optimal *policy* stabilises after 3 iterations while $v_k$ only converges in the limit).

### Disadvantages
- Can converge to local optima (the objective $J(\theta)$ is generally non-convex).
- Can struggle to extract information efficiently from data without an explicit value function to bootstrap from — hence the appeal of hybrid [[Algorithms/Actor-Critic|actor–critic]] methods.

## Examples
[[Algorithms/REINFORCE|REINFORCE]] is the canonical Monte Carlo policy-gradient method; [[Algorithms/Actor-Critic|actor-critic]], [[Algorithms/Proximal Policy Optimization|PPO]], [[Algorithms/Trust Region Policy Optimization|TRPO]], and [[Algorithms/DDPG|DDPG]] are all policy-based (or hybrid) refinements.

## See also
[[Value-based]], [[Policy Gradient Theorem]], [[Deterministic & Stochastic policies]], [[Algorithms/REINFORCE]], [[Algorithms/Actor-Critic]]
