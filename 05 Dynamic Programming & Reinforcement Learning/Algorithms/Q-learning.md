---
title: Q-learning
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
unit: Algorithms
level: MSc
status: drafted
confidence: 0
tags: [reinforcement-learning, td-learning, algorithms, off-policy]
---
## Definition
Q-learning (Watkins, 1989) is the canonical **off-policy** [[Temporal-Difference Learning|TD control]] algorithm:
$$Q(S_t,A_t) \leftarrow Q(S_t,A_t) + \alpha\left[R_{t+1}+\gamma\max_a Q(S_{t+1},a) - Q(S_t,A_t)\right].$$
Widely regarded as one of RL's most important early breakthroughs: the learned $Q$ directly approximates $q_*$, the optimal action-value function, **independent of the policy being followed** while collecting data — simplifying convergence analysis and guaranteeing earlier convergence in practice than on-policy alternatives.

## Properties
### Off-policy by construction
The update bootstraps from $\max_a Q(S_{t+1},a)$ — the value of the *greedy* action in the next state — regardless of which action the exploring behaviour policy actually selects there. The target policy (implicit: greedy w.r.t. $Q$) and behaviour policy (e.g. $\epsilon$-greedy, needed to keep exploring) are thus decoupled, which is the defining structural difference from [[Algorithms/SARSA|SARSA]] (which bootstraps from the action *actually taken* next, $Q(S_{t+1},A_{t+1})$).

### Pseudocode
```
Parameters: α ∈ (0,1], small ε>0
Init: Q(s,a) arbitrary, Q(terminal,·)=0
for each episode:
    initialise S0
    choose A0 from S0 via soft policy on Q
    for k = 0,1,2,...:
        take Ak, observe Sk+1, Rk+1
        Q(Sk,Ak) ← Q(Sk,Ak) + α[Rk+1 + γ max_a Q(Sk+1,a) - Q(Sk,Ak)]
        if Sk+1 terminal: break
```

### Interaction with function approximation: the Deadly Triad
Tabular Q-learning has strong convergence guarantees. Once $Q$ is replaced with a function approximator (e.g. a neural network, see [[Algorithms/Deep Q-Network|DQN]]), Q-learning simultaneously exhibits **all three** components of the Deadly Triad — bootstrapping (via $\max_aQ(S_{t+1},a,w)$), function approximation, and off-policy learning — making naive "deep Q-learning" prone to divergence. DQN's experience replay and target networks exist specifically to stabilise this combination — see [[Nonlinear Functional Approximation]] and [[Deep Reinforcement Learning]].

## Examples
Same 3×2 Gridworld transition as [[Algorithms/SARSA]] (start 1, goal 6, $\{2,\text{up},(-1),5,\text{right},(10),6\}$, $\alpha=0.2,\gamma=0.8$): $Q(2,\text{up}) \leftarrow 6+0.2[-1+0.8\max(2,3,4,5,\dots\text{i.e. }Q(5,\cdot))-6]$; since $\max_a Q(5,a) = \max(10,5,8)=10$ from the given table, this happens to coincide numerically with the SARSA update on this particular transition (because the actually-taken next action, "right", was itself the greedy one) — illustrating that SARSA and Q-learning only diverge numerically when the sampled next action is *not* the greedy one.

## See also
[[Temporal-Difference Learning]], [[Algorithms/SARSA]], [[Nonlinear Functional Approximation]], [[Algorithms/Deep Q-Network]], [[On-policy & Off-policy]]
