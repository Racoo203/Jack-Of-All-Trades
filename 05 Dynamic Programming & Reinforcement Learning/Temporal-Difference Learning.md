---
title: Temporal-Difference Learning
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: drafted
confidence: 0
tags: [reinforcement-learning, td-learning]
---
## Definition
Temporal-Difference (TD) learning is, like [[Monte Carlo Learning|Monte Carlo]], a [[Model-free & Model-based|model-free]] method that learns directly from sampled experience. But like [[Dynamic programming|DP]], it **bootstraps**: its updates use existing estimates rather than waiting for a full episodic return. TD is often described as combining the best of MC (learns from raw experience, no model needed) and DP (bootstraps, updates online).

The simplest form, **TD(0)** (one-step TD), updates $V(S_t)$ using only the immediate reward and the discounted estimate of the successor state's value, rather than waiting until termination:
$$V(S_t) \leftarrow V(S_t) + \alpha\left[R_{t+1}+\gamma V(S_{t+1}) - V(S_t)\right].$$
Compare with the MC update $V(S_t)\leftarrow V(S_t)+\alpha[G_t-V(S_t)]$: TD(0) substitutes the *sampled* $R_{t+1}+\gamma V(S_{t+1})$ for the *full* $G_t$, needing to wait only one step ($t\to t+1$) rather than until episode termination.

## Properties
### The TD error
The bracketed quantity $\delta_t := R_{t+1}+\gamma V(S_{t+1})-V(S_t)$ is called the **TD error**: the discrepancy between the current estimate $V(S_t)$ and the one-step bootstrapped target. It recurs throughout the module's control algorithms ([[Algorithms/SARSA|SARSA]], [[Algorithms/Q-learning|Q-learning]]) and reappears, generalised, as the loss driving [[Deep Reinforcement Learning|DQN]]'s gradient updates.

### Pseudocode: Tabular TD(0)
```
Input: policy π to evaluate; step size α ∈ (0,1]
Init: V(s) arbitrary, V(terminal)=0
for each episode:
    initialise S0
    for k = 0,1,2,...:
        Ak ← action from π(Sk)
        observe Sk+1, Rk+1
        V(Sk) ← V(Sk) + α[Rk+1 + γV(Sk+1) - V(Sk)]
        if Sk+1 terminal: break
```

### Why TD is preferred to MC in many settings
- **No terminal state required**: TD(0) updates after every single step, so it is naturally defined for **continuing** tasks, unlike MC, which requires episode termination to compute $G_t$ — see [[Infinite & Finite Time Horizon]].
- **Fully online and incremental**: updates happen immediately, without waiting for an episode to finish (relevant for long or never-ending episodes, where MC "loses" local information about whether recent decisions were good).
- **Both converge asymptotically** to the correct predictions, but their relative speed/efficiency depends on the problem — this remains an active empirical/theoretical question, not resolved by a single universal answer.

### On-policy control: SARSA
Following the GPI pattern, on-policy TD control estimates $q_\pi(s,a)$ directly by sampling entire quintuples $(S_t,A_t,R_{t+1},S_{t+1},A_{t+1})$ under the *current* policy $\pi$ — giving the algorithm its name. See [[Algorithms/SARSA]] for the full update rule and pseudocode.

### Off-policy control: Q-learning
Watkins (1989)'s Q-learning update replaces the *sampled* next action's value with the greedy $\max_a Q(S_{t+1},a)$, so the learned $Q$ converges to $q_*$ independent of the (exploratory) behaviour policy actually followed — off-policy by construction. See [[Algorithms/Q-learning]].

## See also
[[Monte Carlo Learning]], [[Dynamic programming]], [[Algorithms/SARSA]], [[Algorithms/Q-learning]], [[Algorithms/n-step SARSA]], [[On-policy & Off-policy]]
