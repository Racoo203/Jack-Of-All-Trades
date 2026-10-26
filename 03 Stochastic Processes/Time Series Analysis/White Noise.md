---
title: White Noise
domain: Stochastic Processes
course: Stochastic Processes
unit: Time Series Analysis
level: MSc
status: seeding
confidence: 0
tags: [seeding]
---
## Definition
A [[Stochastic Process|stochastic process]] $\{e_t, t \in \mathbb{Z}\}$ is white noise if:
1. $E(e_t) = 0$ for all $t$;
2. $\operatorname{var}(e_t) = \sigma^2 < \infty$ for all $t$ (constant, finite variance);
3. $\operatorname{cov}(e_t, e_s) = 0$ for all $t \neq s$ (uncorrelated at every non-zero lag).

A stronger, commonly assumed version requires the $e_t$ to be [[Independent and Identically Distributed (i.i.d)|i.i.d.]] with mean $0$ and variance $\sigma^2$ — independence is a stronger condition than the mere uncorrelatedness required above.

## Properties
### Weak stationarity
White noise is trivially [[Weak Stationarity|weakly stationary]]: its mean function is constant ($\equiv 0$), its [[Autocovariance function|autocovariance function]] is $\gamma_0 = \sigma^2$ and $\gamma_s = 0$ for $s \neq 0$ (a function of the lag $s$ alone), and its second moments are finite.

### Role as a building block
White noise is the fundamental "input" or "innovation" process from which the standard linear time-series models are built: a [[Moving Average Process|moving average process]] $\mathrm{MA}(q)$ is a finite linear combination of white-noise terms, and an [[Autoregressive Process|autoregressive process]] $\mathrm{AR}(p)$ can itself be re-expressed as an infinite moving average (hence an infinite linear combination) of white noise, via its $\mathrm{MA}(\infty)$ representation. An [[ARMA Process|ARMA process]] combines both structures.

## See also
- [[Moving Average Process]]
- [[Autoregressive Process]]
- [[ARMA Process]]
- [[Weak Stationarity]]
- [[Autocovariance function]]
- [[Autocorrelation Function]]
