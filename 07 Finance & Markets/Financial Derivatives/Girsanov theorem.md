---
title: "Girsanov theorem"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "Chapter 5 (Appendix); Chapter 8 - Risk-Neutral Pricing"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, girsanov, change-of-measure, martingale]
---
## Definition
**Girsanov's theorem** (also called the **Cameron-Martin-Girsanov theorem**) says: suppose $W_t$ is a standard [[Brownian motion]] under a measure $P$, and $\gamma_t$ is a previsible process. Then there exists a measure $Q$ [[Equivalent Probability Measures|equivalent]] to $P$ such that
$$
W_t^* = W_t + \int_0^t \gamma_\tau\,d\tau
$$
is a standard Brownian motion under $Q$. Conversely, if $W_t$ is a standard Brownian motion under $P$ and $Q\sim P$, there exists a previsible $\gamma_t$ for which $W_t^*$ (defined as above) is a standard Brownian motion under $Q$.

Informally: an equivalent change of measure can shift the **drift** of a Brownian motion by any previsible amount, but leaves its **volatility** unchanged (see [[Equivalent Probability Measures]]).

## Properties
### Application: making discounted GBM a martingale
Let $S_t$ follow [[Geometric Brownian Motion]] under $P$: $S_t = S_0\exp\{(\mu-\tfrac12\sigma^2)t+\sigma W_t\}$. Take $\gamma_t=\gamma=\frac{\mu-r}{\sigma}$ (the **market price of risk**) and define $W_t^*=W_t+\gamma t$. Then
$$
S_t = S_0\exp\!\left\{(\mu-\tfrac12\sigma^2)t+\sigma W_t\right\} = S_0\exp\!\left\{(r-\tfrac12\sigma^2)t+\sigma\!\left[W_t+\tfrac{\mu-r}{\sigma}t\right]\right\} = S_0\exp\!\left\{(r-\tfrac12\sigma^2)t+\sigma W_t^*\right\}.
$$
By Girsanov's theorem there is $Q\sim P$ under which $W_t^*$ is a standard Brownian motion. Then for $u<t$,
$$
E^Q\!\left[e^{-rt}S_t \mid \mathcal F_u\right] = e^{-ru}S_u\, E^Q\!\left[\exp\!\left\{(r-\tfrac12\sigma^2)(t-u)+\sigma(W_t^*-W_u^*)\right\}\right] = e^{-ru}S_u \cdot e^{(r-\frac12\sigma^2)(t-u)+\frac12\sigma^2(t-u)} = e^{-ru}S_u,
$$
so $e^{-rt}S_t$ is a **martingale under $Q$** (the discounted stock price is martingale precisely when priced under the risk-neutral measure). It can be shown $e^{-rt}S_t$ is **not** a martingale under $P$ unless $\mu=r$. This is the theoretical foundation of [[Risk-neutral pricing]].

### Not an arbitrary result: it can change or not change equivalence
A worked check: for $X_t=\gamma t+\sigma W_t$ under $P$, an equivalent $Q$ exists making $X_t$ a standard Brownian motion **iff $\sigma=1$** — reinforcing that only drift, never volatility, can be altered by an equivalent measure change.

## See also
[[Equivalent Probability Measures]], [[Risk-neutral pricing]], [[Martingale]], [[Martingale Representation Theorem]], [[Geometric Brownian Motion]]
