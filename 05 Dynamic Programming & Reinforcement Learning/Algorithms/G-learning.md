---
title: G-learning
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
unit: Algorithms
level: MSc
status: seeding
confidence: 0
tags: [reinforcement-learning, algorithms, theory, entropy-regularization]
---
## Definition
<!-- UNVERIFIED: check against Todorov (2007), "Linearly-solvable Markov decision problems", and Fox, Pakman & Tishby (2016), "Taming the Noise in Reinforcement Learning via Soft Updates"; not covered in the MA338 slide decks -->
G-learning augments the ordinary [[Bellman equation|Bellman]] control objective with a **KL-divergence penalty** against a reference (prior) policy $\pi_0$, rather than optimising expected reward alone. Instead of the Bellman optimality equation $q_*(s,a)=\sum_{s',r}p(s',r\mid s,a)[r+\gamma\max_{a'}q_*(s',a')]$, G-learning solves a **soft**, entropy/KL-regularised control problem whose value function satisfies
$$G(s,a) = \sum_{s',r}p(s',r\mid s,a)\left[r + \gamma\left(-\frac{1}{\beta}\ln\mathbb E_{a'\sim\pi_0(\cdot\mid s')}\left[e^{-\beta G(s',a')}\right]\right)\right],$$
for an inverse-temperature $\beta>0$ controlling the strength of the KL penalty (equivalently, how far the learned policy is allowed to deviate from the prior $\pi_0$).

## Properties
### The soft-max replacing the hard-max
Ordinary Q-learning's $\max_{a'}q_*(s',a')$ is replaced by a **soft-max** (log-sum-exp) over next actions, weighted by the reference policy $\pi_0$ — as $\beta\to\infty$, the KL penalty vanishes and the soft-max reduces exactly to $\max_{a'}$, recovering ordinary [[Algorithms/Q-learning|Q-learning]] as a limiting special case.

### Why regularise toward a prior at all
Three standard motivations: (i) **robustness** — a policy constrained to stay close to a known-safe prior avoids catastrophic exploration failures; (ii) **transfer/composability** — soft/linearly-solvable MDPs (Todorov) have a special algebraic structure under which solutions to *composite* tasks can sometimes be derived from solutions to simpler *component* tasks; (iii) **sample efficiency** — regularisation toward a reasonable prior can substantially reduce the effective search space during early learning, similar in spirit to how a [[Multi-armed bandits|bandit]] algorithm's exploration bonus focuses search rather than exploring uniformly.

### Relation to Soft Q-learning and maximum-entropy RL
G-learning is closely related to (and a KL-regularised generalisation of) [[Algorithms/Soft-Q-learning|Soft Q-learning]]: taking the reference policy $\pi_0$ to be uniform recovers the standard maximum-entropy RL objective (entropy regularisation is the special case of KL-regularisation against a uniform prior).

## See also
[[Algorithms/Soft-Q-learning]], [[Algorithms/Q-learning]], [[Bellman equation]], [[Policy Gradient Theorem]]
