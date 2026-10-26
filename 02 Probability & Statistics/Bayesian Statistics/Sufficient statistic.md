---
title: "Sufficient statistic"
domain: "Probability & Statistics"
course: "Bayesian Statistics"
unit: "Chapter 3 - Bayesian Inference"
level: MSc
status: drafted
confidence: 0
tags: [bayesian-statistics, classical-statistics, foundations]
---
## Definition
A statistic $T(X)$ is **sufficient** for $\theta$ if the conditional distribution of the sample $X=(X_1,\dots,X_n)$ given $T(X)$ does not depend on $\theta$. Informally, $T(X)$ captures all the information in the sample that is relevant to $\theta$ — once $T(X)$ is known, the rest of the data carries no further information about $\theta$.

<!-- UNVERIFIED: check against course slides — the course's Chapter 2/3 lecture notes do not present a dedicated sufficiency section or the Fisher–Neyman factorization theorem explicitly; this note is drafted from standard theory and grounded in the course's exponential-family treatment (Chapter 3), where the sufficient statistics appear implicitly. -->

## Properties
### Fisher–Neyman factorization theorem
$T(X)$ is sufficient for $\theta$ if and only if the likelihood factorizes as
$$
f(x|\theta) = g(T(x),\theta)\,h(x)
$$
for some functions $g$ and $h$, where $h$ does not depend on $\theta$.

### Sufficiency in the exponential family
For a regular $k$-parameter [[Exponential family]] model,
$$
f(x|\theta) = f(x)g(\theta)\exp\left(\sum_{i=1}^k a_i \varphi_i(\theta) h_i(x)\right)
$$
the factorization theorem is satisfied immediately with $h(x) = f(x)$ absorbed into the non-$\theta$ part, and $T(x) = (h_1(x),\dots,h_k(x))$ is a sufficient statistic. This is exactly what drives the [[Conjugate prior]] update rule: when combining a sample $x_1,\dots,x_n$ with a conjugate prior with hyperparameters $(\tau_0,\tau_1,\dots,\tau_k)$, the posterior only depends on the data through
$$
H_i(x) = \sum_j h_i(x_j), \qquad i=1,\dots,k
$$
i.e. through the sufficient statistics $H_i(x)$ — the posterior hyperparameters become $\tau_0+n,\ \tau_1+H_1(x),\dots,\tau_k+H_k(x)$.

## Examples
For i.i.d. Bernoulli$(p)$ data, $h(x)=x$, so $T(X) = \sum_i X_i$ (the number of successes) is sufficient for $p$ — this matches the [[Maximum Likelihood Estimate]] $\hat p = \bar x$, which depends on the data only through this sum.

## See also
[[Exponential family]], [[Likelihood function]], [[Conjugate prior]]
