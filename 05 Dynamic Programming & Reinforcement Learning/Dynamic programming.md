---
title: Dynamic programming
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: drafted
confidence: 0
tags: [reinforcement-learning, dynamic-programming]
---
## Definition
Dynamic Programming (DP) is a collection of algorithms for computing optimal policies given a complete model of the environment (a finite [[Markov Decision Process]] with known $p(s',r\mid s,a)$). The key idea: use value functions to organise and structure the search for good policies, since once the optimal value function ($v_*$ or $q_*$) is known, the optimal policy is obtained by acting greedily with respect to it. DP turns the [[Bellman equation]] into an *iterative update rule* that provably converges to the desired value function.

Two related problems recur throughout: the **prediction problem** (evaluate a fixed policy $\pi$ via its value function) and the **control problem** (improve $\pi$, under some criterion, until it is optimal).

## Properties
### Policy Evaluation (prediction)
Given a fixed $\pi$, define the sequence of successive approximations $v_0,v_1,\dots$ via the update rule
$$v_{k+1}(s) = \mathbb E_\pi[R_{t+1}+\gamma v_k(S_{t+1})\mid S_t=s] = \sum_a\pi(a\mid s)\sum_{s',r}p(s',r\mid s,a)\left[r+\gamma v_k(s')\right],$$
called a **sweep**. $v_\pi$ is a fixed point of this update, and $\{v_k\}\to v_\pi$ as $k\to\infty$ (given $\gamma<1$ or $T<\infty$) — this is **Iterative Policy Evaluation**.
```
Input: policy π, threshold θ>0
Init: V(s) arbitrary, V(terminal)=0, Δ=θ+1
while Δ > θ:
    for each s:
        v ← V(s)
        V(s) ← Σ_a π(a|s) Σ_{s',r} p(s',r|s,a)[r + γV(s')]
        Δ ← max(Δ, |v - V(s)|)
```

### Policy Improvement (control, step 1)
Consider a deterministic $\pi$ with value functions $v_\pi,q_\pi$. **Policy Improvement Theorem**: if $\pi,\pi'$ are deterministic policies with $q_\pi(s,\pi'(s)) \ge v_\pi(s)$ for all $s$, then $\pi'$ is at least as good as $\pi$ everywhere: $v_{\pi'}(s)\ge v_\pi(s)\ \forall s$ (strictly better wherever the inequality is strict). Building the **greedy** policy
$$\pi'(s) = \arg\max_a q_\pi(s,a) = \arg\max_a\sum_{s',r}p(s',r\mid s,a)[r+\gamma v_\pi(s')]$$
automatically satisfies the theorem's hypothesis (since $q_\pi(s,\pi'(s))=\max_a q_\pi(s,a)\ge q_\pi(s,\pi(s))=v_\pi(s)$), so it is guaranteed to be as good as, or better than, $\pi$. This process — making a new policy greedy with respect to the *old* policy's value function — is **policy improvement**. If $v_{\pi'}=v_\pi$ after an iteration, both are optimal and the process stops. This result holds identically for stochastic policies.

### Policy Iteration
Chaining evaluation ($\to_E$) and improvement ($\to_I$) steps: $\pi_0 \to_E v_{\pi_0} \to_I \pi_1 \to_E v_{\pi_1} \to_I \cdots \to \pi^* \to_E v_{\pi^*}$. In a finite MDP with finitely many deterministic policies, this process provably terminates in a finite number of steps (and in practice, not many).

### Value Iteration
Policy iteration's evaluation step can itself be expensive (many sweeps needed for exact convergence). **Value iteration** truncates policy evaluation to a *single* sweep per improvement, combining evaluation and improvement into one update — see [[Value Iteration Equation]] for the full statement and derivation. In the 4×4 Gridworld running example, the *policy* implied by $v_k$ stabilises after only $k=3$ iterations, even though $v_k$ itself only converges to $v_\pi$ in the limit — illustrating that truncated evaluation loses nothing for the purposes of control. This truncate-and-still-converge idea generalises to **Generalised Policy Iteration (GPI)**: any interleaving of (partial) evaluation and (partial) improvement steps, of which policy iteration and value iteration are the two extremes.

### (In)efficiency
In the worst case, DP methods find an optimal policy in time polynomial in $|\mathcal S|$ and $|\mathcal A|$ — exponentially better than a direct/brute-force search over policies (which is exponential in $|\mathcal S|$), even though DP is sometimes dismissed as suffering from the "curse of dimensionality". Both policy iteration and value iteration are widely used; it is not clear which is better in general, and in practice both converge much faster than their theoretical worst-case bounds, especially from good initial estimates. DP's principal limitation is not its complexity class but its **assumption of full knowledge of the environment**, which almost never holds in practice — the motivation for [[Monte Carlo Learning]] and [[Temporal-Difference Learning]].

## Examples
4×4 Gridworld: 14 non-terminal states, reward $-1$ per step, 4 actions, equiprobable random initial policy, $v_0(s)=0$ everywhere. After $k=3$ iterations of the Bellman update, the greedy policy with respect to $v_3$ is already optimal, though $v_k\to v_\pi$ only as $k\to\infty$.

## See also
[[Value Iteration Equation]], [[Bellman equation]], [[Markov Decision Process]], [[Monte Carlo Learning]], [[Model-free & Model-based]]
