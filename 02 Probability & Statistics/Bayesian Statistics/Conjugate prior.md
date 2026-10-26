---
title: "Conjugate prior"
domain: "Probability & Statistics"
course: "Bayesian Statistics"
unit: "Chapter 3 - Bayesian Inference"
level: MSc
status: drafted
confidence: 0
tags: [bayesian-statistics, foundations]
---
## Definition
A family $\mathcal F$ of prior distributions for $\theta$ is **closed under sampling** from a model $f(x|\theta)$ if for every $\pi(\theta) \in \mathcal F$, the posterior $\pi(\theta|x) \propto \pi(\theta)f(x|\theta)$ is also in $\mathcal F$. A prior in such a family is called a **conjugate prior** for the model.

For a regular $k$-parameter [[Exponential family]] model
$$
f(x|\theta) = f(x)g(\theta)\exp\left(\sum_{i=1}^k a_i\varphi_i(\theta)h_i(x)\right)
$$
the conjugate prior has the form
$$
\pi(\theta|\tau) = [K(\tau)]^{-1}[g(\theta)]^{\tau_0}\exp\left(\sum_{i=1}^k a_i\tau_i\varphi_i(\theta)\right)
$$
where $\tau=(\tau_0,\tau_1,\dots,\tau_k)$ are **hyperparameters** and $K(\tau)$ is chosen to normalize the density.

## Properties
### Closure under sampling (Proposition 3.1)
Multiplying the exponential-family likelihood by the conjugate prior and collecting terms in $\theta$:
$$
\pi(\theta|\tau)f(x|\theta) \propto (g(\theta))^{\tau_0+1}\exp\left(\sum_{i=1}^k a_i(\tau_i+h_i(x))\varphi_i(\theta)\right)
$$
which has exactly the same functional form as the prior, but with hyperparameters updated to $\tau_0+1,\ \tau_1+h_1(x),\dots$. For an i.i.d. sample $x_1,\dots,x_n$, the posterior is $\pi(\theta \mid \tau_0+n,\ \tau_1+H_1(x),\dots,\tau_k+H_k(x))$ where $H_i(x)=\sum_j h_i(x_j)$ — see [[Sufficient statistic]] for why the data only enters through $H_i(x)$.

### Worked example: Bernoulli model → Beta prior
$f(x|p) = p^x(1-p)^{1-x} = (1-p)\exp\left(x\log\frac{p}{1-p}\right)$, so $g(p)=1-p$, $h(x)=x$, $\varphi(p)=\log\frac{p}{1-p}$. The conjugate prior is
$$
\pi(p|\tau_0,\tau_1) \propto (1-p)^{\tau_0}\exp\left(\tau_1\log\frac{p}{1-p}\right) = p^{\tau_1}(1-p)^{\tau_0-\tau_1}
$$
which is proper (integrable) iff $\tau_1>-1,\ \tau_0-\tau_1>-1$, and is then $\text{Beta}(\tau_1+1,\tau_0-\tau_1+1)$.

### Worked example: Poisson model → Gamma prior
$f(x|\lambda) = \frac{\lambda^x}{x!}e^{-\lambda} = (x!)^{-1}\exp(-\lambda)\exp(x\log\lambda)$, so $g(\lambda)=e^{-\lambda}$, $h(x)=x$, $\varphi(\lambda)=\log\lambda$. The conjugate prior is
$$
\pi(\lambda|\tau_0,\tau_1) \propto e^{-\tau_0\lambda}\lambda^{\tau_1} = \text{Gamma}(\tau_1+1,\ \tau_0)
$$

### Worked example: full Beta-Binomial posterior
With $X\sim\text{Binomial}(n,p)$ and uniform prior $\pi(p)=1$ (the special case $\text{Beta}(1,1)$),
$$
\pi(p|x) \propto \binom{n}{x}p^x(1-p)^{n-x}\cdot 1 \propto p^x(1-p)^{n-x} = \frac{p^x(1-p)^{n-x}}{B(x+1,n-x+1)}
$$
using $B(\alpha,\beta)=\Gamma(\alpha)\Gamma(\beta)/\Gamma(\alpha+\beta)$. The posterior mean is
$$
E[p|x] = \int_0^1 p\,\frac{p^x(1-p)^{n-x}}{B(x+1,n-x+1)}\,dp = \frac{B(x+2,n-x+1)}{B(x+1,n-x+1)} = \frac{x+1}{n+2}
$$

## See also
[[Exponential family]], [[Posterior distribution]], [[Prior distribution]], [[Sufficient statistic]]
