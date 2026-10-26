---
title: Markov Decision Process
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: drafted
confidence: 0
tags: [reinforcement-learning, mdp]
---
## Definition
A **Markov Decision Process (MDP)** is the classical formalisation of sequential decision-making, generalising the single-state [[Multi-armed bandits|bandit]] setting: actions now influence not just the immediate reward, but also the subsequent state, and hence future rewards too. An MDP is specified by sets $\mathcal{S}$ (states), $\mathcal{A}(s)$ (actions available in state $s$), $\mathcal{R}$ (possible rewards), and a joint dynamics function
$$p(s',r\mid s,a) := \Pr[S_t=s', R_t=r \mid S_{t-1}=s, A_{t-1}=a],$$
which is a valid probability distribution: $\sum_{s'\in\mathcal S}\sum_{r\in\mathcal R}p(s',r\mid s,a) = 1$ for all $s\in\mathcal S, a\in\mathcal A(s)$. A **finite MDP** has $\mathcal S,\mathcal A,\mathcal R$ all finite.

## Properties
### The Markov property
A sequence of states $S_t$ is Markov (has the **Markov property**) iff the future is independent of the past given the present:
$$\Pr[S_{t+1}\mid S_1,\dots,S_t] = \Pr[S_{t+1}\mid S_t].$$
In a finite MDP, $R_t$ and $S_t$ have well-defined discrete distributions dependent *only* on the immediately preceding state and action — this is precisely the Markov property applied to the joint reward/state process.

### What counts as "environment"
$p$ defines the dynamics (state-reward transitions) of the MDP. The framework is deliberately abstract: the general rule is that anything the agent cannot change arbitrarily is considered part of the environment, even if the agent knows exactly how that part works but lacks control over it (see [[Agent-environment Interface]]).

### Marginal and derived quantities
From $p$, useful marginals follow: the **state-transition probability** $p(s'\mid s,a) = \sum_r p(s',r\mid s,a)$, and the **expected reward** for a state-action pair $r(s,a) = \mathbb E[R_t\mid S_{t-1}=s,A_{t-1}=a] = \sum_r r\sum_{s'}p(s',r\mid s,a)$.

### Goals, return, and value
The agent's goal is formalised via a [[Reward function|reward]] signal $R_t$, aggregated into the [[Discount factor|(discounted) return]] $G_t=\sum_k\gamma^kR_{t+k+1}$. Given a [[Deterministic & Stochastic policies|policy]] $\pi$, the [[State value function|state-value function]] $v_\pi(s)$ and [[Action value function|action-value function]] $q_\pi(s,a)$ measure expected return, and satisfy the recursive [[Bellman equation]].

## Examples
The 4×4 gridworld (a deterministic-transition MDP with $-1$ reward per step until a terminal corner is reached) and Gridworld with special states A/A′/B/B′ (leaving A yields $+10$, leaving B yields $+5$, leaving the grid yields $-1$ and no movement) are the module's running toy MDPs, used throughout [[Dynamic programming]], [[Monte Carlo Learning]] and [[Temporal-Difference Learning]] to illustrate each algorithm concretely.

## See also
[[Agent-environment Interface]], [[State value function]], [[Action value function]], [[Bellman equation]], [[Dynamic programming]]
