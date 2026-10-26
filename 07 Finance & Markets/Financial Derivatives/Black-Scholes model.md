---
title: "Black-Scholes model"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "Chapter 6 - The Black-Scholes-Merton Model"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, black-scholes, pde]
---
## Definition
The **Black-Scholes-Merton (BSM) model** assumes a non-dividend-paying share price $S_t$ follows [[Geometric Brownian Motion]] with constant drift $\mu$ and volatility $\sigma$:
$$
dS_t = \mu S_t\,dt+\sigma S_t\,dZ_t,
$$
and a risk-free asset $P$ growing at constant continuously-compounded rate $r$: $dP=rP\,dt$. Let $f(t,S_t)$ be the price of a derivative on the share. The model's central result is a **partial differential equation (PDE)** that $f$ must satisfy.

## Properties
### Solving the GBM SDE
Claim: $S_t=S_0\exp\{(\mu-\tfrac12\sigma^2)t+\sigma Z_t\}$ solves the SDE above. **Proof.** Let $g(t,z)=S_0\exp\{(\mu-\tfrac12\sigma^2)t+\sigma z\}$. By [[Ito's Lemma]],
$$
dS_t = dg(t,Z_t) = \frac{\partial g}{\partial t}dt+\frac{\partial g}{\partial z}dZ_t+\tfrac12\frac{\partial^2g}{\partial z^2}dt = \left(\mu-\tfrac12\sigma^2\right)S_t\,dt+\sigma S_t\,dZ_t+\tfrac12\sigma^2S_t\,dt = \mu S_t\,dt+\sigma S_t\,dZ_t. \quad\blacksquare
$$
Since $Z_t\sim N(0,t)$, $\ln S_t\sim N\!\left(\ln S_0+(\mu-\tfrac12\sigma^2)t,\ \sigma^2t\right)$ — see [[Terminal Share Price Distribution]].

### The Black-Scholes PDE
$f$ must satisfy the backward parabolic PDE
$$
\frac{\partial f}{\partial t} + rS_t\frac{\partial f}{\partial S} + \tfrac12\sigma^2S_t^2\frac{\partial^2f}{\partial S^2} = rf.
$$
**Proof sketch (replicating-portfolio / delta-hedging argument).** Construct a portfolio $\pi_t = -f + \frac{\partial f}{\partial S}S_t$ (short one derivative, long $\frac{\partial f}{\partial S}$ shares). By [[Ito's Lemma]],
$$
df = \left(\frac{\partial f}{\partial t}+\mu S_t\frac{\partial f}{\partial S}+\tfrac12\sigma^2S_t^2\frac{\partial^2f}{\partial S^2}\right)dt+\sigma S_t\frac{\partial f}{\partial S}dZ_t.
$$
Then $d\pi_t = \frac{\partial f}{\partial S}dS_t - df$; substituting $dS_t=\mu S_t dt+\sigma S_t dZ_t$, the $dZ_t$ (random) terms cancel exactly, leaving $\pi_t$ instantaneously riskless:
$$
d\pi_t = -\left(\frac{\partial f}{\partial t}+\tfrac12\sigma^2S_t^2\frac{\partial^2f}{\partial S^2}\right)dt.
$$
Since $\pi_t$ is riskless, by [[No-arbitrage principle|no-arbitrage]] it must earn the risk-free rate: $d\pi_t=r\pi_t\,dt = r\left(\frac{\partial f}{\partial S}S_t-f\right)dt$. Equating the two expressions for $d\pi_t$ and rearranging gives the PDE above. $\blacksquare$ (Note this is the same delta-hedging idea used to derive the [[Greeks|Delta and Gamma formulas]] in the appendix to Chapter 7.)

### Boundary/terminal conditions
The PDE is a **backward** equation: rather than an initial condition, it is solved with a **final** (terminal) condition at $t=T$ determined by the option's payoff — e.g. for a European call, $c_T=\max\{S_T-K,0\}$, together with $c(t,0)=0$ (a worthless stock implies a worthless call) and $\lim_{S\to\infty}c(t,S_t)=S_t$ (deep ITM calls behave like the stock itself). Solving this boundary-value problem yields the [[Black-Scholes formula]].

### Extensions
The dividend-paying case (constant continuous yield $q$) modifies the PDE to $\frac{\partial f}{\partial t}+(r-q)S_t\frac{\partial f}{\partial S}+\tfrac12\sigma^2S_t^2\frac{\partial^2f}{\partial S^2}=rf$ — see [[Garman-Kohlhagen Formula]]. Letting volatility itself follow a stochastic process gives the [[Stochastic volatility|Heston model]].

### Shortcomings
Real share returns are not exactly normal (fat tails are common — see Lab 1), and the model cannot explain the empirically observed **volatility smile** (implied volatility varying systematically with strike — see [[Implied Volatility]]).

## See also
[[Black-Scholes formula]], [[Ito's Lemma]], [[Geometric Brownian Motion]], [[Greeks]], [[Garman-Kohlhagen Formula]], [[Stochastic volatility]]
