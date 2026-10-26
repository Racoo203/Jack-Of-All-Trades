---
title: Actor-Critic
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
unit: Algorithms
level: MSc
status: drafted
confidence: 0
tags: [reinforcement-learning, policy-gradient, algorithms, td-learning]
---
## Definition
Actor-Critic methods extend [[Algorithms/REINFORCE|REINFORCE with baseline]] by using the learned state-value function not merely as a variance-reducing baseline, but to actually **bootstrap** the return target — replacing the full Monte Carlo return $G_t$ with a one-step (or n-step) TD target. This requires **both** a policy (the **actor**, updated by policy gradient — analogous to policy improvement) and a value function (the **critic**, updated by TD — analogous to policy evaluation), hence the name.

## Properties
### Why REINFORCE-with-baseline is not quite Actor-Critic
In REINFORCE with baseline, the learned $V(s,w)$ estimates only the value of the trajectory's **first** state $S_t$ — it sets a baseline for the subsequent return, computed *before* the transition's action is taken, and so cannot itself assess the quality of that action. If instead $V$ is also applied to the *second* state of the transition — e.g. via the one-step target $G_t^{(1)}=R_{t+1}+\gamma v(S_{t+1},w)$ — then the value function is being used to assess the *effect* of the action just taken. When $V$ is used this way, it is called a **critic**, and the overall method an **actor-critic** method.

### One-step Actor-Critic update
Replacing REINFORCE's full return $G_k$ with the one-step return (and using the learnt state-value function as the baseline simultaneously):
$$\theta_{k+1} = \theta_k + \alpha\gamma^k\left(R_{k+1}+\gamma v(S_{k+1},w)-v(S_k,w)\right)\nabla\ln\pi(A_k\mid S_k,\theta_k).$$
The bracketed term is exactly the TD error $\delta_k$ (see [[Temporal-Difference Learning]]). The **critic** updates $w$ by TD(0), n-step TD, or TD(λ) (essentially [[Linear MDPs & Linear Functional Approximation|policy evaluation]]); the **actor** updates $\theta$ by the policy gradient above (essentially policy improvement) — directly paralleling the evaluate/improve structure of Generalised Policy Iteration, but now for parametric policies and value functions simultaneously.

### Pseudocode (episodic, TD(0) critic)
```
Input: differentiable π(a|s,θ), differentiable V(s,w); step sizes αw, αθ
Init: w, θ arbitrary
for each episode:
    initialise s0
    for k = 0,...,T-1:
        apply ak ~ π(·|sk,θk); observe sk+1, rk+1
        wk+1 ← wk + αw [rk+1 + γV(sk+1,wk) - V(sk,wk)] ∇w V(sk,wk)
        θk+1 ← θk + αθ γ^k [rk+1 + γV(sk+1,wk) - V(sk,wk)] ∇θ ln π(ak|sk,θk)
```

### Why one-step Actor-Critic is preferable in practice
It is fully **online and incremental** — states, actions, and rewards are processed as they occur and never revisited — unlike REINFORCE (Monte Carlo, must wait for episode termination). The generalisation to n-step targets is direct: replace the one-step return with $G_t^{(n)}=R_{t+1}+\gamma R_{t+2}+\cdots+\gamma^n v(S_{t+n},w)$, with everything else unchanged.

### Continuous-control descendants
Modern actor-critic algorithms build directly on this skeleton for continuous/high-dimensional action spaces: [[Algorithms/DDPG|DDPG]] (deterministic actor + Q-critic, off-policy), [[Algorithms/Proximal Policy Optimization|PPO]] and [[Algorithms/Trust Region Policy Optimization|TRPO]] (constrained/clipped policy updates for stability, typically on-policy).

## See also
[[Algorithms/REINFORCE]], [[Policy Gradient Theorem]], [[Temporal-Difference Learning]], [[Algorithms/DDPG]], [[Algorithms/Proximal Policy Optimization]]
