---
title: UCB exploration
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: drafted
confidence: 0
tags: [reinforcement-learning, bandits, exploration]
---
## Definition
Upper-Confidence-Bound (UCB) action selection replaces $\epsilon$-greedy's indiscriminate exploration with exploration targeted at actions that are *uncertain*, i.e. under-sampled relative to how promising they look. UCB selects
$$A_t := \arg\max_a \left[Q_t(a) + c\sqrt{\frac{\ln t}{N_t(a)}}\right],$$
where $N_t(a)$ is the number of times $a$ has been selected before time $t$, and $c>0$ controls the degree of exploration. If $N_t(a)=0$, $a$ is treated as maximising (forces every action to be tried at least once).

## Properties
### Why "upper confidence bound"
$Q_t(a) + c\sqrt{\ln t / N_t(a)}$ is an upper bound (with confidence level controlled by $c$) on the plausible true value of $a$: the square-root term shrinks as $N_t(a)$ grows (more samples ⟹ tighter estimate) and grows (slowly, logarithmically) with $t$ (so an action neglected for a long time is eventually re-considered regardless of how confidently sub-optimal it looked). Taking the argmax of this optimistic upper bound is a specific instance of the **optimism in the face of uncertainty** principle underlying most bandit algorithms with provable [[Regret Analysis|regret]] guarantees.

### A recurring exam trap
UCB does **not** select every suboptimal action only once, even for deterministic rewards. The exploration bonus $c\sqrt{\ln t/N_t(a)}$ shrinks with $N_t(a)$ but never disappears, and it grows (slowly) in $t$; so if $c$ is not chosen tightly relative to the true value gap, a suboptimal action's bonus can grow large enough, as $t$ increases, to make it appear optimistic again relative to the best action — it can be re-selected. (Compare: this is a *true/false, justify* style question that has appeared on the MA338 exam.)

### Practical limitation
UCB's confidence term as stated depends on $t$ and $N_t(a)$ alone (Hoeffding-style bound), which does not extend cleanly to large or continuous state spaces the way [[Nonlinear Functional Approximation|function-approximated]] methods do — it is comparatively tricky to implement in more general RL problems beyond the plain bandit setting.

## See also
[[Multi-armed bandits]], [[Epsilon-greedy exploration]], [[Regret Analysis]], [[Algorithms/n-step SARSA]] (UCT, the tree-search analogue of UCB)
