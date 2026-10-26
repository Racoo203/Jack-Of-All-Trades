---
title: Invertibility
domain: Stochastic Processes
course: Stochastic Processes
unit: Time Series Analysis
level: MSc
status: seeding
confidence: 0
tags: [seeding]
---
## Definition
Consider an $\mathrm{MA}(q)$ process $y_t = \mu + e_t + \theta_1 e_{t-1} + \cdots + \theta_q e_{t-q} = \mu + \Theta(L) e_t$ (see [[Moving Average Process]]), where $\Theta(L) = 1+\theta_1 L+\cdots+\theta_q L^q$ and $L$ is the [[Lag Operator|lag operator]]. The process is **invertible** if the roots of the characteristic equation
$$\Theta(z) = 1+\theta_1 z + \theta_2 z^2 + \cdots + \theta_q z^q = 0$$
all satisfy $|z|>1$ — exactly the mirror-image condition to [[Stationarity|stationarity]] of an $\mathrm{AR}(p)$ process (which is stated in terms of $\Phi(z)$, not $\Theta(z)$).

Invertibility means the $\mathrm{MA}(q)$ process can be represented as an autoregressive process with an infinite number of lags, $\mathrm{AR}(\infty)$: $e_t$ can be recovered from the (infinite) history of $y_t$.

## Properties
### Derivation for MA(1)
For $y_t = \mu+e_t+\theta_1 e_{t-1} = \mu+(1+\theta_1 L)e_t$, formally invert:
$$e_t = (1+\theta_1 L)^{-1}(y_t-\mu).$$
Using the geometric series $(1+\theta_1 L)^{-1} = \sum_{k=0}^\infty (-\theta_1 L)^k$, valid (in mean square) precisely when $|\theta_1|<1$, gives
$$e_t = \sum_{k=0}^\infty(-\theta_1 L)^k(y_t-\mu) = (y_t-\mu) + \sum_{k=1}^\infty(-\theta_1)^k L^k(y_t-\mu) = (y_t-\mu) + \sum_{k=1}^\infty(-\theta_1)^k(y_{t-k}-\mu),$$
an $\mathrm{AR}(\infty)$ representation of $e_t$ in terms of $\{y_{t-k}\}_{k\ge0}$. So $|\theta_1|<1$ (equivalently, the root of $\Theta(z)=1+\theta_1z=0$, namely $z=-1/\theta_1$, satisfies $|z|>1$) is the MA(1) invertibility condition.

### General MA(q) case
For general $\mathrm{MA}(q)$, $y_t = \mu + \Theta(L)e_t$, the invertibility condition — roots of $\Theta(z)=0$ all outside the unit circle — guarantees $\Theta(L)^{-1}$ exists as a convergent power series in $L$, so $e_t = \Theta(L)^{-1}(y_t-\mu)$ can be expanded as an $\mathrm{AR}(\infty)$ process in $y_t$.

### Why invertibility matters
Unlike stationarity (a property purely of the observable process $y_t$), invertibility is a modelling/identifiability condition: without it, distinct sets of MA coefficients can generate processes with identical autocovariance structure (hence identical likelihoods), so invertibility is imposed to pin down a *unique* MA representation and to make forecasting/estimation ($e_t$ expressible in terms of observed $y$'s) well-defined. See [[Prediction]].

### Relation to ARMA
For a general $\mathrm{ARMA}(p,q)$, $\Phi(L)y_t = \Theta(L)e_t$, the process is stationary iff the roots of $\Phi(z)=0$ lie outside the unit circle, and invertible iff the roots of $\Theta(z)=0$ lie outside the unit circle — the two conditions are independent of each other and act on the AR and MA parts respectively. See [[ARMA Process]].

## See also
- [[Moving Average Process]]
- [[Autoregressive Process]]
- [[ARMA Process]]
- [[Stationarity]]
- [[Lag Operator]]
- [[Prediction]]
