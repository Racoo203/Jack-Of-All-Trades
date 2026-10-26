---
title: Linear MDPs & Linear Functional Approximation
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: drafted
confidence: 0
tags: [reinforcement-learning, function-approximation]
---
## Definition
When state/action spaces are too large for tabular methods (Backgammon: $10^{20}$ states; Go: $10^{170}$; robot control: continuous), value functions are represented **parametrically**: $v(s,w)\approx v_\pi(s)$, $q(s,a,w)\approx q_\pi(s,a)$, where $w$ is fixed-*form* but variable-*value*, with $\dim(w)$ far smaller than $|\mathcal S|$ (or $|\mathcal S|\times|\mathcal A|$). This generalises from seen states to unseen ones and only requires storing the parameters — at the cost of losing the tabular convergence guarantees.

**Linear function approximation** is the special case $v(S,w) = x(S)^\top w = \sum_{j=1}^d x_j(S)w_j$, where $x(S) = (x_1(S),\dots,x_d(S))^\top$ is a hand-designed **feature vector**.

## Properties
### Choosing $w$: the mean-square objective
Given sampled true values $v_\pi(s_k)$, fit $w$ by minimising the sampled Mean-Square Error
$$J(w) = \sum_k\left[v_\pi(x_k)-\hat v(\tilde x_k,w)\right]^2, \qquad w^*=\arg\min_w J(w).$$
This works cleanly for on-policy prediction; the off-policy case is materially harder and prone to divergence (see [[Nonlinear Functional Approximation]]).

### Gradient descent and Stochastic Gradient Descent (SGD)
For differentiable $J(w)$, gradient descent moves $w$ opposite its gradient: $\Delta w := w_{t+1}-w_t = -\tfrac12\alpha\nabla J(w_t)$. Since $\nabla J(w)$ typically requires summing over the whole (possibly infinite) state distribution, **SGD** samples it instead: $\nabla J(w) \approx -2(v_\pi(s)-v(s,w))\nabla v(s,w)$, giving
$$w_{t+1}-w_t = \alpha\left(v_\pi(s_t)-v(s_t,w_t)\right)\nabla v(s_t,w_t).$$
Since $v_\pi(s)$ is generally unknown, it is substituted by the target each algorithm actually has access to:
- **MC**: $w_{t+1}-w_t = \alpha(G_t-v(s_t,w_t))\nabla v(s_t,w_t)$ (Gradient Monte Carlo — same structure as tabular MC, just with a parametric target).
- **TD(0)**: $w_{t+1}-w_t = \alpha(R_{t+1}+\gamma v(s_{t+1},w_t)-v(s_t,w_t))\nabla v(s_t,w_t)$.
- **n-step TD**: replace the target with $G_t^{(n)}$.

### Semi-gradient methods
When bootstrapping (TD, n-step), the "true" target $v_\pi(s_{t+1})$ is itself approximated by $v(s_{t+1},w_t)$ — so the update above is not the *exact* gradient of $J(w)$: the exact gradient of $J(w)\approx[r_{t+1}+\gamma v(s_{t+1},w_t)-v(s_t,w_t)]^2$ would include an extra term $\nabla_w[\gamma v(s_{t+1},w_t)]$, which is dropped by convention (it is small when $\gamma$ is not close to 1, and dropping it is computationally cheaper). The resulting update, $\nabla_wJ(w)\approx -[r_{t+1}+\gamma v(s_{t+1},w_t)-v(s_t,w_t)]\nabla_wv(s_t,w_t)$, is called a **semi-gradient** — used for both TD(0) and n-step TD.

### The linear case: convexity and its consequence for $\nabla v$
If $v(s,w)$ is linear in $w$, $J(w)$ is convex: the local optimum equals the global optimum and is uniquely discoverable — the "nice case". If $v$ is non-linear, $J(w)$'s optimisation landscape can have multiple local optima with no guarantee of reaching the global one — the "ugly case" — and the RL algorithm may diverge depending on the optimisation strategy used (see [[Nonlinear Functional Approximation]]). Because $v(S,w)=x(S)^\top w$ is linear, $\nabla_w v(s,w) = \nabla_w[x(s)^\top w] = x(s)$ — the gradient is simply the feature vector, independent of $w$ — so the Gradient MC update simplifies to $w_{t+1}-w_t = \alpha_t(G_t-v(s_t,w_t))x_t$.

### Convergence guarantees under linear approximation
MC with linear approximation converges to the **global optimum** $w_{MC} = \mathbb E[x_tx_t^\top]^{-1}\mathbb E[G_tx_t]$ (derived by setting $\nabla_wJ(w)=0$). Semi-gradient TD(0) with linear approximation converges to a *different* fixed point $w_{TD}=\mathbb E[x_t(x_t-\gamma x_{t+1})^\top]^{-1}\mathbb E[R_{t+1}x_t]$, which coincides with $w_{MC}$ only when $\gamma=0$; $w_{TD}$ is not the global MSE optimum in general, but is preferred in practice for faster convergence and lower prediction error. See [[Deep Reinforcement Learning]] for the full convergence proof sketches.

### Feature selection
There is no universal recipe; a common approach for continuous state spaces is discretisation-based features (tile coding), with the granularity/shape of the tiling (irregular, log-stripe, diagonal-stripe) itself a design choice affecting generalisation.

### Control with linear function approximation
Two conventions for representing $q(s,a,w)$: **state-action features**, $q(s,a,w)=x(s,a)^\top w$ ("action-in": a single weight vector shared across actions, so no extra training needed per action, easier for continuous action spaces); or **state features per action**, $q(s,a,w)=x(s)^\top w_a$ ("action-out": separate weight vectors $w_a$ per discrete action, updating only $w_a$ for the taken action and leaving $w_b, b\ne a$ unchanged — reuses the same features across actions, preferable for discrete action spaces).

## See also
[[Nonlinear Functional Approximation]], [[Deep Reinforcement Learning]], [[Algorithms/Deep Q-Network]], [[Policy Gradient Theorem]]
