---
title: Proximal Policy Optimization
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
unit: Algorithms
level: MSc
status: seeding
confidence: 0
tags: [reinforcement-learning, policy-gradient, algorithms, on-policy]
---
## Definition
<!-- UNVERIFIED: check against Schulman et al. (2017), "Proximal Policy Optimization Algorithms"; not covered in the MA338 slide decks -->
Proximal Policy Optimization (PPO) achieves [[Algorithms/Trust Region Policy Optimization|TRPO]]'s goal — stable, monotonic-ish policy improvement without catastrophically large updates — using only first-order SGD, replacing TRPO's explicit KL-divergence constraint with a much cheaper **clipped surrogate objective**. Letting $r_t(\theta):=\pi_\theta(a_t\mid s_t)/\pi_{\theta_{\text{old}}}(a_t\mid s_t)$ be the same importance-sampling probability ratio TRPO uses, PPO's clipped objective is
$$L^{CLIP}(\theta) = \mathbb E_t\left[\min\left(r_t(\theta)A_t,\ \mathrm{clip}(r_t(\theta),1-\epsilon,1+\epsilon)A_t\right)\right],$$
for a small $\epsilon$ (e.g. $0.2$) and advantage estimate $A_t$ (see [[Algorithms/Trust Region Policy Optimization|TRPO]]'s advantage function).

## Properties
### How clipping enforces a soft trust region
- When the advantage $A_t>0$ (the action was better than average), clipping caps $r_t(\theta)$ at $1+\epsilon$: the objective is prevented from rewarding an arbitrarily large increase in the probability of a good action — removing the incentive to move $\theta$ too far in that direction in a single update.
- When $A_t<0$, clipping caps $r_t(\theta)$ at $1-\epsilon$ symmetrically: the objective is prevented from driving the probability of a bad action arbitrarily close to zero in one step.
- Taking the $\min$ of the clipped and unclipped terms makes the objective a **pessimistic lower bound**: it never rewards moving further from $\theta_{\text{old}}$ than the clip range once the sign of the advantage would make that direction attractive, but still allows the *unclipped* (more negative) term through when moving toward $\theta_{\text{old}}$ would otherwise look artificially good — this asymmetry is what prevents the clipping mechanism from being trivially exploited.

### Why PPO displaced TRPO in practice
PPO requires only ordinary first-order gradient computation (no conjugate-gradient Fisher-matrix approximation, no line search), making it substantially simpler to implement and cheaper per update than TRPO, while empirically matching or exceeding TRPO's sample efficiency and stability across most benchmark continuous-control and Atari tasks — this simplicity/performance trade-off is why PPO became the default on-policy baseline in most subsequent deep-RL work (e.g. it underlies much of modern RLHF fine-tuning for large language models, connecting directly to the DeepSeek-R1 discussion referenced in the PGT-II lecture).

### On-policy nature
Unlike [[Algorithms/DDPG|DDPG]], PPO is **on-policy**: each batch of trajectories is collected under the *current* $\pi_{\theta_{\text{old}}}$ and used for only a few epochs of clipped-objective updates before being discarded and re-collected — avoiding the off-policy Deadly-Triad concerns of DDPG/DQN, but at the cost of sample efficiency (no reuse of old data via a replay buffer).

## See also
[[Algorithms/Trust Region Policy Optimization]], [[Policy Gradient Theorem]], [[Algorithms/Actor-Critic]], [[On-policy & Off-policy]]
