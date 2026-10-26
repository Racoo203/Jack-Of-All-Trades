---
title: Epsilon-greedy exploration
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: drafted
confidence: 0
tags: [reinforcement-learning, bandits, exploration]
---
## Definition
$\epsilon$-greedy is the simplest fix to pure greedy action selection: behave greedily most of the time, but with a small fixed probability $\epsilon \in (0,1)$, select an action uniformly at random instead (independent of the current value estimates):
$$A \leftarrow \begin{cases}\arg\max_a Q(a) & \text{with probability } 1-\epsilon\\ \text{uniformly random action} & \text{with probability } \epsilon\end{cases}$$
In state-conditioned form, an $\epsilon$-soft policy chooses each action with probability at least $\tfrac{\epsilon}{|\mathcal A(s)|}$, and the greedy action with probability $1-\epsilon+\tfrac{\epsilon}{|\mathcal A(s)|}$ — this is the form used to keep on-policy control methods (e.g. [[Algorithms/SARSA]], Monte Carlo control) exploring every state-action pair. See [[On-policy & Off-policy]].

## Properties
### Pseudocode (bandit form)
```
initialise Q(a) ← 0, N(a) ← 0 for a = 1..k
loop:
    A ← argmax_a Q(a) with prob. 1-ε, else random action
    R ← bandit(A)
    N(A) ← N(A) + 1
    Q(A) ← Q(A) + (1/N(A))[R - Q(A)]
```

### Guaranteed but inefficient exploration
Since every action retains probability $\ge \epsilon/|\mathcal A(s)|$ forever, $\epsilon$-greedy guarantees every action is sampled infinitely often as $t\to\infty$, which is exactly the coverage condition needed for convergence to $q_*$. Its weakness is that exploration is **indiscriminate**: a clearly suboptimal action is explored exactly as often as a near-optimal one. [[UCB exploration]] and [[Thompson sampling]] address this by directing exploration toward actions whose value is *uncertain*, not merely non-greedy.

## See also
[[Multi-armed bandits]], [[On-policy & Off-policy]], [[UCB exploration]], [[Boltzmann exploration]], [[Thompson sampling]]
