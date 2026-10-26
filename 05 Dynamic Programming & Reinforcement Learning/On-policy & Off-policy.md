---
title: On-policy & Off-policy
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: drafted
confidence: 0
tags: [reinforcement-learning, foundations]
---
## Definition
To guarantee every action is tried infinitely often (needed for convergence to $q_*$), an agent must keep selecting non-greedy actions with positive probability. There are two general ways to arrange this:

- **On-policy**: evaluate or improve the policy $\pi$ using experience *sampled from $\pi$ itself*. $\pi$ must therefore be kept "soft" — see below.
- **Off-policy**: evaluate or improve a **target policy** $\pi$ using experience sampled from a different **behaviour policy** $b$. For example, $b$ could be given by a human expert's demonstrations.

## Properties
### Soft policies (needed on-policy)
A policy $\pi$ is **soft** if $\pi(a\mid s) > 0$ for all $s,a$. The canonical soft policy is $\epsilon$-soft: choose an action uniformly at random with probability $\epsilon$ (across all $|\mathcal{A}(s)|$ actions, including the greedy one), and act greedily with the remaining probability, giving each action probability $\tfrac{\epsilon}{|\mathcal{A}(s)|}$ if non-greedy, $1-\epsilon+\tfrac{\epsilon}{|\mathcal{A}(s)|}$ if greedy. See [[Epsilon-greedy exploration]].

### The coverage assumption (needed off-policy)
To use episodes generated under $b$ to estimate values for $\pi$, every action $\pi$ might take must also occasionally be taken under $b$: $\pi(a\mid s) > 0 \implies b(a\mid s) > 0$. It follows that $b$ must be stochastic wherever it differs from $\pi$; $\pi$ itself may be fully deterministic.

### Importance sampling (the standard off-policy tool)
The probability of a trajectory $A_t,S_{t+1},\dots,S_T$ under an arbitrary policy $\mu$ is $\prod_{k=t}^{T-1}\mu(A_k\mid S_k)p(S_{k+1}\mid S_k,A_k)$. The **importance-sampling ratio**
$$\rho_{t:T-1} := \frac{\prod_{k=t}^{T-1}\pi(A_k\mid S_k)}{\prod_{k=t}^{T-1}b(A_k\mid S_k)}$$
depends only on the two policies, *not* on the (generally unknown) transition probabilities $p$, because they appear in both numerator and denominator and cancel. Since $\mathbb{E}[G_t\mid S_t=s] = v_b(s)$ (the "wrong" expectation), importance sampling corrects it: $v_\pi(s) = \mathbb{E}_\pi[\rho_{t:T-1}G_t\mid S_t=s]$. In practice, **weighted importance sampling** (WIS) is used for numerical stability:
$$V_n := \frac{\sum_{k=1}^{n-1}W_kG_k}{\sum_{k=1}^{n-1}W_k}, \qquad V_{n+1} = V_n + \frac{W_n}{C_n}[G_n - V_n],\ C_{n+1}=C_n+W_{n+1}, C_0=0.$$

### Examples of each in the module
- On-policy: [[Algorithms/SARSA|SARSA]] (updates $Q(S_t,A_t)$ using the actually-selected next action $A_{t+1}\sim\pi$).
- Off-policy: [[Algorithms/Q-learning|Q-learning]] (updates using $\max_a Q(S_{t+1},a)$, i.e. the greedy target policy, regardless of which action was actually taken by the exploring behaviour policy).

## See also
[[Epsilon-greedy exploration]], [[Algorithms/SARSA]], [[Algorithms/Q-learning]], [[Monte Carlo Learning]]
