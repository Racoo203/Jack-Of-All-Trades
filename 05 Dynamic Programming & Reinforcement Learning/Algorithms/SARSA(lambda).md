---
title: "SARSA(λ)"
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
unit: Algorithms
level: MSc
status: drafted
confidence: 0
tags: [reinforcement-learning, td-learning, algorithms, on-policy, eligibility-traces]
---
## Definition
SARSA(λ) replaces [[Algorithms/n-step SARSA|n-step SARSA]]'s fixed, hard commitment to a single $n$ with a **weighted combination of all n-step returns**, controlled by a trace-decay parameter $\lambda \in [0,1]$, while avoiding the delay and memory cost of storing $n$ steps explicitly — via a backward-view mechanism called an **eligibility trace**.

## Properties
### The λ-return (forward view)
A convex combination of n-step returns, weighted by $\lambda^{n-1}$ and normalised by $(1-\lambda)$ so the weights sum to 1:
$$G_t^\lambda := (1-\lambda)\sum_{n=1}^\infty \lambda^{n-1}G_t^{(n)},$$
or, separating pre- and post-termination terms explicitly for an episode ending at $T$:
$$G_t^\lambda = (1-\lambda)\sum_{n=1}^{T-t-1}\lambda^{n-1}G_t^{(n)} + \lambda^{T-t-1}G_t.$$
Special cases: $\lambda=1$ gives $G_t^1=G_t$, the plain [[Monte Carlo Learning|MC]] return; $\lambda=0$ gives $G_t^0=G_t^{(1)}=R_{t+1}+\gamma Q(S_{t+1},A_{t+1})$, the [[Algorithms/SARSA|TD(0)/SARSA]] target. The forward view "looks ahead" from each visited state to all future rewards — conceptually clean, but requires knowing the whole future, which is impractical to implement directly online.

### Eligibility traces (backward view)
The backward view achieves the *same* update using only information available up to the current step, via a trace vector $e_t \in \mathbb R^d$ (matching the dimension of the weight vector $w_t$, or for the tabular case, one scalar per state-action pair), updated recursively:
$$e_0 = 0, \qquad e_t = \gamma\lambda e_{t-1} + \nabla_w Q(S_t,A_t,w_t).$$
$e_t$ tracks how much each component of $w$ has contributed to *recently visited* state-action pairs: $w_t$ is a long-term memory (spanning the whole episode), while $e_t$ is a short-term memory that fades geometrically at rate $\gamma\lambda$. The backward-view weight update is then
$$w_{t+1} = w_t + \alpha\, e_t\left[R_{t+1}+\gamma Q(S_{t+1},A_{t+1},w_t) - Q(S_t,A_t,w_t)\right],$$
i.e. the ordinary one-step TD error, but applied to **every** state-action pair proportionally to its current eligibility, not just the most recently visited one. Forward and backward views are mathematically equivalent formulations of the same $\lambda$-return target.

### Semi-gradient SARSA(λ) pseudocode
```
Parameters: α ∈ (0,1], λ ∈ [0,1], small ε>0
Init: w ∈ R^d arbitrary
initialise s0, e=0
a0 ← π(s0) or ε-greedy on Q(s0,·,w)
for k = 0,1,2,...:
    ek ← γλ e_{k-1} + ∇w Q(sk,ak,wk)
    apply ak, observe sk+1, rk+1
    if sk+1 not terminal:
        ak+1 ← π(sk+1) or ε-greedy on Q(sk+1,·,wk)
        wk+1 ← wk + α[rk+1 + γQ(sk+1,ak+1,wk) - Q(sk,ak,wk)] ek
    else:
        wk+1 ← wk + α[rk+1 - Q(sk,ak,w)] ek
    if sk+1 terminal: break
```

### Why eligibility traces outperform fixed-n methods
$\lambda$ can be interpreted as a discounting factor acting on the eligibility trace itself, with an intuitive reading: more recent transitions are more relevant to the current update. Empirically (Mountain Car), SARSA(λ) with an intermediate $\lambda$ learns **significantly faster** than any fixed-$n$ n-step SARSA variant, because a single trace-based update simultaneously spreads credit across *all* recently visited state-action pairs (fading with recency), rather than the fixed last-$n$ window that n-step methods use. **True Online TD(λ)/SARSA(λ)** (Lecture IV-PGT) is a refinement matching the *exact* forward-view λ-return online, correcting a subtle inexactness in the standard backward-view implementation.

## Examples
On Mountain Car, the early-performance comparison (steps per episode over the first 50 episodes, averaged over 100 runs) shows accumulating-trace and replacing-trace SARSA(λ) both outperforming plain $n$-step SARSA across a wide range of step sizes, with intermediate $\lambda$ (not $\lambda=0$ or $\lambda=1$) best.

## See also
[[Algorithms/n-step SARSA]], [[Algorithms/SARSA]], [[Temporal-Difference Learning]], [[Nonlinear Functional Approximation]], [[Rate of Convergence]]
