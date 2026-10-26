---
title: "Collective Risk Model"
domain: "Probability & Statistics"
course: "Bayesian Statistics"
unit: "Chapter 8 - Risk Theory"
level: MSc
status: drafted
confidence: 0
tags: [bayesian-statistics, actuarial, risk-theory]
---
## Definition
For a short-term insurance risk (policy or portfolio), the aggregate claims $S$ in one year are modelled as a random sum
$$
S = X_1 + \cdots + X_N
$$
where $N$ is the (random) number of claims and $X_i$ is the amount of the $i$-th claim, with the $X_i$ i.i.d. and independent of $N$; $S=0$ if $N=0$. This decouples claim *frequency* ($N$) from claim *severity* ($X_i$) — useful because different factors affect each (e.g. weather affects motor-claim frequency but not repair-cost severity; inflation affects severity but not frequency). The distribution of $S$ is called a **compound distribution**; if $N\sim\text{Poisson}$, $S$ has a **compound Poisson** distribution; if $N\sim$ Negative Binomial, $S$ is **compound Negative Binomial**.

## Properties
### Mean, variance and MGF of a compound sum
Writing $\mu_k=E[X^k]$ for the claim-size moments, conditioning on $N$ (law of total expectation/variance):
$$
E[S] = E_N[E_X[S|N]] = E_N[N\mu_1] = \mu_1 E[N]
$$
$$
\text{Var}[S] = E[N]\,\text{Var}[X] + \mu_1^2\,\text{Var}[N]
$$
For the moment generating function, using independence of the $X_i$ and of $N$ from the $X_i$:
$$
m_S(t) = E_N\left[E_X[e^{tS}|N]\right] = \sum_{n=0}^\infty \{m_X(t)\}^n P[N=n] = E[e^{N\log m_X(t)}] = m_N(\log m_X(t))
$$
This "mgf of $N$, evaluated at $\log m_X(t)$" identity is the standard tool for identifying a compound distribution's exact form.

### Worked example: compound Poisson
If $N\sim\text{Poisson}(\lambda)$ ($E[N]=\text{Var}[N]=\lambda$, $M_N(t)=e^{(e^t-1)\lambda}$):
$$
E[S]=\lambda\mu_1, \qquad \text{Var}[S]=\lambda\mu_2=\lambda E[X^2], \qquad M_S(t) = e^{\lambda(m_X(t)-1)}
$$

### Worked example: compound Geometric/Exponential has a closed-form distribution
Let $N\sim\text{Geometric}(p)$ ($q=1-p$), $X\sim\text{Exp}(1)$. Then $m_N(t)=\frac{p}{1-qe^t}$ and $m_X(t)=(1-t)^{-1}$, so
$$
m_S(t) = m_N(\log m_X(t)) = \frac{p}{1-q\,m_X(t)} = p + q\frac{p}{p-t}
$$
This is a mixture of the mgf of the constant $0$ (weight $p$) and the mgf of $\text{Exp}(p)$ (weight $q$). By uniqueness of mgfs (see [[Moment Generating Function]]), $S$ has cdf
$$
F(x) = p + q(1-e^{-px}) = 1-qe^{-px}, \qquad x\ge0
$$
— a point mass of size $p$ at $0$, and exponential($p$) otherwise. This is a common pattern in risk theory: compound distributions frequently have a jump at zero (the probability $N=0$) with a continuous distribution above it.

## See also
[[Moment Generating Function]], [[Mixed Poisson Distribution]], [[Ruin Theory]], [[Reinsurance]]
