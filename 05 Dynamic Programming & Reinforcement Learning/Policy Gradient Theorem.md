---
title: Policy Gradient Theorem
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: drafted
confidence: 0
tags: [reinforcement-learning, policy-gradient]
---
## Definition
For a parametrised, differentiable policy $\pi(a\mid s,\theta)$ and a scalar objective $J(\theta)$ measuring its quality, the **policy gradient theorem** gives
$$\nabla J(\theta) = \mathbb E_\pi\left[q_\pi(s,a)\,\frac{\nabla\pi(a\mid s,\theta)}{\pi(a\mid s,\theta)}\right] = \mathbb E_\pi\left[q_\pi(s,a)\,\nabla\ln\pi(a\mid s,\theta)\right],$$
using the log-derivative identity $\nabla\ln f = \nabla f/f$. The quantity $\nabla\ln\pi(a\mid s,\theta)$ is called the **score function**. Crucially, $\nabla J(\theta)$ does **not** depend on the state distribution (only on the policy and $q_\pi$), so this gradient can be estimated **model-free** — no knowledge of the environment's dynamics is required, only a differentiable policy.

## Properties
### Setting up the objective $J(\theta)$
Without a value function to directly optimise, policy quality must be measured some other way. Two standard choices: for **episodic tasks**, the *episodic-return objective* $J(\theta):=v_{\pi_\theta}(s_0)=\mathbb E[v\mid S=s_0,\theta]$; for **continuing tasks**, the *average-reward objective* $J(\theta):=\bar r_{\pi_\theta}=\mathbb E_{\pi_\theta}[R_{t+1}]$. Either way, policy-based RL reduces to an optimisation problem over $\theta$, which is generally non-linear, multi-dimensional, and non-stationary — candidate solution methods range from heuristics (hill-climbing, simulated annealing) and meta-heuristics (evolutionary algorithms) to **gradient-based** techniques (stochastic gradient ascent), the latter preferred for their theoretical properties, efficiency, and compatibility with neural-network policies.

### Gradient ascent update
$$\Delta\theta := \theta_{t+1}-\theta_t = \alpha\nabla J(\theta_t), \qquad \theta_{t+1}=\theta_t+\alpha\,\mathbb E_\pi\left[q_\pi(S_t,A_t)\frac{\nabla\pi(A_t\mid S_t,\theta_t)}{\pi(A_t\mid S_t,\theta_t)}\right].$$
The numerator pushes $\theta$ toward increasing the probability of high-value actions; the denominator normalises by how often each action is already selected, preventing the update from being dominated purely by frequently-taken actions.

### Discrete-action policies: softmax
$$\pi(a\mid s,\theta) = \frac{e^{h(a,s,\theta)}}{\sum_{b\in\mathcal A}e^{h(b,s,\theta)}},$$
with a preference function $h(a,s,\theta):\mathcal A\times\mathcal S\times\mathbb R^d\to\mathbb R$, often linear: $h(a,s,\theta)\approx\theta^\top x(a,s)$. In the limit this represents deterministic behaviour, but for finite $\theta$ it is genuinely stochastic — see [[Deterministic & Stochastic policies]] for why this matters beyond mere exploration.

### Continuous-action policies: Gaussian
For a single continuous action $a\in\mathbb R$:
$$\pi(a\mid s,\theta) = \frac{1}{\sigma(s,\theta)\sqrt{2\pi}}\exp\left(-\frac{(a-\mu(s,\theta))^2}{2\sigma(s,\theta)^2}\right),$$
with mean $\mu(s,\theta)$ and standard deviation $\sigma(s,\theta)$ themselves parametric functions (e.g. neural-network outputs, sharing $\theta$ or parametrised independently $\theta=[\theta_\mu,\theta_\sigma]^\top$). Multi-dimensional continuous actions extend naturally via the multivariate Gaussian.

## Examples
The gridworld example from [[Dynamic programming]] illustrates the case for policy-based methods qualitatively: while $v_k$ under value iteration only converges numerically in the limit, the corresponding *policy* stabilises after just 3 iterations — suggesting that, in complex dynamics, values can be harder to pin down than the policy they induce, motivating optimising the policy directly.

## See also
[[Policy-based]], [[Algorithms/REINFORCE]], [[Algorithms/Actor-Critic]], [[Deterministic & Stochastic policies]]
