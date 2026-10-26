---
title: "Replicating Portfolio"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "Chapter 5 - Binomial Trees (Appendix)"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, replication, no-arbitrage]
---
## Definition
Let $X_u$ be the (contingent) payoff of a derivative at time $u$. A **replicating strategy** is a [[Self-Financing Strategy|self-financing]] portfolio $(\phi_t,\psi_t)_{t\in[0,u)}$ (units of the risky asset $S_t$ and the risk-free bond $B_t$) such that
$$
V(u) = \phi_uS_u+\psi_uB_u = X_u.
$$
That is, starting from $V(0)$ and following the trading strategy — with no cash injected or withdrawn — reproduces the derivative's payoff exactly and without risk.

## Properties
### Why replication prices derivatives
If a replicating strategy exists, the derivative's initial fair value **must** equal $V(0)$: if it were priced differently, one could trade the derivative against its replicating portfolio for a riskless arbitrage profit (see [[No-arbitrage principle]]). This is precisely how prices are derived in the [[Binomial option pricing model]] and the PDE derivation of the [[Black-Scholes model]].

### Complete markets
A market is **complete** if every contingent claim admits a replicating strategy — see [[Complete and Incomplete Financial Markets]].

## Examples
In the one-step [[Binomial option pricing model]], the pair $(\phi,\psi)$ solving
$$
\phi S_1^0+\psi e^{r\delta T}=f_1^0, \qquad \phi S_1^1+\psi e^{r\delta T}=f_1^1
$$
is exactly a one-period replicating strategy for the derivative with payoffs $f_1^0,f_1^1$.

## See also
[[Self-Financing Strategy]], [[Complete and Incomplete Financial Markets]], [[No-arbitrage principle]], [[Binomial option pricing model]], [[Risk-neutral pricing]]
