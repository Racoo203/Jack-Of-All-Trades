---
title: Simulator
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: drafted
confidence: 0
tags: [reinforcement-learning, foundations]
---
## Definition
A **simulator** (or **sample model**) of an environment is any mechanism able to generate sample transitions $(S_{t+1}, R_{t+1}) \sim p(\cdot,\cdot\mid S_t,A_t)$ on demand, without necessarily being able to output the transition-probability distribution $p(s',r\mid s,a)$ in closed form. This is a strictly weaker requirement than a full **distribution model**, which must be able to generate (or evaluate) all possible transitions and their exact probabilities — the requirement needed by [[Dynamic programming]].

## Properties
### Why simulators are enough for model-free-adjacent methods
[[Monte Carlo Learning]] and [[Temporal-Difference Learning]] only ever need *samples* of experience — either genuine interaction with the real environment, or interaction with a simulator standing in for it. Learning from simulated experience is powerful precisely because building a simulator (something that can be *run forward*) is often far easier than deriving the closed-form dynamics $p$ needed by DP. Blackjack is the canonical illustration in this module: the rules define a trivial simulator (deal cards, apply the rules), but computing $p(s',r\mid s,a)$ in closed form for DP would require enumerating and probability-weighting the entire remaining deck for every state — complex and error-prone, whereas generating a sample hand is immediate.

### Planning with a simulator
A simulator also underlies **planning methods** (indirect RL — see [[Model-free & Model-based]]): a model, whether given or learned from real experience, is queried repeatedly (simulated rollouts) to improve the value function/policy without further real-environment interaction. Monte Carlo Tree Search is the module's principal example: its Simulation step performs a rollout using a rollout policy through the simulator, without touching the real environment.

## See also
[[Model-free & Model-based]], [[Monte Carlo Learning]], [[Dynamic programming]]
