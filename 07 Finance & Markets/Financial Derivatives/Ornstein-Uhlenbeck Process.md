---
title: "Ornstein-Uhlenbeck Process"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "Chapter 3 - The Itô Integral"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, stochastic-calculus, mean-reversion]
---
## Definition
The **Ornstein-Uhlenbeck (OU) process** is a common model in finance (alongside [[Geometric Brownian Motion]]) satisfying the stochastic differential equation
$$
dX_t = -\gamma X_t\,dt + \sigma\,dB_t, \qquad \gamma>0,
$$
where $B_t$ is a standard [[Brownian motion]]. It is the prototypical **mean-reverting** diffusion: the drift $-\gamma X_t$ always pulls $X_t$ back towards $0$ (or, in the shifted form $dX_t=\gamma(\theta-X_t)dt+\sigma dB_t$, towards a long-run level $\theta$), at a speed governed by $\gamma$.

## Properties
### Solution via an integrating factor
Multiply both sides by the integrating factor $e^{\gamma t}$:
$$
d\!\left(e^{\gamma t}X_t\right) = \gamma e^{\gamma t}X_t\,dt + e^{\gamma t}dX_t = e^{\gamma t}\sigma\,dB_t
$$
(using [[Ito's Lemma]] on $f(x,t)=e^{\gamma t}x$, which has no second-order term since $f$ is linear in $x$). Integrating over $[0,t]$:
$$
e^{\gamma t}X_t - X_0 = \sigma\int_0^t e^{\gamma s}\,dB_s \quad\Longrightarrow\quad X_t = X_0e^{-\gamma t} + \sigma\int_0^t e^{-\gamma(t-s)}\,dB_s.
$$

### Distribution of $X_t$
Since the stochastic integral above is a (deterministic-integrand) [[Itô Integral]], $X_t$ is normally distributed:
$$
X_t \sim N\!\left(X_0e^{-\gamma t},\ \frac{\sigma^2}{2\gamma}\left(1-e^{-2\gamma t}\right)\right).
$$
As $t\to\infty$, $E[X_t]\to0$ and $\operatorname{Var}(X_t)\to \sigma^2/(2\gamma)$: the process reaches a stationary distribution, unlike [[Brownian motion]] whose variance grows without bound.

### Relation to interest-rate models
The OU process (with a level-shifted mean) is exactly the [[Vasicek Model]]'s short-rate dynamics, and its square-root cousin is the [[Cox-Ingersoll-Ross (CIR) Process]] — both chosen in Chapter 9 specifically for this mean-reverting behaviour, which real interest rates and volatilities exhibit but plain GBM cannot capture.

## See also
[[Ito's Lemma]], [[Itô Integral]], [[Geometric Brownian Motion]], [[Vasicek Model]], [[Cox-Ingersoll-Ross (CIR) Process]]
