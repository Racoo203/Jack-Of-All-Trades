---
title: "Jeffrey's prior"
domain: "Probability & Statistics"
course: "Bayesian Statistics"
unit: "Chapter 3 - Bayesian Inference"
level: MSc
status: drafted
confidence: 0
tags: [bayesian-statistics, non-informative-prior]
---
## Definition
The Jeffreys prior for a scalar parameter $\theta$ is defined to be proportional to the square root of the [[Fisher Information]]:
$$
\pi(\theta) \propto I(\theta)^{1/2}
$$
For a vector parameter $\theta \in \mathbb R^k$, it generalizes to
$$
\pi(\theta) \propto [\det(I(\theta))]^{1/2}
$$
It is a **non-informative prior**: rather than being flat in an arbitrary parameterization (which is not itself invariant — e.g. $p\sim U[0,1]$ implies $\sqrt p$ is *not* uniform), the Jeffreys prior is constructed to be consistent across reparameterizations.

## Properties
### Invariance under reparameterization
If $h$ is a monotone differentiable function of $\theta$ and $\tilde\theta=h(\theta)$, the prior induced on $\tilde\theta$ by transforming the Jeffreys prior on $\theta$ is
$$
\pi^*(h(\theta)) = \pi(\theta)\left|\frac{dh}{d\theta}\right|^{-1} \propto I(\theta)^{1/2}\left|\frac{dh}{d\theta}\right|^{-1} = I^*(h(\theta))^{1/2}
$$
using the [[Fisher Information]] transformation rule $I(\theta)=I^*(h(\theta))\left(\frac{dh}{d\theta}\right)^2$. This is exactly the Jeffreys prior for $\tilde\theta$ directly — i.e. "Jeffreys prior, then transform" gives the same answer as "transform, then take Jeffreys prior."

### Worked example: Binomial
For $X\sim\text{Binomial}(n,p)$, $I(p)=\frac{n}{p(1-p)}$ (see [[Fisher Information]]), so
$$
\pi(p) \propto [p(1-p)]^{-1/2}
$$
which is the (proper) $\text{Beta}(0.5,0.5)$ density.

### Worked example: Normal($\mu,\sigma^2$)
With $\theta=(\mu,\sigma)$:
$$
\log f(x|\mu,\sigma^2) = -\frac{1}{2\sigma^2}(x-\mu)^2 - \log\sigma
$$
$$
\frac{\partial^2\log f}{\partial\mu^2} = -\frac{1}{\sigma^2}, \quad
\frac{\partial^2\log f}{\partial\sigma^2} = -3\sigma^{-4}(x-\mu)^2+\sigma^{-2}, \quad
\frac{\partial^2\log f}{\partial\mu\,\partial\sigma} = -2\sigma^{-3}(x-\mu)
$$
Taking expectations (using $E[(x-\mu)^2]=\sigma^2$, $E[x-\mu]=0$):
$$
I(\theta) = \begin{pmatrix}\sigma^{-2} & 0 \\ 0 & 2\sigma^{-2}\end{pmatrix}, \qquad \pi(\theta) \propto \det(I(\theta))^{1/2} \propto \sigma^{-2}
$$

## See also
[[Fisher Information]], [[Prior distribution]], [[Posterior distribution]]
