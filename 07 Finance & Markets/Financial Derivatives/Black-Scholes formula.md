---
title: "Black-Scholes formula"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "Chapter 6 - The Black-Scholes-Merton Model"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, black-scholes, options-pricing]
---
## Definition
Solving the [[Black-Scholes model|Black-Scholes PDE]] with the European call boundary condition gives the **Black-Scholes formula**:
$$
c(0,S_0) = S_0N(d_1) - Ke^{-rT}N(d_2),
$$
$$
d_1 = \frac{\ln(S_0/K)+\left(r+\tfrac12\sigma^2\right)T}{\sigma\sqrt T}, \qquad d_2 = \frac{\ln(S_0/K)+\left(r-\tfrac12\sigma^2\right)T}{\sigma\sqrt T} = d_1-\sigma\sqrt T,
$$
$$
N(x) = \frac1{\sqrt{2\pi}}\int_{-\infty}^x e^{-\frac12u^2}\,du.
$$
The corresponding European **put** price (via [[Put-call parity]]) is $p(0,S_0)=Ke^{-rT}N(-d_2)-S_0N(-d_1)$.

## Properties
### Derivation via risk-neutral expectation
From [[Risk-neutral pricing]], $c_0=e^{-rT}E^Q[\max\{S_T-K,0\}]$, with $S_T=S_0e^{(r-\frac12\sigma^2)T+\sigma\sqrt T\,\varepsilon}$, $\varepsilon\sim N(0,1)$ under $Q$. Writing $\lambda=\frac{\ln(S_0/K)-(r-\frac12\sigma^2)T}{\sigma\sqrt T}=-d_2$,
$$
c_0 = \frac{e^{-rT}}{\sqrt{2\pi}}\int_\lambda^\infty \left\{S_0e^{(r-\frac12\sigma^2)T+\sigma\sqrt Tx}-K\right\}e^{-x^2/2}\,dx.
$$
The $K$-term integrates directly to $Ke^{-rT}N(-\lambda)=Ke^{-rT}N(d_2)$. For the $S_0$-term, complete the square in the exponent (substitute $y=x-\sigma\sqrt T$) to get $S_0e^{rT}\{1-N(\lambda-\sigma\sqrt T)\}=S_0e^{rT}N(-(\lambda-\sigma\sqrt T))$; discounting by $e^{-rT}$ and using $-(\lambda-\sigma\sqrt T)=d_2+\sigma\sqrt T=d_1$ gives $S_0N(d_1)$. Combining: $c_0=S_0N(d_1)-Ke^{-rT}N(d_2)$. $\blacksquare$

### Log-normal probability results
Because $S_T$ is [[Lognormal distribution|lognormal]] under $Q$, $\Pr^Q(S_T<K)=N(-d_2)$ (see [[Terminal Share Price Distribution]] for the analogous real-world statement with $\hat d_2$); $N(d_2)$ is therefore the risk-neutral probability that a call finishes **in the money**.

### Decomposition into asset-or-nothing / cash-or-nothing components
The formula splits into two recognisable pieces: $S_0N(d_1)$ is the value of an *asset-or-nothing call* (pays one share if $S_T>K$), and $Ke^{-rT}N(d_2)$ is $K$ times the value of a *cash-or-nothing call* (pays \$1 if $S_T>K$). This decomposition is useful for pricing embedded options directly from a partial BSM formula (see Examples).

## Examples
**Employee share scheme (Revision Q7).** An employer promises staff 1,000 shares in a year if the price rises from £1 to at least £1.50 ($r=4\%$, $\sigma=30\%$). The promise is exactly the asset-or-nothing component of a call: value $=S\cdot N(d_1)$ per share, with
$$
d_1 = \frac{\ln(1/1.5)+(0.04+\tfrac12(0.3)^2)}{0.3} = -1.0682,
$$
so the value per share is $1\times N(-1.0682)\approx 0.1428$; capping the employee's gain at £2,500 turns this into a **bull spread** of two BSM components (an embedded application connecting to [[Option Trading Strategies]] and [[Variable Annuity Guarantees]]).

## See also
[[Black-Scholes model]], [[Risk-neutral pricing]], [[Terminal Share Price Distribution]], [[Greeks]], [[Garman-Kohlhagen Formula]], [[Implied Volatility]], [[Merton Model (Credit Risk)]]
