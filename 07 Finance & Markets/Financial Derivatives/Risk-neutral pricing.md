---
title: "Risk-neutral pricing"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "Chapter 8 - Risk-Neutral Pricing and the Equivalent Martingale Measure"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, risk-neutral-pricing, martingale]
---
## Definition
**Risk-neutral pricing** is an alternative to the PDE approach ([[Black-Scholes model]]) for computing derivative prices: instead of solving a PDE, change the probability measure from the real-world measure $P$ to an **equivalent martingale measure** $Q$ under which discounted asset prices are [[Martingale|martingales]]. Under $Q$, the derivative's price is simply the discounted expected payoff, $V_0=e^{-rT}E^Q[X_T]$.

Setup: a share price process $\{S_t\}_{t\ge0}$ is $\mathcal F_t$-measurable (adapted); a risk-free bond $B_t=B_0e^{rt}$ (constant $r$, $B_0=1$).

## Properties
### Self-financing and replicating strategies
A portfolio $(\phi_t,\psi_t)$ (units of $S_t$, units of $B_t$) is **previsible** if $\mathcal F_{t^-}$-measurable, and **[[Self-Financing Strategy|self-financing]]** if $d\pi_t=\phi_t\,dS_t+\psi_t\,dB_t$. A **[[Replicating Portfolio|replicating strategy]]** is a self-financing $(\phi_t,\psi_t)$ on $[0,u)$ with $\pi_u=\phi_uS_u+\psi_uB_u=X$, the derivative's payoff. A market is **complete** ([[Complete and Incomplete Financial Markets]]) if every contingent claim admits a replicating strategy — true of both the [[Binomial option pricing model|binomial model]] and the continuous lognormal ([[Black-Scholes model]]) model.

### Equivalent measures and the change-of-measure argument
$P,Q$ on $\mathcal F$ are [[Equivalent Probability Measures|equivalent]] ($P\sim Q$) if $P(E)>0\iff Q(E)>0\,\forall E$. By [[Girsanov theorem|the Cameron-Martin-Girsanov theorem]], if $W_t$ is a standard Brownian motion under $P$ and $\gamma_t$ previsible, there is $Q\sim P$ under which $W_t^*=W_t+\int_0^t\gamma_s\,ds$ is a standard Brownian motion. Taking $\gamma=\frac{\mu-r}{\sigma}$ for $S_t=S_0\exp\{(\mu-\tfrac12\sigma^2)t+\sigma W_t\}$ makes $e^{-rt}S_t$ a **martingale under $Q$** (full derivation in [[Girsanov theorem]]) — but **not** under $P$ (unless $\mu=r$).

### Why this reproduces the PDE answer
Once discounted prices are $Q$-martingales, no-arbitrage pricing collapses to a conditional expectation: $V_t=e^{-r(T-t)}E^Q[X_T\mid\mathcal F_t]$. This gives exactly the same [[Black-Scholes formula]] as solving the PDE directly (see that note's risk-neutral-expectation derivation) — the two methods are equivalent routes to the same price.

### Martingale representation
The **[[Martingale Representation Theorem]]** is the rigorous tool that guarantees a replicating strategy actually exists in the continuous-time complete market — it is what makes the risk-neutral pricing formula constructive rather than merely a consistency check.

## See also
[[Girsanov theorem]], [[Equivalent Probability Measures]], [[Martingale Representation Theorem]], [[Black-Scholes formula]], [[Complete and Incomplete Financial Markets]], [[Replicating Portfolio]]
