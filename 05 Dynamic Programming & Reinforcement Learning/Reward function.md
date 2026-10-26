---
title: Reward function
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: drafted
confidence: 0
tags: [reinforcement-learning, foundations]
---
## Definition
The reward is a scalar signal $R_t \in \mathbb{R}$ sent from the environment to the agent at each time step, formalising the agent's purpose. In a [[Markov Decision Process]] the reward is generated jointly with the next state by the dynamics function
$$p(s', r \mid s, a) := \Pr[S_t = s', R_t = r \mid S_{t-1} = s, A_{t-1} = a].$$
The agent's goal is to maximise the total **cumulative** reward received (the [[Discount factor|(discounted) return]]) — not the immediate reward at any single step.

## Properties
### The reward hypothesis
All goals can, in principle, be formalised as the maximisation of the expected cumulative sum of a scalar reward signal. This is a strong modelling assumption ("Reward is Enough", Silver et al. 2021), and it is critical that the reward faithfully captures *what* should be achieved rather than *how*: a chess agent should be rewarded only for winning, not for capturing pieces or controlling the centre — rewarding subgoals invites the agent to find ways of achieving the subgoal without achieving the true goal (reward hacking).

### Reward shaping and policy invariance
Auxiliary reward terms are often added to speed up learning: $R'(s,a,s') = R(s,a,s') + F(s,a,s')$. Careless shaping is dangerous: Randløv & Alström (1998), teaching a simulated bicycle to reach a goal, gave positive reward for moving closer to the goal — the agent learned to ride in tiny circles near the start state, since no negative reward penalised moving away. Ng, Harada & Russell (1999) show that a shaping function $F$ preserves the optimal policy **if and only if** it is a *potential-based shaping function*:
$$F(s,a,s') = \gamma\Phi(s') - \Phi(s)$$
for some $\Phi: \mathcal{S} \to \mathbb{R}$. If $F$ has this form, $\pi$ is optimal in the shaped MDP $\{\mathcal{S},\mathcal{A},R+F,\gamma\}$ iff it is optimal in the original $\{\mathcal{S},\mathcal{A},R,\gamma\}$ (**sufficiency**); if $F$ is *not* of this form, there exists some $R$ for which the shaped-MDP-optimal policy is not optimal in the original (**necessity**). A natural choice is $\Phi(s) = v_M^*(s)$, which drives $v_{M'}^*(s) = 0$ for all $s$.

A consequence: $Q^*_{M'}(s,a) = Q_M^*(s,a) - \Phi(s)$ and $V^*_{M'}(s) = V_M^*(s) - \Phi(s)$.

**Scaling vs. translating.** More generally, among *non-additive* transformations, the only one preserving optimal policies (besides potential-based shaping) is uniform positive scaling: $R' = k \cdot R$ for $k > 0$. Scaling all rewards by a positive constant does **not** change the optimal policy — but adding a positive constant $c$ to every reward **can** change it (this is a classic exam trap: with $\gamma = 1$ and a policy that reaches a terminal state faster vs. slower, adding $c>0$ per step biases the comparison toward *longer* trajectories, since more steps accumulate more of the added constant).

## Examples
Consider an MDP where action $A_1$ from $S_0$ reaches the terminal state directly with reward $-1$, while $A_2$ requires two steps of reward $-1$ each via $S_2$. With $\gamma=1$, $A_1$ is optimal ($-1 > -2$). Adding $c=2$ to every reward flips the comparison: $A_1$ now yields $1$, $A_2$ yields $2$, and $A_2$ becomes optimal — despite reward *translation* seemingly being an innocuous rescaling.

## See also
[[Markov Decision Process]], [[Discount factor]], [[Bellman equation]], [[Inverse Reinforcement Learning]]
