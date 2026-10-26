---
title: "Fisher Information"
domain: "Probability & Statistics"
course: "Bayesian Statistics"
unit: "Chapter 3 - Bayesian Inference"
level: MSc
status: drafted
confidence: 0
tags: [bayesian-statistics, classical-statistics, foundations]
---
## Definition
For a model with scalar parameter $\theta \in \Theta \subset \mathbb R$, the Fisher information is
$$
I(\theta) = E_{X|\theta}\left[\left(\frac{\partial \log f(X|\theta)}{\partial \theta}\right)^2\right]
$$
Under regularity conditions (allowing differentiation under the integral sign), this equals
$$
I(\theta) = -E_{X|\theta}\left[\frac{\partial^2 \log f(X|\theta)}{\partial \theta^2}\right]
$$
$I(\theta)$ measures the amount of information the data carries about $\theta$: it can be interpreted as the ability of the data to distinguish between $\theta$ and $\theta+d\theta$.

For $\Theta \subset \mathbb R^k$, the Fisher **information matrix** has $(i,j)$-entry
$$
I_{ij}(\theta) = -E_{X|\theta}\left[\frac{\partial^2}{\partial\theta_i\partial\theta_j}\log f(X|\theta)\right]
$$

## Properties
### Reparameterization (chain rule)
If $\tilde\theta = h(\theta)$ for a differentiable $h$, then
$$
I(\theta) = I^*(h(\theta))\left(\frac{dh}{d\theta}\right)^2
$$
where $I^*$ is the Fisher information for $\tilde\theta$. This transformation rule is what makes the [[Jeffrey's prior]] invariant under reparameterization.

### Worked derivation: Binomial Fisher information
For $X\sim\text{Binomial}(n,p)$, $f(x|p)=\binom{n}{x}p^x(1-p)^{n-x}$, so $\log f = \text{const} + x\log p + (n-x)\log(1-p)$ and
$$
\frac{d^2\log f}{dp^2} = -\frac{x}{p^2}-\frac{n-x}{(1-p)^2}
$$
Taking $-E[\cdot]$ and using $E[X]=np$:
$$
I(p) = E\left[\frac{X}{p^2}+\frac{n-X}{(1-p)^2}\right] = \frac{n}{p}+\frac{n}{1-p} = \frac{n}{p(1-p)}
$$

## Examples
The Binomial Fisher information above is used directly in [[Jeffrey's prior]] to derive the Jeffreys prior $\pi(p)\propto[p(1-p)]^{-1/2}$, i.e. $\text{Beta}(0.5,0.5)$.

## See also
[[Jeffrey's prior]], [[Likelihood function]], [[Maximum Likelihood Estimate]]
