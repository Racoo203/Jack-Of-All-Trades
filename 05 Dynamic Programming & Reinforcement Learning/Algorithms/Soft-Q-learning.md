---
title: Soft-Q-learning
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
unit: Algorithms
level: MSc
status: seeding
confidence: 0
tags: [reinforcement-learning, algorithms, theory, entropy-regularization]
---
## Definition
<!-- UNVERIFIED: check against Haarnoja et al. (2017), "Reinforcement Learning with Deep Energy-Based Policies"; not covered in the MA338 slide decks -->
Soft Q-learning is the **maximum-entropy** special case of [[Algorithms/G-learning|G-learning]]: rather than regularising toward an arbitrary reference policy $\pi_0$, it adds an explicit entropy bonus $\mathcal H(\pi(\cdot\mid s))$ to the standard RL objective, so the agent maximises
$$J(\pi) = \mathbb E_\pi\left[\sum_t\gamma^t\left(R_{t+1}+\alpha\,\mathcal H(\pi(\cdot\mid S_t))\right)\right],$$
for a temperature $\alpha>0$ controlling the entropy bonus's weight. The corresponding soft Bellman equation replaces the hard max with a log-sum-exp ("soft-max") over actions:
$$V_{\text{soft}}(s) = \alpha\ln\int_{\mathcal A}\exp\left(\frac{1}{\alpha}Q_{\text{soft}}(s,a)\right)da, \qquad Q_{\text{soft}}(s,a) = r(s,a)+\gamma\,\mathbb E_{s'}[V_{\text{soft}}(s')].$$

## Properties
### The optimal soft policy is Boltzmann-distributed
The policy that maximises the entropy-regularised objective, given $Q_{\text{soft}}$, is
$$\pi(a\mid s) = \exp\left(\frac{1}{\alpha}\left(Q_{\text{soft}}(s,a)-V_{\text{soft}}(s)\right)\right),$$
a direct continuous-action generalisation of the discrete [[Boltzmann exploration|Boltzmann/softmax]] exploration policy — here derived as the exact optimum of a regularised objective, rather than adopted heuristically for exploration.

### Why maximum entropy, beyond exploration
Beyond encouraging exploration (a stochastic, high-entropy policy naturally samples more broadly than a near-deterministic greedy one — directly addressing [[Exploration vs Exploitation]] without a separate hand-tuned exploration schedule like [[Epsilon-greedy exploration|$\epsilon$-greedy]]), maximum-entropy objectives also yield **more robust** policies (multiple near-equally-good action modes are all retained with meaningful probability, rather than collapsing onto a single mode that may be brittle to model/environment mismatch) and provide a smoother, easier-to-optimise objective landscape, since the entropy term regularises against premature, overconfident convergence to a single action.

### Descendants: Soft Actor-Critic
Soft Q-learning's ideas were subsequently extended into an actor-critic architecture (**Soft Actor-Critic**, Haarnoja et al., 2018), pairing an explicit stochastic policy network with a soft Q-critic, and remains one of the standard off-policy baselines for continuous control, alongside [[Algorithms/DDPG|DDPG]] and its successor TD3.

## See also
[[Algorithms/G-learning]], [[Boltzmann exploration]], [[Exploration vs Exploitation]], [[Algorithms/Q-learning]]
