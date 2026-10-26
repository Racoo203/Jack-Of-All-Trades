---
title: "Posterior predictive distribution"
domain: "Probability & Statistics"
course: "Bayesian Statistics"
unit: "Chapter 3 - Bayesian Inference"
level: MSc
status: drafted
confidence: 0
tags: [bayesian-statistics, foundations]
---
## Definition
Given observed data $x_1$, the posterior predictive distribution for a new, conditionally-independent observation $x_2$ is obtained by integrating the model against the [[Posterior distribution]] $\pi(\theta|x_1)$:
$$
p(x_2|x_1) = \int_\Theta f(x_2|\theta)\,\pi(\theta|x_1)\,d\theta
$$

## Properties
### Derivation
Starting from the definition of conditional probability and the [[Prior predictive distribution]] $p(x_1)=\int f(x_1|\theta)\pi(\theta)\,d\theta$:
$$
p(x_2|x_1) = \frac{p(x_2,x_1)}{p(x_1)} = \frac{\int f(x_2,x_1|\theta)\pi(\theta)\,d\theta}{\int f(x_1|\theta)\pi(\theta)\,d\theta}
= \int f(x_2|\theta,x_1)\left\{\frac{f(x_1|\theta)\pi(\theta)}{\int f(x_1|\theta)\pi(\theta)\,d\theta}\right\}d\theta
$$
Using conditional independence of $x_1,x_2$ given $\theta$ ($f(x_2|\theta,x_1)=f(x_2|\theta)$), and recognising the term in braces as $\pi(\theta|x_1)$:
$$
p(x_2|x_1) = \int_\Theta f(x_2|\theta)\,\pi(\theta|x_1)\,d\theta
$$
Note $x_1,x_2$ need not be *unconditionally* independent — only conditionally independent given $\theta$.

## Examples
### Worked derivation: Binomial with uniform prior
Given $x_1$ successes in $n$ Binomial trials with a uniform prior on $p$ (posterior $\text{Beta}(x_1+1,n-x_1+1)$, see [[Conjugate prior]]), the posterior predictive probability that the next trial succeeds is
$$
P[X=1|x_1] = \int_0^1 p \cdot \frac{p^{x_1}(1-p)^{n-x_1}}{B(x_1+1,n-x_1+1)}\,dp = \frac{B(x_1+2,n-x_1+1)}{B(x_1+1,n-x_1+1)} = \frac{x_1+1}{n+2}
$$
Compare with the classical [[Maximum Likelihood Estimate]] $\hat p = x_1/n$: the two are close for large $n$, but for small $n$ the Bayesian predictive probability is never exactly $0$ or $1$ even if $x_1=0$ or $x_1=n$ — a useful regularizing property for small samples.

### Worked derivation: Poisson with Gamma prior
For $X\sim\text{Poisson}(\lambda)$ with conjugate prior $\lambda\sim\text{Gamma}(\alpha,\beta)$ ($\alpha$ integer), the (prior) predictive distribution is
$$
p(x) = \int \frac{\lambda^x e^{-\lambda}}{x!}\cdot\frac{\beta^\alpha\lambda^{\alpha-1}e^{-\beta\lambda}}{\Gamma(\alpha)}\,d\lambda
= \frac{\beta^\alpha}{x!\,\Gamma(\alpha)}\int \lambda^{x+\alpha-1}e^{-(\beta+1)\lambda}\,d\lambda
= \binom{\alpha+x-1}{x}\left(\frac{\beta}{\beta+1}\right)^\alpha\left(\frac{1}{\beta+1}\right)^x
$$
a Negative Binomial distribution.

## See also
[[Prior predictive distribution]], [[Posterior distribution]], [[Conjugate prior]]
