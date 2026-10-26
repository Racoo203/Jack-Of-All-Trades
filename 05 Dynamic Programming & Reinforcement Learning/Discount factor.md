---
title: Discount factor
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: drafted
confidence: 0
tags: [reinforcement-learning, foundations]
---
## Definition
The discount factor $\gamma \in [0,1]$ weights future rewards relative to immediate ones inside the **return**, the quantity an agent seeks to maximise. For episodic tasks with a natural final step $T$ (see [[Infinite & Finite Time Horizon]]), the simplest return is the plain sum $G_t := R_{t+1} + \cdots + R_T$. For continuing tasks (no natural termination), an undiscounted sum can diverge, so the **discounted return** is used instead:
$$G_t := R_{t+1} + \gamma R_{t+2} + \gamma^2 R_{t+3} + \cdots = \sum_{k=0}^{\infty} \gamma^k R_{t+k+1}.$$
Setting $R_t = 0$ for all $t > T$ recovers the episodic (undiscounted, $\gamma=1$) case as a special instance, so the discounted form is the general one used throughout the module.

## Properties
### Recursive (Bellman-style) structure
$G_t$ satisfies the recurrence
$$G_t = R_{t+1} + \gamma G_{t+1}.$$
*Proof.* $G_t = R_{t+1} + \gamma R_{t+2} + \gamma^2 R_{t+3} + \cdots = R_{t+1} + \gamma(R_{t+2} + \gamma R_{t+3} + \cdots) = R_{t+1} + \gamma G_{t+1}$. $\blacksquare$
This recurrence is exactly what makes the [[Bellman equation]] possible.

### Constant-reward closed form
If $R_j = c$ for all $j$, then $G_t = c\sum_{k=0}^\infty \gamma^k = \dfrac{c}{1-\gamma}$ for $\gamma < 1$ (geometric series).

### Interpretation of $\gamma$
- A reward received $k$ steps in the future is worth only $\gamma^{k-1}$ times what it would be worth if received immediately.
- If $\gamma < 1$ and rewards are bounded, the infinite sum in $G_t$ is finite even for continuing tasks.
- $\gamma = 0$: the agent is fully **myopic**, maximising only $R_{t+1}$.
- $\gamma \to 1$: the agent becomes increasingly **farsighted**, weighting distant rewards almost as heavily as immediate ones.

### Why discount at all?
- Mathematical convenience (guarantees a finite return).
- Avoids infinite returns on continuing tasks.
- Models genuine uncertainty about the future (a reward promised later might not materialise).
- Analogous to time value of money in finance: reward today is worth more than the same reward tomorrow.
- Matches observed preference for immediate reward in animal/human behaviour.

## Examples
With $\gamma = 0.5$ and rewards $R_1,\dots,R_5 = 1,2,3,4,5$ (episode ends at $T=5$), working backwards: $G_5 = 0$, $G_4 = R_5 = 5$, $G_3 = R_4 + \gamma G_4 = 4 + 2.5 = 6.5$, $G_2 = 3 + 0.5(6.5) = 6.25$, $G_1 = 2 + 0.5(6.25) = 5.125$, $G_0 = 1 + 0.5(5.125) = 3.5625$.

## See also
[[Bellman equation]], [[State value function]], [[Action value function]], [[Infinite & Finite Time Horizon]], [[Reward function]]
