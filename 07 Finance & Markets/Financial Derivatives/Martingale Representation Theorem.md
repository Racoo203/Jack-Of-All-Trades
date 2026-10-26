---
title: "Martingale Representation Theorem"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "Chapter 8 - Risk-Neutral Pricing and the Equivalent Martingale Measure"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, martingale, risk-neutral-pricing]
---
## Definition
Suppose $X_t$ is a [[Martingale]] under $P$ (with $\sigma\ne0$), and $Y_t$ is another $P$-martingale. The **martingale representation theorem** states there exists a unique previsible process $\phi_t$ such that
$$
Y_t = Y_0 + \int_0^t \phi_s\,dX_s \qquad \text{i.e.} \qquad dY_t=\phi_t\,dX_t,
$$
**if and only if** there is no measure other than $P$, equivalent to $P$, under which $X_t$ is a martingale.

## Properties
### Role in derivative pricing
This theorem is what makes [[Risk-neutral pricing]] **constructive**, not merely descriptive: once a derivative's discounted payoff process is known to be a $Q$-martingale, the theorem guarantees there exists a previsible trading strategy $\phi_t$ that exactly replicates it — i.e. that the market is complete and the replicating portfolio required by [[Replicating Portfolio|replication]] can actually be found (not just shown to exist in principle). This is the continuous-time analogue of solving the two simultaneous equations for $(\phi,\psi)$ in the one-step [[Binomial option pricing model]].

## See also
[[Risk-neutral pricing]], [[Martingale]], [[Girsanov theorem]], [[Replicating Portfolio]], [[Complete and Incomplete Financial Markets]]
