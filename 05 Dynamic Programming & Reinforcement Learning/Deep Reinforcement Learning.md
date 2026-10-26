---
title: Deep Reinforcement Learning
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: drafted
confidence: 0
tags: [reinforcement-learning, deep-rl]
---
## Definition
Deep Reinforcement Learning uses (artificial) neural networks — [[Nonlinear Functional Approximation|non-linear function approximators]] — to represent value functions, policies, or environment models. A neural network is a flexible approximator built by stacking linear and non-linear transformations: $\hat y(x) = \cdots\phi_2(W_2\phi_1(W_1x))$, for activation functions $\phi_i$ and weight matrices $W_i$. Training minimises a loss (typically mean-squared error) via stochastic gradient descent and **backpropagation** (the chain rule applied backward through the layers).

## Properties
### Why linear approximation is often insufficient
Hand-designed linear features require the modeller to explicitly specify how raw problem variables combine. Even simple-looking problems can have genuinely non-linear feature relationships (e.g. three raw features $a,b,c$ with $c=\log(1.2+\sin(\pi(a-b)))$) that a linear combination of $a,b,c$ alone cannot capture, however the individual features are engineered. Neural networks learn the necessary non-linear combinations automatically from data, at the cost of the convergence guarantees enjoyed by linear approximation (see [[Linear MDPs & Linear Functional Approximation]]).

### Convergence/divergence: the precise theoretical picture
- **MC with non-linear approximation**: always converges, but possibly only to a **local** optimum.
- **MC with linear approximation**: converges to the **global** optimum. *Theorem*: for the update $w_{t+1}-w_t=-\alpha_t\mathbb E_\pi[(G_t-v(S_t,w_t))^2]$ with $v(s,w)=x^\top(s)w$, $w\to w_{MC}=\mathbb E[x_tx_t^\top]^{-1}\mathbb E[G_tx_t]$. *Proof sketch*: setting the gradient of the MSE objective to zero, $\nabla_w\mathbb E_\pi[(G_t-x_t^\top w)^2]=0 \Rightarrow \mathbb E_\pi[(G_t-x_tw)x_t]=0 \Rightarrow \mathbb E[x_tx_t^\top]w=\mathbb E[G_tx_t] \Rightarrow w=w_{MC}$. Under mild conditions on $\alpha_t$ (decaying to zero, satisfying Robbins–Monro), this fixed point is reached. Notably $S_t$ need not have the Markov property for this result — the fixed point depends only on the weights and the observed data.
- **TD(0) with linear approximation**: *Theorem*: for $w_{t+1}-w_t=-\alpha_t\mathbb E_\pi[(R_{t+1}+\gamma v(S_{t+1},w_t)-v(S_t,w_t))]\nabla v(S_t,w_t)$, $w\to w_{TD}=\mathbb E[x_t(x_t-\gamma x_{t+1})^\top]^{-1}\mathbb E[R_{t+1}x_t]$. *Proof sketch*: setting $0=w_{t+1}-w_t \Rightarrow \mathbb E_\pi[(R_{t+1}+\gamma x_{t+1}^\top w - x_t^\top w)x_t]=0 \Rightarrow \mathbb E[x_t(x_t-\gamma x_{t+1})^\top]w = \mathbb E[R_{t+1}x_t] \Rightarrow w=w_{TD}$. $w_{TD}=w_{MC}$ only when $\gamma=0$; in general they differ, but $w_{TD}$ is typically preferred for smaller prediction error and faster convergence (n-step/λ variants can be even faster — see [[Algorithms/SARSA(lambda)]]).
- **Off-policy semi-gradient TD(0)**, using importance-sampling ratio $\rho_t=\pi(A_t\mid S_t)/b(A_t\mid S_t)$: even under **linear** approximation, this update ($w_{t+1}=w_t-\alpha_t\rho_t[R_{t+1}+\gamma v(S_{t+1},w_t)-v(S_t,w_t)]\nabla v(S_t,w_t)$) **can diverge** — see [[Nonlinear Functional Approximation]] for the explicit worked counterexample where $\rho_t=1$ throughout but $w_t\to\infty$ for $\gamma>\tfrac12$.

### The Deadly Triad, restated
Bootstrapping + function approximation + off-policy learning together threaten stability; see [[Nonlinear Functional Approximation]] for the full discussion and [[Algorithms/Deep Q-Network]] for the engineering (experience replay, target networks) that lets deep Q-learning survive it in practice.

### Value-based vs. policy-based deep RL
**Value-based** deep RL fits $Q(s,a,w)$ via [[Algorithms/Deep Q-Network|DQN]]-style experience replay and target networks, minimising $l=\left[r+\gamma\max_aQ(s',a,w^-)-Q(s,a,w)\right]^2$. **Policy-based** deep RL parametrises $\pi(a\mid s,\theta)$ directly (see [[Policy Gradient Theorem]]); if used within an [[Algorithms/Actor-Critic|actor-critic]] scheme, the DQN idea (mini-batches, replay) can be reused for the *critic* (policy evaluation), while the *actor* collects the samples stored in the buffer — but this makes the overall scheme off-policy (experience is drawn from a policy different from the one currently being updated), reintroducing the same stability concerns DQN was built to manage.

## See also
[[Nonlinear Functional Approximation]], [[Linear MDPs & Linear Functional Approximation]], [[Algorithms/Deep Q-Network]], [[Algorithms/Double Deep Q-Network]], [[Policy Gradient Theorem]]
