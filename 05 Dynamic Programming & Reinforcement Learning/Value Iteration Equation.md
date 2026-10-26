---
title: Value Iteration Equation
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: drafted
confidence: 0
tags: [reinforcement-learning, dynamic-programming]
---
## Definition
Value iteration combines one sweep of [[Dynamic programming|policy evaluation]] and one sweep of policy improvement into a single update, by truncating policy evaluation to just one sweep before re-improving:
$$v_{k+1}(s) = \max_a \mathbb E[R_{t+1}+\gamma v_k(S_{t+1})\mid S_t=s,A_t=a] = \max_a \sum_{s',r}p(s',r\mid s,a)\left[r+\gamma v_k(s')\right].$$
For arbitrary $v_0$, $\{v_k\} \to v_*$ (given $\gamma<1$ or $T<\infty$).

## Properties
### Derivation: replacing the policy sum with a max
Ordinary policy evaluation updates via $v_{k+1}(s)=\sum_a\pi(a\mid s)\sum_{s',r}p(s',r\mid s,a)[r+\gamma v_k(s')]$. If, instead of evaluating a *fixed* $\pi$, the policy is re-selected greedily at every single sweep (i.e. policy improvement is performed after *every* evaluation sweep, rather than only after full convergence), the weighted sum over actions $\sum_a\pi(a\mid s)(\cdots)$ collapses to a $\max_a(\cdots)$, since the greedy policy places all its probability mass on the maximising action. This yields exactly the Bellman *optimality* equation turned into an update rule.

### Pseudocode
```
Input: threshold θ>0
Init: V(s) arbitrary, V(terminal)=0, Δ=θ+1
while Δ > θ:
    for each s:
        v ← V(s)
        V(s) ← max_a Σ_{s',r} p(s',r|s,a)[r + γV(s')]
        Δ ← max(Δ, |v - V(s)|)
Output: π(s) = argmax_a Σ_{s',r} p(s',r|s,a)[r + γV(s')]
```

### Relation to Generalised Policy Iteration (GPI)
Value iteration is one extreme of GPI (evaluation truncated to a single sweep); [[Dynamic programming|policy iteration]] is the other (evaluation run to convergence before each improvement). Intermediate variants — multiple evaluation sweeps between improvements — are also valid instances of GPI and can converge faster than either extreme in practice.

### Convergence and cost per sweep
Each sweep of value iteration costs the same as one sweep of ordinary policy evaluation, but folds in an implicit improvement step (via the $\max$), so no separate "policy stable?" check across full-evaluation cycles is needed — the trade-off is that a single value-iteration sweep does strictly more work per state (a $\max$ over all actions, rather than a weighted sum) than a policy-evaluation sweep for a fixed policy.

## Examples
4×4 Gridworld: with $v_0(s)=0$ and reward $-1$ per step, value iteration's greedy policy is already optimal after $k=3$ sweeps, even though $v_k$ has not yet converged numerically to $v_*$ (see [[Dynamic programming]]).

## See also
[[Dynamic programming]], [[Bellman equation]], [[State value function]], [[Markov Decision Process]]
