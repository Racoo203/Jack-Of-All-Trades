---
title: Inverse Reinforcement Learning
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: seeding
confidence: 0
tags: [reinforcement-learning, theory]
---
## Definition
<!-- UNVERIFIED: check against a dedicated IRL reference (e.g. Ng & Russell 2000; Abbeel & Ng 2004); not covered in the MA338 slide decks -->
Inverse Reinforcement Learning (IRL) inverts the standard RL problem: rather than being given a [[Reward function]] and asked to find an optimal policy, IRL is given (observed) behaviour — typically expert demonstration trajectories $\{(s_t,a_t)\}$ assumed to be (near-)optimal under some *unknown* reward — and asked to **recover the reward function** that best explains that behaviour.

## Properties
### Ill-posedness
IRL is fundamentally **ill-posed**: for any observed policy $\pi$, there are infinitely many reward functions under which $\pi$ is optimal — trivially, the all-zero reward makes *every* policy optimal. Ng & Russell (2000) address this by seeking the reward function that makes the observed policy *maximally* better than all alternatives (a linear-programming formulation maximising the margin), rather than merely *any* reward consistent with it.

### Connection to reward shaping
The [[Reward function|potential-based shaping theorem]] (Ng, Harada & Russell 1999) is closely related in authorship and spirit: both address the question of which reward transformations preserve or determine optimal behaviour. Where reward shaping asks "does this reward transformation change the optimal policy?", IRL asks the inverse question: "given this (assumed-optimal) policy/behaviour, what reward is consistent with it?"

### Apprenticeship learning
A widely-used practical reformulation (Abbeel & Ng, 2004) avoids fully recovering the reward and instead seeks a policy whose *feature expectations* match those of the expert demonstrations — i.e. learn to perform *at least as well as* the demonstrator under the expert's (unknown but linearly-parametrised) true reward, without needing to pin the reward down uniquely. This sidesteps IRL's ill-posedness by only requiring behavioural matching, not reward identification.

### Relation to imitation learning
IRL is one of two broad families for learning from demonstrations, alongside direct **behavioural cloning** (supervised learning of $\pi(a\mid s)$ directly from expert $(s,a)$ pairs, with no reward recovered at all). IRL/apprenticeship learning is generally more robust to distributional shift than naive behavioural cloning, because it recovers (or approximates) the underlying *incentive structure* rather than merely the surface-level action mapping — but at the cost of requiring an RL solve (or an equivalent) as an inner loop.

## See also
[[Reward function]], [[Markov Decision Process]], [[Policy Gradient Theorem]]
