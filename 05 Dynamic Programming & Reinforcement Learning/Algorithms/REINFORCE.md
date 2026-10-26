---
title: REINFORCE
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
unit: Algorithms
level: MSc
status: drafted
confidence: 0
tags: [reinforcement-learning, policy-gradient, algorithms, monte-carlo]
---
## Definition
REINFORCE (also called *vanilla policy gradient*) is the Monte Carlo instantiation of the [[Policy Gradient Theorem]]: rather than requiring the true $q_\pi(s,a)$ and an expectation over $\pi$, it approximates $q_\pi(s,a)$ by the **sampled episodic return** $G_k$ from a generated episode, and uses that as a stochastic estimate of the gradient:
$$\theta_{k+1} = \theta_k + \alpha\gamma^k G_k\,\nabla\ln\pi(a_k\mid s_k,\theta_k).$$

## Properties
### Pseudocode
```
Input: differentiable policy π(a|s,θ); step size α
Init: θ ∈ R^d arbitrary
for each episode:
    generate episode s0,a0,r1,...,sT following π(·|·,θ)
    for k = 0,...,T-1:
        gk ← Σ_{i=k+1}^{T} γ^{i-k-1} ri
        θk+1 ← θk + α γ^k gk ∇θ ln π(ak|sk,θk)
```
Since $\mathbb E_\pi[q_\pi(s,a)\nabla\ln\pi(a\mid s,\theta)] = \nabla J(\theta)$ and $G_k$ is an unbiased sample of $q_\pi(s_k,a_k)$, REINFORCE performs unbiased **stochastic gradient ascent** on $J(\theta)$.

### High variance is the central weakness
Like tabular Monte Carlo, REINFORCE suffers from high variance in its updates (a single episode's return is a noisy estimate of $q_\pi$) and correspondingly slow learning. On the short-corridor gridworld benchmark, total reward per episode (averaged over 100 runs) approaches the optimal value $v_*(s_0)$ only gradually, and the achievable learning rate is highly sensitive to step size $\alpha$.

### Differentiability is required — a recurring exam point
Because the update depends on $\nabla\ln\pi(a\mid s,\theta)$, REINFORCE can only be applied to **differentiable** policies. A discontinuous/non-differentiable policy (e.g. a hard step-function threshold policy $\sigma(x)=0$ for $x\le 0.5$, $\sigma(x)=1$ for $x>0.5$) has no well-defined gradient at the discontinuity, so REINFORCE cannot directly improve it — this is a standard true/false exam question (see the MOC's Exam focus).

### Baselines reduce variance without introducing bias
Subtracting a state-dependent (not action-dependent) **baseline** $b(s)$ leaves the expectation unchanged: $\mathbb E_\pi[b(s)\nabla\ln\pi(a\mid s,\theta)]=0$, since $\sum_a\nabla\pi(a\mid s,\theta) = \nabla\sum_a\pi(a\mid s,\theta)=\nabla 1 = 0$ and $b(s)$ can be pulled out of the sum over $a$. So
$$\nabla J(\theta) = \mathbb E_\pi\left[(q_\pi(s,a)-b(s))\nabla\ln\pi(a\mid s,\theta)\right], \qquad \theta_{k+1}=\theta_k+\alpha\gamma^k(G_k-b(s_k))\nabla\ln\pi(a_k\mid s_k,\theta_k).$$
A natural choice is $b(s)=v_\pi(s)$, itself estimated by a second, separately-learned parameter vector $w$ (via Monte Carlo regression), giving **REINFORCE with baseline**:
```
Init: w ∈ R^dw, θ ∈ R^dθ arbitrary; step sizes αw, αθ
for each episode:
    generate episode following π(·|·,θ)
    for k = 0,...,T-1:
        gk ← Σ_{i=k+1}^T γ^{i-k-1} ri
        wk+1 ← wk + αw [gk - V(sk,wk)] ∇w V(sk,wk)
        θk+1 ← θk + αθ γ^k [gk - V(sk,wk)] ∇θ ln π(ak|sk,θk)
```
On the same short-corridor benchmark, adding a baseline lets the algorithm learn much faster than plain REINFORCE — the trade-off is learning two sets of parameters ($w$ and $\theta$) instead of one, and there is no universally-best baseline choice — each RL method tends to have its own preferred one.

## Examples
See [[Policy Gradient Theorem]] for the softmax/Gaussian policy forms REINFORCE is typically paired with, and [[Algorithms/Actor-Critic]] for the natural next step: replacing the Monte Carlo return $G_k$ with a bootstrapped one-step estimate.

## See also
[[Policy Gradient Theorem]], [[Algorithms/Actor-Critic]], [[Monte Carlo Learning]], [[Mean-square Sample Complexity]]
