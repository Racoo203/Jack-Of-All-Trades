---
title: Geometric Brownian Motion
domain: Stochastic Processes
course: Stochastic Processes
unit: Foundations & Random Walks
level: MSc
status: seeding
confidence: 0
tags: [seeding]
---
## Definition
A [[Stochastic Process|stochastic process]] $\{S_t, t \geq 0\}$ is a geometric Brownian motion with drift $\mu$, variance parameter $\sigma^2$, and starting value $S_0$ if
$$
S_t = S_0\, e^{\left(\mu - \frac{\sigma^2}{2}\right)t + \sigma B_t}
$$
where $\{B_t\}$ is a standard [[Brownian motion]] with $B_0 = 0$.

## Properties
### Martingale case
If $\mu = 0$, geometric Brownian motion is a continuous-time [[Martingale|martingale]] (as well as a standard Brownian motion is).

### Use as an asset-price model
Geometric Brownian motion is widely used to model the prices of assets traded in a (frictionless) market, e.g. shares of stock. Such prices are non-negative by construction (being an exponential) and exhibit random fluctuations about a long-term exponential growth or decay trend, matching the qualitative behaviour of real asset prices better than an (unrestricted, possibly negative) Brownian motion would.

## See also
- [[Brownian motion]]
- [[Martingale]]
