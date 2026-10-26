---
title: "Terminal Share Price Distribution"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "Chapter 1 - Common Distributions in Finance"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, lognormal, share-prices]
---
## Definition
Assume a share price $S_t$ follows the standard model used throughout this course: $\ln(S_t/S_0)$ is normally distributed with
$$
\ln\frac{S_t}{S_0} \sim N\!\left(\left(\mu-\tfrac12\sigma^2\right)t,\ \sigma^2 t\right),
$$
equivalently
$$
S_t = S_0\exp\!\left\{\left(\mu-\tfrac12\sigma^2\right)t+\sigma\sqrt t\, Z\right\}, \qquad Z\sim N(0,1),
$$
where $\mu$ is the annual expected rate of return and $\sigma$ the annual volatility of the share. This is exactly the terminal distribution of a [[Geometric Brownian Motion]], and $S_t$ is [[Lognormal distribution|lognormally]] distributed: $S_t \sim LN\!\left(\ln S_0+(\mu-\tfrac12\sigma^2)t,\ \sigma^2 t\right)$.

## Properties
### Expected value
Using the lognormal mean formula (see [[Lognormal distribution]]) with $\mu_Y = \ln S_0 + (\mu-\tfrac12\sigma^2)t$ and $\sigma_Y^2=\sigma^2t$:
$$
E[S_t] = \exp\left\{\ln S_0 + \left(\mu-\tfrac12\sigma^2\right)t + \tfrac12\sigma^2t\right\} = S_0e^{\mu t}.
$$
This confirms $\mu$ is indeed the expected (continuously compounded) rate of return.

### Proposition (probability of falling below a threshold)
Let $K>0$. Then
$$
\Pr(S_t < K) = N(-\hat d_2), \qquad \hat d_2 = \frac{\ln(S_0/K)+\left(\mu-\tfrac12\sigma^2\right)t}{\sigma\sqrt t}.
$$
**Proof.** $\Pr(S_t<K)=\Pr(\ln S_t < \ln K)$. Standardising $\ln S_t$,
$$
\Pr(S_t<K) = \Pr\!\left(\frac{\ln S_t-\ln S_0-(\mu-\tfrac12\sigma^2)t}{\sigma\sqrt t} < \frac{\ln K-\ln S_0-(\mu-\tfrac12\sigma^2)t}{\sigma\sqrt t}\right) = \Pr(Z<-\hat d_2) = N(-\hat d_2). \qquad\blacksquare
$$

### Corollary
By symmetry of the normal distribution, $\Pr(S_t>K)=N(\hat d_2)$.

> [!note] Idiosyncratic notation
> This course writes the threshold statistic as $\hat d_2$ (using the **real-world** drift $\mu$) to distinguish it from the risk-neutral $d_2$ that appears in the [[Black-Scholes formula]] (which replaces $\mu$ with the risk-free rate $r$). The two are structurally identical — $\hat d_2$ is the direct conceptual ancestor of $d_2$.

### Conditional expectation given exceedance
For a threshold $K$, the partial expectation of $S_t$ conditional on $S_t>K$ is
$$
E^P(S_t \mid S_t>K) = \frac{S_0e^{\mu t}N(\hat d_1)}{N(\hat d_2)}, \qquad \hat d_1 = \hat d_2+\sigma\sqrt t.
$$
This result is used later (Chapter 6) when computing the expected payoff of a call option conditional on it expiring in the money — the risk-neutral version of this same identity (with $\mu\to r$) drives the $S_0N(d_1)$ term of the [[Black-Scholes formula]].

## Examples
Let $S_0=\$100$, $\mu=10\%$ p.a., $\sigma=30\%$ p.a. The two-year price is
$$
S_2 = 100\,e^{(0.1-\frac12(0.3)^2)2+0.3\sqrt2 Z} = 100\,e^{0.11+0.4243Z},
$$
and $E(S_2) = 100e^{0.1\times2} = \$122.14$.

## See also
[[Normal distribution]], [[Lognormal distribution]], [[Geometric Brownian Motion]], [[Black-Scholes formula]], [[Moment Generating Function]]
