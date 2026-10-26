---
title: "Moment Generating Function"
domain: "Probability & Statistics"
course: "Bayesian Statistics"
unit: "Chapter 7 - Reinsurance, Convolution and Central Limit Theory (CLT)"
level: MSc
status: drafted
confidence: 0
tags: [bayesian-statistics, actuarial, risk-theory]
---
## Definition
The moment generating function (mgf) of a random variable $X$ is
$$
M_X(t) = E[e^{Xt}]
$$
whenever this expectation exists in a neighbourhood of $t=0$.

## Properties
### MGF of a sum of independent random variables factorizes
For independent $X,Y$, $Z=X+Y$:
$$
M_Z(t) = E[e^{(X+Y)t}] = E[e^{Xt}]\,E[e^{Yt}] = M_X(t)\,M_Y(t)
$$
This gives a much easier route to the distribution of a sum than direct [[Convolution]]: compute the product of mgfs, then recognise which distribution has that mgf.

### Uniqueness
The mgf, when it exists, uniquely determines the distribution: two random variables with the same mgf (on a common neighbourhood of $0$) have the same distribution.

## Examples
### Poisson mgf
For $X\sim\text{Poisson}(\lambda)$:
$$
M_X(t) = \sum_{x=0}^\infty e^{xt}\frac{\lambda^x}{x!}e^{-\lambda} = e^{-\lambda}\sum_{x=0}^\infty\frac{(e^t\lambda)^x}{x!} = e^{-\lambda}e^{e^t\lambda} = e^{(e^t-1)\lambda}
$$
Multiplying two independent Poisson mgfs, $e^{(e^t-1)\lambda}\cdot e^{(e^t-1)\mu}=e^{(e^t-1)(\lambda+\mu)}$, immediately re-derives $X+Y\sim\text{Poisson}(\lambda+\mu)$ (matching the direct convolution result in [[Convolution]]) — much less work than the discrete convolution sum.

### Exponential sum via MGF
For $X\sim\text{Exp}(\lambda)$: $M_X(t) = \int_0^\infty e^{xt}\lambda e^{-\lambda x}\,dx = \frac{\lambda}{\lambda-t}$ for $t<\lambda$. For $X,Y$ i.i.d. $\text{Exp}(\lambda)$:
$$
M_{X+Y}(t) = \left(\frac{\lambda}{\lambda-t}\right)^2
$$
which is the mgf of $\text{Gamma}(2,\lambda)$ — confirming the direct change-of-variable result in [[Distribution of a Function of a Random Variable]] ($X_1+X_2\sim\text{Gamma}(2,1)$ for standard exponentials).

## See also
[[Convolution]], [[Central Limit Theorem (CLT)]], [[Distribution of a Function of a Random Variable]]
