---
title: "Vasicek Model"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "Chapter 9 - Interest Rate Models"
level: MSc
status: seeding
confidence: 0
tags: [financial-derivatives, interest-rate-models, vasicek]
---
## Definition
The **Vasicek model** (Vasicek, 1977) assumes the short rate $r_t$ follows an [[Ornstein-Uhlenbeck Process]] (mean-reverting, constant volatility):
$$
dr_t = \alpha(\mu-r_t)\,dt + \sigma\,dW_t, \qquad \alpha,\mu,\sigma \text{ constant},
$$
where $\alpha$ is the speed of mean reversion, $\mu$ the long-run equilibrium level, and $W_t$ a standard Brownian motion under the risk-neutral measure $Q$.

## Properties
### Solving the SDE
As for any [[Ornstein-Uhlenbeck Process|OU process]], multiply by the integrating factor $e^{\alpha t}$ and integrate over $[0,t]$:
$$
r_t = r_0e^{-\alpha t} + \mu\!\left(1-e^{-\alpha t}\right) + \sigma\!\int_0^te^{-\alpha(t-u)}\,dW_u.
$$

### Distribution of $r_t$
Being a (deterministic-integrand) [[Itô Integral]] plus a deterministic shift, $r_t$ is **normally** distributed:
$$
E[r_t] = r_0e^{-\alpha t}+\mu(1-e^{-\alpha t}), \qquad \operatorname{Var}(r_t) = \frac{\sigma^2}{2\alpha}\left(1-e^{-2\alpha(T-t)}\right).
$$
Because the support of a normal distribution is all of $\mathbb R$, the Vasicek model allows $r_t<0$ with positive probability — its principal shortcoming, mirroring [[Bachelier's Model]]'s flaw for share prices. <!-- UNVERIFIED: variance formula transcribed from a heavily-annotated scanned slide; cross-check against the original PDF -->

### Bond price
$$
B(t,T) = a(t,T)\,e^{-b(t,T)r_t}
$$
for deterministic functions $a(t,T),b(t,T)$ (not derived in the slides — solved by substituting an exponential-affine ansatz into the bond-pricing PDE of [[Interest rate models]] and matching coefficients).

### Instantaneous forward rate
$$
f(t,T) = r_te^{-\alpha(T-t)} + \mu\!\left(1-e^{-\alpha(T-t)}\right) - \frac{\sigma^2}{2\alpha^2}\left(1-e^{-\alpha(T-t)}\right)^2.
$$
<!-- UNVERIFIED: transcribed from a heavily-annotated scanned slide; the derivation via $f(t,T)=-\partial_T\ln B(t,T)$ should be reconstructed and checked -->

## See also
[[Ornstein-Uhlenbeck Process]], [[Interest rate models]], [[Cox-Ingersoll-Ross (CIR) Process]], [[Hull-White Model]]
