---
title: Agent-environment Interface
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: drafted
confidence: 0
tags: [reinforcement-learning, foundations]
---
## Definition
Reinforcement learning (RL) formalises sequential decision-making as an interaction between two entities: the **agent** (the learner/decision-maker) and the **environment** (everything outside the agent). Interaction happens over a sequence of discrete time steps $t = 0, 1, 2, \dots$:

- At each step $t$, the agent observes some representation of the environment's state $S_t$ (or, more generally, an observation $O_t$), and on that basis selects an action $A_t \in \mathcal{A}(S_t)$.
- One step later, at $t+1$, the environment emits a numerical **reward** $R_{t+1} \in \mathcal{R} \subset \mathbb{R}$ and a new state $S_{t+1}$.

This produces a **trajectory** (or **episode**, if it terminates):
$$S_0, A_0, R_1, S_1, A_1, R_2, S_2, \dots$$

The agent's behaviour is governed by a [[Deterministic & Stochastic policies|policy]] $\pi$, which uses experience from the past (states, past rewards, and possibly a [[Model-free & Model-based|model]] of the environment) to recommend actions. A general rule for what belongs to the environment: **anything the agent cannot change arbitrarily is part of the environment** — even if the agent has full knowledge of how it works (e.g. a Rubik's Cube: known dynamics, but the agent cannot simply decree the cube solved).

## Properties
### Contrast with other learning paradigms
- **Supervised learning (SL)**: learns from a training set of labelled examples provided by a knowledgeable external supervisor. There is no interaction — the data is fixed and pre-labelled.
- **Unsupervised learning (UL)**: finds hidden structure in unlabelled data.
- **Reinforcement learning**: learns purely from **trial and error** and **delayed reward**, the two features that most distinguish it from SL/UL. Informally: UL might let you cluster together the places where wild animals live; SL could teach you to recognise a lion; only RL tells you that you need to run from that place — because running is the *action* that maximises long-run reward, not merely a label.

### The reward signal defines the goal
On each time step, the environment sends the agent a single scalar $R_t$ (see [[Reward function]]). This signal alone defines the goal of the RL problem: the agent's objective is to maximise the *cumulative* reward it receives, not the immediate one. A [[State value function|value function]] specifies what is good *in the long run* — the total reward the agent can expect to accumulate starting from a given state — which is what distinguishes it from the reward signal itself (good in the immediate sense only).

### Elements of an RL problem
1. **Optimisation** — find an optimal way to make decisions.
2. **Delayed consequences** — decisions now can affect outcomes much later.
3. **Exploration** — learning about the world by acting in it, where the actions taken determine what can be learned (see [[Exploration vs Exploitation]]).
4. **Decisions** — made via a policy that maps experience to actions.

## Examples
Chess, a Roomba navigating a room, and preparing breakfast all share the same underlying structure: an active decision-making agent interacting with an environment to achieve a goal under uncertainty, where correct choices require anticipating indirect, delayed consequences (foresight/planning).

## See also
[[Exploration vs Exploitation]], [[Reward function]], [[State value function]], [[Markov Decision Process]], [[Model-free & Model-based]]
