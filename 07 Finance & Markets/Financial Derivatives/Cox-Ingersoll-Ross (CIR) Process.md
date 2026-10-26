---
title: "Cox-Ingersoll-Ross (CIR) Process"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "Chapter 6 - Stochastic Volatility; Chapter 9 - Interest Rate Models"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, cir, mean-reversion, feller-condition]
---
## Definition
The **Cox-Ingersoll-Ross (CIR) process** is a mean-reverting diffusion with state-dependent ("square-root") volatility:
$$
dX_t = \kappa(\theta-X_t)\,dt + \lambda\sqrt{X_t}\,dW_t,
$$
where $\kappa$ is the speed of mean reversion, $\theta$ the long-run mean, and $\lambda$ the volatility parameter (often called "volatility of volatility" when $X_t$ represents a variance process). It appears twice in this course: as a **short-rate model** ($X_t=r_t$, Chapter 9) and as the **variance process** in the [[Stochastic volatility|Heston model]] ($X_t=v_t$, Chapter 6).

## Properties
### Non-negativity and the Feller condition
Unlike the [[Vasicek Model]] or plain [[Ornstein-Uhlenbeck Process]], the $\sqrt{X_t}$ diffusion term shrinks to zero as $X_t\to0$, which (combined with a positive drift $\kappa\theta$ pulling the process back up) can keep $X_t\ge0$ almost surely. This requires the **Feller condition**:
$$
2\kappa\theta > \lambda^2.
$$
If the Feller condition fails, $X_t$ can reach zero (though it remains non-negative).

### Distribution
$X_t$ follows a (scaled) **non-central chi-squared distribution** — in contrast to the Vasicek/OU model's normal distribution, reflecting the process's inability to go negative.

### As a short-rate model (Chapter 9)
$$
dr_t = \alpha(\mu-r_t)\,dt+\sigma\sqrt{r_t}\,dW_t.
$$
Bond prices retain the exponential-affine form $B(t,T)=a(t,T)e^{-b(t,T)r_t}$, with $a,b$ solving ODEs derived from the CIR bond-pricing PDE (see [[Interest rate models]]); unlike Vasicek, $B(t,T)$ under CIR guarantees $r_t\ge0$.

### As a variance process (Chapter 6, Heston model)
$$
dv_t = \kappa(\theta-v_t)\,dt+\lambda\sqrt{v_t}\,dW_t^V,
$$
correlated with the asset's own Brownian motion — see [[Stochastic volatility]].

## See also
[[Vasicek Model]], [[Hull-White Model]], [[Interest rate models]], [[Stochastic volatility]], [[Ornstein-Uhlenbeck Process]]
