---
title: "Bachelier's Model"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "Chapter 2 - Brownian Motion"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, brownian-motion, history]
---
## Definition
**Bachelier's model** (Bachelier, 1900) was the first mathematical model of share-price movements, proposing that a share price $S_t$ follows an (arithmetic) [[Brownian motion]] directly:
$$
S_t = S_0 + \alpha t + \beta B_t,
$$
where $B_t$ is a standard Brownian motion. Bachelier believed Brownian motion captured some of the observed characteristics of share prices (continuous, unpredictable fluctuations).

## Properties
### Shortcoming: negative prices
Because $B_t$ is normally distributed on all of $\mathbb{R}$, $S_t$ under Bachelier's model is itself normally distributed and can take negative values with positive probability — an economically nonsensical feature for a limited-liability share price. This is the model's principal, well-documented flaw.

### Historical resolution: Geometric Brownian Motion
It was not until the late 1950s that a workable alternative was proposed by Osborne (1959): [[Geometric Brownian Motion]],
$$
S_t = S_0\exp(\alpha t+\beta B_t),
$$
which forces $S_t>0$ for all $t$ since it is the exponential of a (finite) random variable. Since $\ln(S_t/S_0)\sim N(\alpha t,\beta^2t)$, $S_t/S_0$ is [[Lognormal distribution|lognormal]] rather than normal. GBM is the model used throughout the rest of this course (see [[Terminal Share Price Distribution]], [[Black-Scholes model]]).

## See also
[[Brownian motion]], [[Geometric Brownian Motion]], [[Efficient Market Hypothesis]], [[Lognormal distribution]]
