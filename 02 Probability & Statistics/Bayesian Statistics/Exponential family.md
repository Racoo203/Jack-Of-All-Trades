---
title: "Exponential family"
domain: "Probability & Statistics"
course: "Bayesian Statistics"
unit: "Chapter 3 - Bayesian Inference"
level: MSc
status: drafted
confidence: 0
tags: [bayesian-statistics, foundations]
---
## Definition
A random variable $X$ has a density belonging to a regular $k$-parameter exponential family if
$$
f(x|\theta) = f(x)\,g(\theta)\,\exp\left(\sum_{i=1}^k a_i\,\varphi_i(\theta)\,h_i(x)\right)
$$
Most standard distributions used in this course (Bernoulli, Binomial, Poisson, Normal, Gamma, Exponential) belong to this family. The importance of the form is twofold: (1) it isolates the parts of the data, $h_i(x)$, that the likelihood depends on — these are exactly the [[Sufficient statistic|sufficient statistics]] — and (2) it guarantees the existence of a [[Conjugate prior]].

## Properties
### Why a conjugate prior always exists
Because $f(x|\theta)$ depends on $x$ only through $g(\theta)$ and the linear-in-$\varphi_i(\theta)$ exponent weighted by $h_i(x)$, choosing a prior of matching exponential form in $\theta$ makes prior $\times$ likelihood close under multiplication (the exponents simply add) — see [[Conjugate prior]] for the full closure argument (Proposition 3.1).

### Examples of the exponential-family form
- **Bernoulli**: $f(x|p)=p^x(1-p)^{1-x} = 1\cdot(1-p)\cdot\exp\left(1\cdot\log\left(\frac{p}{1-p}\right)\cdot x\right)$, so $g(p)=1-p$, $h(x)=x$, $\varphi(p)=\log\frac{p}{1-p}$ (the log-odds).
- **Poisson**: $f(x|\lambda) = \frac{\lambda^x}{x!}e^{-\lambda} = (x!)^{-1}\cdot e^{-\lambda}\cdot\exp(1\cdot\log(\lambda)\cdot x)$, so $g(\lambda)=e^{-\lambda}$, $h(x)=x$, $\varphi(\lambda)=\log\lambda$.
- **Normal** (writing $\lambda=1/\sigma^2$ for precision, $\mu$ for the mean):
$$
\pi(x|\mu,\lambda) = \left(\frac{\lambda}{2\pi}\right)^{1/2}\exp\left(-\frac{\lambda}{2}\mu^2\right)\cdot\exp\left(-\frac{\lambda}{2}x^2+\lambda\mu x\right)
$$
giving two natural parameters/statistics: $\varphi_1=-\lambda/2,\ h_1(x)=x^2$ and $\varphi_2=\lambda\mu,\ h_2(x)=x$ — i.e. the Normal is a 2-parameter exponential family with sufficient statistics $(\sum x_i,\sum x_i^2)$.

### Consequence for updating beliefs
When a conjugate prior is used, prior and posterior belong to the same exponential family, so "updating belief" is just updating hyperparameters — no re-derivation of the functional form is needed. With a non-conjugate prior, the posterior density is often not available in closed form.

## See also
[[Conjugate prior]], [[Sufficient statistic]], [[Likelihood function]]
