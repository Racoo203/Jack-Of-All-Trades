---
title: "Volatility (Financial)"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "Chapter 5 - Binomial Trees"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, volatility]
---
## Definition
The **volatility** $\sigma$ of a stock price is a measure of how uncertain we are about its future movements. Formally, $\sigma$ is defined so that $\sigma\sqrt{\delta t}$ is the standard deviation of the (log-)return on the stock over a short time period $\delta t$; equivalently $\sigma^2\delta t$ is the variance of the return over $\delta t$.

## Properties
### Role across the course
Volatility is the single unobservable parameter in the whole pricing framework: it calibrates the [[Binomial option pricing model|CRR binomial tree]] ($u=e^{\sigma\sqrt{\delta T}}$, $d=e^{-\sigma\sqrt{\delta T}}$), it is the diffusion coefficient of [[Geometric Brownian Motion]] and hence of the [[Black-Scholes formula]], and its sensitivity is measured directly by **vega**, one of the [[Greeks]].

### Estimating volatility
Two broad approaches: (i) **historical volatility**, estimated from a time series of past returns; (ii) **[[Implied Volatility]]**, inferred from quoted option prices by inverting the Black-Scholes formula. Historical volatility need not predict future volatility well, which is one motivation for [[Implied Volatility]] and, further, for [[Stochastic volatility]] models.

## See also
[[Implied Volatility]], [[Stochastic volatility]], [[Black-Scholes formula]], [[Greeks]], [[Binomial option pricing model]]
