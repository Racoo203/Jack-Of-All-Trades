---
title: "Prior predictive distribution"
domain: "Probability & Statistics"
course: "Bayesian Statistics"
unit: "Chapter 3 - Bayesian Inference"
level: MSc
status: drafted
confidence: 0
tags: [bayesian-statistics, foundations]
---
## Definition
The prior predictive distribution of a [[Random Variable]] $X$ marginalizes over the [[Prior distribution]] of $\theta$:
$$
p(x) = \int_{-\infty}^{\infty} f(x|\theta)\,\pi(\theta)\,d\theta
$$
It describes the distribution of a new (not-yet-observed) data point before any data has been seen, i.e. it is the marginal distribution of $X$ implied jointly by the model and the prior.

## Properties
### Relation to the posterior predictive distribution
Setting $\pi(\theta)$ to the [[Posterior distribution]] $\pi(\theta|x_1)$ instead of the prior in the same integral gives the [[Posterior predictive distribution]] — the prior predictive distribution is the special case with no data yet observed (equivalently: the posterior predictive distribution before any $x_1$ has updated the prior).

## Examples
### Worked derivation: Binomial with uniform prior
For $X\sim\text{Binomial}(n,p)$ with prior $\pi(p)=1$ on $[0,1]$,
$$
P[X=x] = \int_0^1 \binom{n}{x}p^x(1-p)^{n-x}\cdot 1\,dp = \binom{n}{x}B(x+1,n-x+1) = \binom{n}{x}\frac{x!(n-x)!}{(n+1)!} = \frac{1}{n+1}
$$
for $x=0,1,\dots,n$. So the prior predictive distribution of $X$ is **uniform** on $\{0,1,\dots,n\}$ — with no data yet, every count is equally likely under a flat prior on $p$.

## See also
[[Posterior predictive distribution]], [[Prior distribution]], [[Conjugate prior]]
