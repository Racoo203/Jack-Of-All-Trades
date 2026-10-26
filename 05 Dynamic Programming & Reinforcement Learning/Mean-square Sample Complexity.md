---
title: Mean-square Sample Complexity
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: seeding
confidence: 0
tags: [reinforcement-learning, theory]
---
## Definition
<!-- UNVERIFIED: check against a dedicated RL-theory reference; not covered in the MA338 slide decks -->
**Mean-square sample complexity** is the number of samples $n$ needed so that an estimator's *mean squared error* (MSE) against the true target falls below a threshold $\epsilon$:
$$\mathbb{E}\left[(\hat\theta_n - \theta)^2\right] \le \epsilon.$$
This differs from the PAC-style [[Sample Complexity]] criterion (a *high-probability* bound on the error, $\Pr[|\hat\theta_n-\theta|>\epsilon]\le\delta$) by instead bounding the *expected squared* error directly — a criterion more natural when the estimator (e.g. a value function fit by [[Linear MDPs & Linear Functional Approximation|linear regression]] or SGD) is itself explicitly optimising a mean-square objective $J(w)=\sum_k[v_\pi(x_k)-\hat v(x_k,w)]^2$, as in this module's function-approximation lectures.

## Properties
### Bias–variance decomposition
For an estimator $\hat\theta_n$ of $\theta$,
$$\mathbb{E}[(\hat\theta_n-\theta)^2] = \underbrace{\left(\mathbb{E}[\hat\theta_n]-\theta\right)^2}_{\text{bias}^2} + \underbrace{\mathrm{Var}(\hat\theta_n)}_{\text{variance}}.$$
This decomposition is exactly what separates $w_{MC}$ (unbiased, higher variance) from $w_{TD}$ (biased by bootstrapping, typically lower variance) under linear function approximation — see [[Asymptotic Convergence]] — and is the same logic behind adding a [[Algorithms/REINFORCE|baseline]] to REINFORCE: baselines reduce variance without introducing bias, directly lowering mean-square sample complexity for a fixed accuracy target.

### Scaling with $1/\epsilon$
For an unbiased estimator with bounded variance $\sigma^2$, the sample-average estimator's MSE is $\sigma^2/n$, so mean-square sample complexity scales as $n = O(\sigma^2/\epsilon)$ — a factor of $1/\epsilon$, sharper than the $1/\epsilon^2$ scaling of the high-probability PAC bound in [[Sample Complexity]] for the *same* $\epsilon$, precisely because MSE is a weaker (average-case, not worst-case-with-confidence) guarantee.

## See also
[[Sample Complexity]], [[Sample Complexity of Exploration]], [[Linear MDPs & Linear Functional Approximation]], [[Algorithms/REINFORCE]]
