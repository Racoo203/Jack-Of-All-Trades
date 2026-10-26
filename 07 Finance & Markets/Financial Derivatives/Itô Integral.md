---
title: "Itô Integral"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "Chapter 3 - The Itô Integral"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, stochastic-calculus, ito-calculus]
---
## Definition
Ordinary calculus does not apply directly to functions of [[Brownian motion]], because sample paths of $B_t$ are continuous but nowhere differentiable. **Stochastic calculus** builds a substitute: stochastic calculus = ordinary calculus + randomness. Its central object is the **Itô integral**
$$
\int_0^t X(s)\,dB_s,
$$
for an "appropriate" (previsible) stochastic process $X$, constructed in stages:

1. **Deterministic integrands.** For $X(s)=k$ constant, $\int_0^t k\,dB_s = k B_t$. More generally, for a step function $\varphi(s)$, $\int_a^b\varphi(s)\,dB_s$ is a sum of independent normal increments. For an arbitrary (well-behaved) deterministic function $f$, borrowing the Riemann-sum construction, $\int_0^t f(s)\,dB_s$ is normally distributed with mean $0$ and variance given by the Riemann integral $\int_0^t f(s)^2\,ds$.
2. **Random integrands.** For a previsible (i.e. $\mathcal F_{t^-}$-measurable) step process $Y_s$, and letting the step functions converge, the limit — when it exists — is the Itô integral $\int_0^t Y_s\,dB_s$.

## Properties
Writing $I_t=\int_0^t Y_s\,dB_s$ (with $\mathcal F_t$ the natural [[Filtration]] of $B_t$), the Itô integral satisfies:

1. $\{I_t\}_{t\ge0}$ is a [[Martingale]].
2. $E[I_t]=0$.
3. **Itô isometry**: $E\!\left[I_t^2\right] = E\!\left[\int_0^t Y_s^2\,ds\right]$ (norm-preserving property).
4. Sample paths of $I_t$ are continuous.

> [!note] We rarely evaluate $\int_0^t Y_s\,dB_s$ directly from its definition; instead [[Ito's Lemma]] is used to manipulate such integrals in practice.

## See also
[[Brownian motion]], [[Ito's Lemma]], [[Multivariate Itô's Lemma]], [[Martingale]], [[Filtration]], [[Ornstein-Uhlenbeck Process]]
