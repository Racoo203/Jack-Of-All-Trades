---
title: "Equivalent Probability Measures"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "Chapter 5 - Binomial Trees (Appendix); Chapter 8 - Risk-Neutral Pricing"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, measure-theory, risk-neutral]
---
## Definition
Two probability measures $P,Q$ defined on the same $\sigma$-algebra $\mathcal F$ are **equivalent**, written $P\sim Q$, if they agree on which events are possible:
$$
P(E)>0 \iff Q(E)>0, \qquad \forall E\in\mathcal F.
$$

## Properties
### The real-world vs. risk-neutral pair
In this course, $P$ denotes the real-world (physical) probability measure and $Q$ the **risk-neutral measure**. Equivalence is exactly the right notion for change of measure in derivative pricing: it guarantees $P$ and $Q$ never disagree about which outcomes are attainable, only about their likelihood.

### Constraint in the binomial model
In the [[Binomial option pricing model]], the risk-neutral "probability" $q=\frac{e^{r\delta T}-d}{u-d}$ must lie in $(0,1)$ for $P\sim Q$ to hold with $u,d$ the up/down factors and $r$ the risk-free rate. Multiplying $0<q<1$ through by $u-d>0$ gives the **no-arbitrage condition**
$$
d < e^{r\delta t} < u.
$$

### Changing drift, not volatility
A key qualitative fact (made precise by [[Girsanov theorem|Girsanov's theorem]]): given a standard Brownian motion $W_t$ under $P$, and $X_t=\gamma t+\sigma W_t$, there exists a measure $Q\sim P$ under which $X_t$ is itself a standard Brownian motion **if and only if $\sigma=1$**. That is, an equivalent change of measure can shift the *drift* of a Brownian motion but never its *volatility* — this is exactly why [[Stochastic volatility]] models are hard to hedge, and why the constant-$\sigma$ assumption of [[Black-Scholes model|Black-Scholes]] is preserved across the change to $Q$.

## See also
[[Girsanov theorem]], [[Risk-neutral pricing]], [[Binomial option pricing model]], [[Martingale Representation Theorem]]
