---
title: DDPG
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
unit: Algorithms
level: MSc
status: seeding
confidence: 0
tags: [reinforcement-learning, deep-rl, algorithms, off-policy, continuous-control]
---
## Definition
<!-- UNVERIFIED: check against Lillicrap et al. (2015), "Continuous control with deep reinforcement learning"; not covered in the MA338 slide decks -->
Deep Deterministic Policy Gradient (DDPG) extends [[Algorithms/Deep Q-Network|DQN]]-style off-policy learning to **continuous** action spaces by pairing a **deterministic** actor $\mu(s,\theta)$ with a Q-critic $Q(s,a,w)$, avoiding the $\max_a$ over a continuous action space that ordinary Q-learning would require.

## Properties
### Actor and critic updates
The critic is trained exactly as in [[Algorithms/Deep Q-Network|DQN]] (experience replay, target networks), minimising $L(w)=\mathbb E\left[(r+\gamma Q(s',\mu(s',\theta^-),w^-)-Q(s,a,w))^2\right]$ — using the *actor's own* deterministic action $\mu(s',\theta^-)$ in place of $\max_aQ(s',a,w^-)$, since a discrete max is unavailable/intractable over $\mathbb R^m$. The actor is trained by the **deterministic policy gradient** (Silver et al., 2014):
$$\nabla_\theta J(\theta) = \mathbb E_s\left[\nabla_aQ(s,a,w)\big|_{a=\mu(s,\theta)}\,\nabla_\theta\mu(s,\theta)\right],$$
i.e. ascend the critic's estimated Q-value with respect to the action, backpropagated through the deterministic policy — directly analogous to how a value-based method would act greedily, but made differentiable so it works continuously rather than via a discrete $\arg\max$.

### Relation to Actor-Critic and DQN
DDPG is best understood as [[Algorithms/Actor-Critic|Actor-Critic]]'s structure (actor updated by policy gradient, critic updated by TD) combined with DQN's stabilisation machinery (replay buffer, target networks, here applied to *both* actor and critic target copies) and a deterministic (rather than stochastic) policy — trading off the exploration benefits of a stochastic policy for the tractability of continuous-action Q-maximisation. Exploration is typically added externally, by injecting noise (e.g. Ornstein–Uhlenbeck or Gaussian) into the actor's action at rollout time, since a purely deterministic policy would not explore on its own.

### Off-policy by construction
Like Q-learning/DQN, DDPG is off-policy: the replay buffer stores transitions from past (noise-injected) behaviour, reused to train both actor and critic under the current policy — inheriting DQN's Deadly-Triad concerns (see [[Nonlinear Functional Approximation]]), which the target-network machinery is again responsible for controlling.

## See also
[[Algorithms/Actor-Critic]], [[Algorithms/Deep Q-Network]], [[Policy Gradient Theorem]], [[Algorithms/Proximal Policy Optimization]], [[Algorithms/Trust Region Policy Optimization]]
