---
title: "No-arbitrage principle"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "Chapter 4 - Financial Markets"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, arbitrage, no-arbitrage]
---
## Definition
**Arbitrage** is the possibility of guaranteeing a riskless profit with no net investment. The **no-arbitrage principle** is the assumption that such opportunities cannot persist in a functioning financial market: it should not be possible to guarantee a profit without exposure to risk. Crucially, this assumption requires **no** knowledge of investors' risk preferences or beliefs — only that they prefer more wealth to less (an increase in consumption at no cost is always accepted).

## Properties
### Why it is enough to price derivatives
The minimal requirement of "no arbitrage opportunities" is sufficient, together with [[Replicating Portfolio|replication]], to build a realistic and mathematically tractable model of a financial market and to price contingent claims — the **arbitrage pricing technique** used throughout this course (e.g. [[Forward contract]] valuation, the [[Binomial option pricing model]], the [[Black-Scholes model|Black-Scholes PDE derivation]]).

### Worked example: forward pricing
If the forward price $F_t$ on a non-dividend-paying asset satisfies $F_t > S_te^{r(T-t)}$, an arbitrageur borrows $S_t$ at the risk-free rate, buys the asset, and takes a short forward position, locking in a riskless profit at $T$; a symmetric trade rules out $F_t<S_te^{r(T-t)}$. Hence no-arbitrage forces $F_t=S_te^{r(T-t)}$ (see [[Forward contract]]).

### Bounds on option prices
The no-arbitrage principle also produces model-free bounds on option prices before any pricing formula is derived — see [[Bounds for Option Prices]] and [[Put-call parity]].

## See also
[[Forward contract]], [[Put-call parity]], [[Replicating Portfolio]], [[Bounds for Option Prices]], [[Binomial option pricing model]]
