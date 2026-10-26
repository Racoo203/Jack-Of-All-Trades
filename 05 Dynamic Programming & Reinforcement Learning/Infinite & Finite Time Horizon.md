---
title: Infinite & Finite Time Horizon
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: drafted
confidence: 0
tags: [reinforcement-learning, foundations]
---
## Definition
An RL task has a **finite (time) horizon** — or is **episodic** — if the agent-environment interaction naturally breaks into subsequences ("episodes") that terminate at some step $T$: plays of a game, trips through a maze, or any other bounded repeated interaction. It has an **infinite horizon** — or is a **continuing task** — if the interaction goes on indefinitely with no natural termination.

## Properties
### Consequences for the return
Episodic tasks admit the plain (undiscounted) return $G_t = R_{t+1}+\cdots+R_T$ directly, since the sum is automatically finite. Continuing tasks need the [[Discount factor|discounted return]] $G_t = \sum_{k=0}^\infty \gamma^k R_{t+k+1}$ with $\gamma < 1$ to guarantee a finite value (assuming bounded rewards). Setting $R_t=0$ for $t>T$ shows the episodic case is recovered as $\gamma \to 1$, so the discounted formulation is the more general one, used uniformly throughout the module.

### Consequences for existence/uniqueness of $v_\pi$
The Bellman equation for $v_\pi$ has a **unique** solution precisely when $\gamma < 1$, *or* the task is episodic with finite termination time $T < \infty$ — either condition alone suffices. This existence/uniqueness result underlies the convergence guarantees of [[Dynamic programming|iterative policy evaluation]].

### Consequences for algorithm design
- [[Monte Carlo Learning]] fundamentally requires well-defined returns and is naturally suited to episodic (finite-horizon) tasks — it must wait for an episode to end to compute $G_t$.
- [[Temporal-Difference Learning]] is well-defined for **both**: it needs no terminal state, since it bootstraps after a single step rather than waiting for termination, making it naturally suited to continuing (infinite-horizon) tasks as well as episodic ones.
- [[Stationary & Non-stationary Policies|Optimal policies]] in infinite-horizon (or discounted) settings are stationary; in genuinely finite-horizon settings they are generally non-stationary (time-dependent).

## See also
[[Discount factor]], [[Monte Carlo Learning]], [[Temporal-Difference Learning]], [[Stationary & Non-stationary Policies]]
