---
title: n-step SARSA
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
unit: Algorithms
level: MSc
status: drafted
confidence: 0
tags: [reinforcement-learning, td-learning, algorithms, on-policy]
---
## Definition
n-step SARSA generalises [[Algorithms/SARSA|SARSA]] (1-step TD) and Monte Carlo control ($\infty$-step) into a single spectrum, parametrised by $n$. The **n-step return** for action values is
$$G_t^{(n)} := R_{t+1}+\gamma R_{t+2}+\cdots+\gamma^{n-1}R_{t+n}+\gamma^n Q(S_{t+n},A_{t+n}) = \sum_{i=t+1}^{t+n}\gamma^{i-t-1}R_i + \gamma^nQ(S_{t+n},A_{t+n}),$$
and the update is $Q(S_t,A_t) \leftarrow Q(S_t,A_t) + \alpha[G_t^{(n)}-Q(S_t,A_t)]$. $n=1$ recovers ordinary SARSA (TD(0)); $n\to\infty$ recovers a Monte Carlo-style full-return update.

## Properties
### Handling episode boundaries
If the episode terminates before $t+n$ (i.e. $T < t+n$), the sum in $G_t^{(n)}$ is truncated at $T$ and the bootstrap term dropped:
$$G_t^{(n)} := \sum_{i=t+1}^{\min(t+n,T)}\gamma^{i-t-1}R_i + \left[\gamma^nQ(S_{t+n},A_{t+n})\ \text{if } t+n<T\right].$$

### Pseudocode
```
Parameters: α ∈ (0,1], n ∈ Z+, small ε>0
Init: Q(s,a) arbitrary except terminal; π ε-greedy w.r.t. Q
for each episode:
    initialise S0, A0 ~ π(·|S0); store them; T ← ∞
    for k = 0,1,2,...:
        if k < T:
            take Ak, observe & store Sk+1, Rk+1
            if Sk+1 terminal: T ← k+1
            else: store Ak+1 ~ π(·|Sk+1)
        t ← k - n + 1
        if t ≥ 0:
            g ← Σ_{i=t+1}^{min(t+n,T)} γ^{i-t-1} Ri
            if t+n < T: g ← g + γ^n Q(St+n,At+n)
            Q(St,At) ← Q(St,At) + α[g - Q(St,At)]
            (if learning π ≈ π*, keep π(·|St) ε-greedy w.r.t. Q)
    until t = T-1
```
Note the update at time $t$ requires information up to $t+n$: updates are delayed by $n$ steps, and the last $n$ states/actions/rewards must be stored — the algorithm is **not** fully online the way TD(0)/SARSA is.

### Why intermediate $n$ tends to work best
Empirically (19-state random walk benchmark), neither the $n=1$ (TD(0)) nor $n=\infty$ (MC) extreme minimises RMS prediction error for a fixed number of episodes; **intermediate** $n$ performs best, generalising the bootstrapping of TD over multiple steps rather than a single one. In the Gridworld path-strengthening illustration: one-step SARSA only strengthens the *last* action of a rewarding trajectory, whereas $n$-step SARSA strengthens the last $n$ actions — so more is learned from a single episode, at the cost of a learning delay and the memory needed to store $n$ steps of history. This delay/memory trade-off is exactly what [[Algorithms/SARSA(lambda)|SARSA(λ)]] (eligibility traces) is designed to avoid while retaining the same "spread credit over multiple recent steps" benefit.

## Examples
In the Gridworld speedup illustration (Lecture 6), a single episode ending at a high-reward state $G$: one-step SARSA strengthens only the final action; ten-step SARSA strengthens the last ten actions of the path that led there — visibly propagating credit much further back per episode.

## See also
[[Temporal-Difference Learning]], [[Algorithms/SARSA]], [[Algorithms/SARSA(lambda)]], [[Monte Carlo Learning]], [[UCB exploration]] (UCT, the tree-search analogue)
