---
title: Trust Region Policy Optimization
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
unit: Algorithms
level: MSc
status: seeding
confidence: 0
tags: [reinforcement-learning, policy-gradient, algorithms, on-policy]
---
## Definition
<!-- UNVERIFIED: check against Schulman et al. (2015), "Trust Region Policy Optimization"; not covered in the MA338 slide decks -->
Trust Region Policy Optimization (TRPO) is an on-policy policy-gradient method addressing a key weakness of plain [[Policy Gradient Theorem|policy gradient]]/[[Algorithms/REINFORCE|REINFORCE]]-style updates: an update step $\theta_{t+1}=\theta_t+\alpha\nabla J(\theta_t)$ of the *wrong size* can move the policy so far in parameter space that performance collapses catastrophically (since $\theta$-space distance does not correspond reliably to *policy-behaviour* distance). TRPO instead maximises a surrogate objective **subject to a constraint** that the new and old policies remain close in a *behavioural* sense — measured by KL divergence, not parameter distance:
$$\max_\theta\ \mathbb E_{s,a\sim\pi_{\theta_{\text{old}}}}\left[\frac{\pi_\theta(a\mid s)}{\pi_{\theta_{\text{old}}}(a\mid s)}A^{\pi_{\theta_{\text{old}}}}(s,a)\right] \quad \text{s.t.}\quad \mathbb E_s\left[D_{KL}\left(\pi_{\theta_{\text{old}}}(\cdot\mid s)\,\|\,\pi_\theta(\cdot\mid s)\right)\right]\le\delta.$$

## Properties
### The advantage function
$A^\pi(s,a):=q_\pi(s,a)-v_\pi(s)$ measures how much better action $a$ is than the policy's average at state $s$ — using the advantage (rather than $q_\pi$ directly) in the surrogate objective is itself a variance-reduction device, in the same spirit as [[Algorithms/REINFORCE|REINFORCE's baseline]] $b(s)=v_\pi(s)$: $A^\pi(s,a) = q_\pi(s,a)-v_\pi(s)$ is exactly $q_\pi(s,a)-b(s)$ with the canonical baseline choice.

### Why a trust region, not just importance-sampled reweighting
The importance-sampling ratio $\pi_\theta(a\mid s)/\pi_{\theta_{\text{old}}}(a\mid s)$ (see [[On-policy & Off-policy]]) allows reusing samples from $\pi_{\theta_{\text{old}}}$ to estimate the objective for a nearby $\pi_\theta$, but this estimate is only reliable when $\pi_\theta$ stays close to $\pi_{\theta_{\text{old}}}$ — exactly what the KL constraint enforces. TRPO's theoretical justification (Kakade & Langford, 2002; Schulman et al., 2015) is a monotonic-improvement guarantee: subject to a *sufficiently small* trust region, the true policy performance is guaranteed not to decrease.

### Computational cost
Solving the KL-constrained optimisation exactly requires a conjugate-gradient approximation of a Fisher-information-matrix–vector product (natural gradient) plus a line search — considerably more expensive per update than plain SGD, which is the direct motivation for [[Algorithms/Proximal Policy Optimization|PPO]]'s simpler clipped-surrogate approximation to the same idea.

## See also
[[Algorithms/Proximal Policy Optimization]], [[Policy Gradient Theorem]], [[Algorithms/Actor-Critic]], [[Algorithms/DDPG]]
