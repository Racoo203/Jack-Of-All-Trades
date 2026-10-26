---
title: "Multivariate Itô's Lemma"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "PGT Lectures - Advanced Topics in Option Pricing"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, ito-calculus, multivariate]
---
## Definition
Extends [[Ito's Lemma]] to **two-dimensional stochastic systems**, where two interacting processes evolve simultaneously:
$$
dX_t = Y_t\,dt+tX_t\,dW_t, \qquad dY_t = X_t\,dt+t\,dV_t,
$$
with $W_t,V_t$ independent standard Brownian motions. For a twice-differentiable function $F(t,X_t,Y_t)$, the multivariate Itô formula is
$$
dF = F_t\,dt+F_x\,dX_t+F_y\,dY_t+\tfrac12F_{xx}(dX_t)^2+\tfrac12F_{yy}(dY_t)^2+F_{xy}\,dX_t\,dY_t,
$$
using the multiplication rules $(dX_t)^2=(tX_t)^2dt$, $(dY_t)^2=t^2dt$, and $dX_t\,dY_t=dW_tdV_t=0$ (since $W,V$ are independent).

## Properties
### Worked derivation
For $F(t,X_t,Y_t)=t+X_te^{Y_t}$: $F_t=1,\ F_x=e^{Y_t},\ F_y=X_te^{Y_t},\ F_{xx}=0,\ F_{yy}=X_te^{Y_t},\ F_{xy}=e^{Y_t}$. Substituting,
$$
dF = \left(1+Y_te^{Y_t}+X_t^2e^{Y_t}+\tfrac12t^2X_te^{Y_t}\right)dt + tX_te^{Y_t}(dW_t+dV_t).
$$
Defining $Z_t=\frac{1}{\sqrt2}(W_t+V_t)$ (a standard Brownian motion, since $W_{t+s}-W_t$ and $V_{t+s}-V_t$ are independent $N(0,s)$, so their sum is $N(0,2s)$ and $Z_{t+s}-Z_t\sim N(0,s)$), we have $dW_t+dV_t=\sqrt2\,dZ_t$, giving the compact form
$$
dF = \left(1+Y_te^{Y_t}+X_t^2e^{Y_t}+\tfrac12t^2X_te^{Y_t}\right)dt + \sqrt2\,tX_te^{Y_t}\,dZ_t.
$$

### Application: the Heston model
The [[Stochastic volatility|Heston stochastic volatility model]] is the course's motivating example of a genuine two-dimensional stochastic system: $dS_t=\mu S_t\,dt+\sqrt{v_t}S_t\,dW_t^S$, $dv_t=\kappa(\theta-v_t)\,dt+\sigma_v\sqrt{v_t}\,dW_t^V$, with $dW_t^SdW_t^V=\rho\,dt$ — here the two driving Brownian motions are *correlated* (unlike the independent $W_t,V_t$ above), which is precisely what generates the volatility smile the plain [[Black-Scholes model]] cannot reproduce.

## See also
[[Ito's Lemma]], [[Itô Integral]], [[Stochastic volatility]], [[Cox-Ingersoll-Ross (CIR) Process]]
