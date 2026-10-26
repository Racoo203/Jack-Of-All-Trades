---
title: "Likelihood function"
domain: "Probability & Statistics"
course: "Bayesian Statistics"
unit: "Chapter 2 - Classical Methods of Statistics"
level: MSc
status: drafted
confidence: 0
tags: [bayesian-statistics, classical-statistics, foundations]
---
## Definition
A parametric statistical model is a family of distributions $f(x;\theta)$ indexed by $\theta \in \Theta$. For a fixed, *observed* data set $x$, viewing $f(x;\theta)$ as a function of $\theta$ (rather than of $x$) defines the **likelihood function**, written
$$
L(\theta|x) = f(x;\theta)
$$
For independent observations $X_1=x_1,\dots,X_n=x_n$, the joint density factorizes and the likelihood is
$$
L(\theta|x_1,\dots,x_n) = \prod_{i=1}^n f(x_i;\theta)
$$
It is usually more convenient to work with the **log-likelihood** $\ell(\theta|x) = \log L(\theta|x)$, since $\log$ is strictly increasing so $L$ and $\log L$ are maximized at the same $\theta$.

## Properties
### Worked derivation: Bernoulli likelihood
Let $X_1,\dots,X_n$ be i.i.d. Bernoulli$(p)$, $f(x|p)=p^x(1-p)^{1-x}$. The joint density (likelihood) is
$$
L(p|x) = \prod_{i=1}^n p^{x_i}(1-p)^{1-x_i} = p^{\sum_i x_i}(1-p)^{n-\sum_i x_i}, \quad 0 \le p \le 1
$$
and the log-likelihood is
$$
\ell(p|x) = \left(\sum_i x_i\right)\log p + \left(n-\sum_i x_i\right)\log(1-p)
$$
This is the basis for the [[Maximum Likelihood Estimate]] of $p$ (differentiate and set to zero — see that note for the full derivation) and is also exactly the form used to derive the [[Conjugate prior]] for Bernoulli data (Beta prior).

### Role in Bayesian inference
The likelihood is the vehicle through which data enters [[Bayes' theorem]]: $\text{posterior} \propto \text{likelihood} \times \text{prior}$. Unlike in classical statistics, in Bayesian inference $\theta$ is random, so $f(x|\theta)$ is literally a conditional density, and the same function plays a dual role as "likelihood of $\theta$" and "conditional density of $x$".

## See also
[[Maximum Likelihood Estimate]], [[Sufficient statistic]], [[Exponential family]], [[Posterior distribution]], [[Point estimation]]
