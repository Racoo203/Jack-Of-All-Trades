---
title: Multi-agent LQ
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: seeding
confidence: 0
tags: [reinforcement-learning, optimal-control, multi-agent, theory]
---
## Definition
<!-- UNVERIFIED: check against a dedicated multi-agent control/game-theory reference (e.g. Başar & Olsder, "Dynamic Noncooperative Game Theory"); not covered in the MA338 slide decks -->
Multi-agent LQ extends the single-agent [[Linear-quadratic problems|linear-quadratic]] setting to $N$ agents, each with their own control $u_t^i$ and, generally, their own quadratic cost $J^i$, coupled through a **shared** linear state transition:
$$x_{t+1} = Ax_t + \sum_{i=1}^N B^iu_t^i + w_t, \qquad J^i = \mathbb E\left[\sum_t\left(x_t^\top Q^ix_t + \sum_j(u_t^j)^\top R^{i,j}u_t^j\right)\right].$$
Because the state dynamics couple every agent's control together, each agent's optimal action generally depends on what the *other* agents are doing — turning the problem into a **dynamic (stochastic) game** rather than a single-agent optimal-control problem.

## Properties
### Cooperative vs. non-cooperative structure
If all agents share an identical cost $J^1=\cdots=J^N$ (**cooperative/team** setting), the problem reduces to a single centralised LQ problem over the joint control $u_t = (u_t^1,\dots,u_t^N)$, solved by the ordinary [[Linear-quadratic regulator (LQR)|LQR]] Riccati recursion with a block-structured $B$ matrix. If costs differ (**non-cooperative/general-sum** setting), the relevant solution concept is a **Nash equilibrium** of the dynamic game: a set of policies $(u^{1*},\dots,u^{N*})$ such that no agent can unilaterally improve its own cost by deviating — computed via a *coupled* system of Riccati-like equations (one per agent), rather than the single Riccati recursion of the single-agent case.

### Relation to multi-agent reinforcement learning (MARL)
Multi-agent LQ is the closed-form-solvable special case most MARL theory is benchmarked/stress-tested against, exactly analogous to how single-agent LQR grounds single-agent continuous-control RL theory. It captures core MARL phenomena in tractable form: non-stationarity from the perspective of any single agent (the "environment", from agent $i$'s point of view, includes the other agents' evolving policies — an instance of [[Stationary & Non-stationary Environments|environment non-stationarity]] induced *endogenously* by co-learning, rather than by the physical environment itself), and the cooperative/competitive spectrum.

## See also
[[Linear-quadratic regulator (LQR)]], [[Linear-quadratic problems]], [[Stationary & Non-stationary Environments]], [[Deterministic & Stochastic policies]]
