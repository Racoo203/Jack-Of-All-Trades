---
title: SARSA
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
unit: Algorithms
level: MSc
status: drafted
confidence: 0
tags: [reinforcement-learning, td-learning, algorithms, on-policy]
---
## Definition
SARSA is the canonical **on-policy** [[Temporal-Difference Learning|TD control]] algorithm: it estimates $q_\pi(s,a)$ (and drives $\pi$ toward $q_*$) using the update
$$Q(S_t,A_t) \leftarrow Q(S_t,A_t) + \alpha\left[R_{t+1}+\gamma Q(S_{t+1},A_{t+1}) - Q(S_t,A_t)\right],$$
with $Q(S_{t+1},A_{t+1}):=0$ if $S_{t+1}$ is terminal. The algorithm's name comes directly from the five quantities the update requires: $(S_t, A_t, R_{t+1}, S_{t+1}, A_{t+1})$.

## Properties
### On-policy by construction
$A_{t+1}$ is the action *actually chosen* by the current behaviour policy (e.g. $\epsilon$-greedy derived from $Q$) — not the greedy action with respect to $Q(S_{t+1},\cdot)$. This is what makes SARSA on-policy: the value being learned is the value of the policy currently being followed (including its exploratory, non-greedy choices), not of the greedy policy alone. Contrast directly with [[Algorithms/Q-learning|Q-learning]].

### Pseudocode
```
Parameters: α ∈ (0,1], small ε>0
Init: Q(s,a) arbitrary, Q(terminal,·)=0
for each episode:
    initialise S0
    choose A0 from S0 via soft policy (e.g. ε-greedy) on Q
    for k = 0,1,2,...:
        take Ak, observe Sk+1, Rk+1
        choose Ak+1 from Sk+1 via soft policy on Q
        Q(Sk,Ak) ← Q(Sk,Ak) + α[Rk+1 + γQ(Sk+1,Ak+1) - Q(Sk,Ak)]
        if Sk+1 terminal: break
```

## Examples
3×2 Gridworld (Lecture 5): start node 1, goal node 6 ($+10$), $-1$ elsewhere. From the sampled transition $\{2,\text{up},(-1),5,\text{right},(10),6\}$, with $\alpha=0.2,\gamma=0.8$: $Q(2,\text{up}) \leftarrow 6 + 0.2[-1+0.8(10)-6] = 6+0.2(1) = 6.2$ (using $Q(5,\text{right})=10$ from the table before its own update — SARSA uses the actually-selected next action's *current* estimate). This is directly comparable, on the same trajectory, against [[Algorithms/Q-learning]]'s update — a standard MA338 exam pairing (see the MOC's Exam focus).

## See also
[[Temporal-Difference Learning]], [[Algorithms/Q-learning]], [[Algorithms/n-step SARSA]], [[Algorithms/SARSA(lambda)]], [[On-policy & Off-policy]]
