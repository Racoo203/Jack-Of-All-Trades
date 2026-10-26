---
title: "Stochastic volatility"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "Chapter 6 - The Black-Scholes-Merton Model (Heston Model)"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, heston, stochastic-volatility]
---
## Definition
The [[Black-Scholes model]] assumes constant volatility $\sigma$ — an assumption contradicted by the empirically observed **volatility smile** (see [[Implied Volatility]]). The **Heston model** (1993) relaxes this by letting volatility itself follow a stochastic process, giving a genuinely **two-dimensional stochastic system**:
$$
dS_t = rS_t\,dt + \sigma_tS_t\,dW_t^S, \qquad dv_t = \kappa(\theta-v_t)\,dt + \lambda\sqrt{v_t}\,dW_t^V,
$$
where $v_t=\sigma_t^2$, $\kappa$ is the speed of mean reversion of variance, $\theta$ the long-run mean variance, $\lambda$ the volatility of volatility, and $W_t^S,W_t^V$ are Brownian motions with correlation $dW_t^SdW_t^V=\rho\,dt$.

## Properties
### The variance process is a CIR process
The second SDE above is exactly a [[Cox-Ingersoll-Ross (CIR) Process]]: mean-reverting, with $v_t\ge0$ guaranteed provided the **Feller condition** $2\kappa\theta>\lambda^2$ holds.

### The Heston PDE
Applying [[Ito's Lemma|Itô's Lemma]] in two dimensions (see [[Multivariate Itô's Lemma]]) to a derivative price $f(t,S_t,v_t)$ and the usual replicating-portfolio no-arbitrage argument gives a PDE with cross-partial and correlation terms:
$$
\frac{\partial f}{\partial t}+rS\frac{\partial f}{\partial S}+\tfrac12vS^2\frac{\partial^2f}{\partial S^2}+\tfrac12\lambda^2v\frac{\partial^2f}{\partial v^2}+\rho\lambda vS\frac{\partial^2f}{\partial v\,\partial S}+\left(\kappa\theta-(\kappa+v)v\right)\frac{\partial f}{\partial v} = rf.
$$
This is materially harder to solve than the (one-dimensional) [[Black-Scholes model|Black-Scholes PDE]]; in practice the Heston model is solved numerically (e.g. via characteristic-function / Fourier methods), and the details are beyond the scope of this module.

### Why it matters
Despite the added complexity, the Heston model is heavily used in industry because it captures features the Black-Scholes model cannot: a volatility smile/skew, and volatility clustering.

## See also
[[Black-Scholes model]], [[Cox-Ingersoll-Ross (CIR) Process]], [[Implied Volatility]], [[Multivariate Itô's Lemma]], [[Volatility (Financial)]]
