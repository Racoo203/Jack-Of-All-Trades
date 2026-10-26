---
title: Model-free & Model-based
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: drafted
confidence: 0
tags: [reinforcement-learning, foundations]
---
## Definition
A method is **model-based** if it requires (or learns) the environment's dynamics function $p(s',r\mid s,a)$ — the transition/reward probabilities — and uses it to compute or plan value functions. A method is **model-free** if it learns purely from sampled experience (trajectories of states/actions/rewards obtained by interacting with the environment or a [[Simulator]]), without ever needing $p$ explicitly.

[[Dynamic programming]] is the model-based archetype (requires full knowledge of $p$). [[Monte Carlo Learning]] and [[Temporal-Difference Learning]] are model-free (they use only sampled experience).

## Properties
### Why model-free methods matter
In most real problems, either the dynamics of the environment are unknown, or the state/action space is too large for tabular DP to be feasible even when the dynamics *are* known. Model-free methods sidestep this: they require no prior knowledge of the environment's dynamics, yet can still attain optimal behaviour, purely from trial and error.

### A subtlety: knowing $p$ does not always help
Even when the environment's dynamics are fully known (e.g. Blackjack: the rules are completely specified), it can be prohibitively complex to actually *compute* $p(s',r\mid s,a)$ in closed form — e.g. enumerating "given the player's sum is 14 and they stick, what is $P(\text{win}\mid \text{dealer's up-card})$?" for every state requires effectively unrolling the whole game tree. Generating sample games, in contrast, is trivial. This is why Monte Carlo methods can be advantageous even with complete knowledge of the environment's dynamics.

### Learning from simulated vs. real experience
- Learning from **actual experience** requires no prior model knowledge and can still reach optimal behaviour.
- Learning from **simulated experience** is also powerful, but does require *some* model — though only one capable of generating sample transitions, not the full transition-probability table $p(s',r\mid s,a)$. This weaker requirement (a [[Simulator]]) is often far easier to satisfy than deriving $p$ in closed form.

### Indirect (planning) RL
A third category — **planning methods** — learns a model of the environment from real experience and then uses that learned model to improve the policy (Monte Carlo Tree Search is the canonical example — see [[Algorithms/n-step SARSA|n-step methods]] material). This introduces a second source of approximation error (model error, in addition to value-function error) but can be substantially more data-efficient, since a learned model can be queried arbitrarily many times without further environment interaction.

## See also
[[Dynamic programming]], [[Monte Carlo Learning]], [[Temporal-Difference Learning]], [[Simulator]], [[Markov Decision Process]]
