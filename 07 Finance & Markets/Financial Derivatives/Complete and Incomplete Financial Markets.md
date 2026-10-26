---
title: "Complete and Incomplete Financial Markets"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "Chapter 5 - Binomial Trees (Appendix)"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, market-completeness]
---
## Definition
Let $X_t$ be the value of a derivative at time $t$ (so $X_t$ is $\mathcal F_t$-measurable). A market is **complete** if, for every contingent claim $X$, there exists a [[Replicating Portfolio|replicating strategy]]. If not every claim can be replicated, the market is **incomplete**.

## Properties
### The binomial and lognormal models are complete
The [[Binomial option pricing model]] is a complete market: the one-step system of two equations in two unknowns $(\phi,\psi)$ always has a unique solution. The continuous-time lognormal model for share prices (with [[Black-Scholes model|Black-Scholes assumptions]]), $S_t = S_0\exp\{(\mu-\tfrac12\sigma^2)t+\sigma W_t\}$, is likewise complete.

### The trinomial model is incomplete
Extend the one-step tree to **three** final states $S_1^0,S_1^m,S_1^1$ (with corresponding derivative payoffs $f_1^0,f_1^m,f_1^1$). A replicating portfolio of $\phi$ units of stock and $\psi$ units of a bond gives three equations in two unknowns:
$$
\phi S_1^0+\psi e^{r\delta T}=f_1^0,\qquad \phi S_1^m+\psi e^{r\delta T}=f_1^m,\qquad \phi S_1^1+\psi e^{r\delta T}=f_1^1,
$$
which is in general **inconsistent** (over-determined) — no replicating portfolio exists for an arbitrary payoff. Augmenting the portfolio with a *second* bond (a third instrument) still leaves the system generically inconsistent, since now there are three equations in three unknowns but the resulting coefficient matrix is typically singular for the extra degree of freedom to help. Hence the trinomial model is **incomplete**, and pricing an arbitrary derivative there requires more than no-arbitrage arguments alone.

### Practical implication
In an incomplete market, the price of a derivative is no longer pinned down uniquely by no-arbitrage; instead a *range* of no-arbitrage prices is consistent with the model, and choosing among them requires extra assumptions (e.g. about risk preferences) or additional traded instruments.

## See also
[[Replicating Portfolio]], [[Self-Financing Strategy]], [[Binomial option pricing model]], [[Risk-neutral pricing]], [[Equivalent Probability Measures]]
