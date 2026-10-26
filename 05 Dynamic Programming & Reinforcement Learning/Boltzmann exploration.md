---
title: Boltzmann exploration
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: drafted
confidence: 0
tags: [reinforcement-learning, bandits, exploration]
---
## Definition
Boltzmann (softmax) exploration selects actions stochastically, with probability increasing in estimated value but never collapsing entirely to zero for lower-valued actions:
$$\pi(a) = \frac{\exp(Q_t(a)/\tau)}{\sum_{b}\exp(Q_t(b)/\tau)},$$
where $\tau > 0$ is a **temperature** parameter. As $\tau \to 0^+$, the distribution concentrates on the greedy action (recovering greedy selection); as $\tau \to \infty$, it approaches a uniform distribution (recovering pure random exploration).

## Properties
### Relation to the policy-gradient softmax
This is the identical functional form used as a discrete-action **policy function** in [[Policy Gradient Theorem|policy-gradient methods]] (with a preference function $h(a,s,\theta)$ in place of $Q_t(a)/\tau$): $\pi(a\mid s,\theta) = e^{h(a,s,\theta)} / \sum_b e^{h(b,s,\theta)}$. In the bandit-exploration context, the "preferences" are simply the current value estimates scaled by inverse temperature, rather than a learned parametric function.

### Contrast with $\epsilon$-greedy and UCB
Unlike $\epsilon$-greedy, Boltzmann exploration is *graded*: an action estimated to be nearly as good as the best receives almost as much probability mass, while a clearly poor action is explored rarely — closer in spirit to UCB's targeted exploration, but without UCB's explicit dependence on visitation counts $N_t(a)$, so it does not automatically guarantee that under-visited actions are revisited at a controlled rate.

## See also
[[Multi-armed bandits]], [[Epsilon-greedy exploration]], [[UCB exploration]], [[Policy Gradient Theorem]]
