---
title: ARMA Process
domain: Stochastic Processes
course: Stochastic Processes
unit: Time Series Analysis
level: MSc
status: seeding
confidence: 0
tags: [seeding]
---
## Definition
To model data whose autocorrelation depends both on its own lagged values and on lagged white-noise shocks simultaneously, the [[Autoregressive Process|AR($p$)]] and [[Moving Average Process|MA($q$)]] processes are combined into the **$\mathrm{ARMA}(p,q)$ process**:
$$y_t = \alpha + \phi_1 y_{t-1} + \cdots + \phi_p y_{t-p} + e_t + \theta_1 e_{t-1} + \cdots + \theta_q e_{t-q},$$
where $\{e_t\}$ is [[White Noise|white noise]]. Moving all $y$-terms to the left (taking $\alpha = 0$ WLOG) and using the [[Lag Operator|lag operator]] $L$:
$$\Phi(L) y_t = \Theta(L) e_t, \qquad \Phi(L) = 1-\phi_1 L - \cdots - \phi_p L^p, \quad \Theta(L) = 1+\theta_1 L + \cdots + \theta_q L^q,$$
where $\Phi(L)$ is the **AR (characteristic) polynomial** and $\Theta(L)$ is the **MA polynomial**.

## Properties
### Stationarity and invertibility conditions
The conditions on $\phi_1,\ldots,\phi_p$ and $\theta_1,\ldots,\theta_q$ that ensure stationarity/invertibility of $\mathrm{ARMA}(p,q)$ **coincide** with those for the pure $\mathrm{AR}(p)$ and pure $\mathrm{MA}(q)$ components respectively (the AR part governs stationarity, the MA part governs invertibility — see [[Stationarity]] and [[Invertibility]]):
- $\mathrm{ARMA}(p,q)$ is **stationary** iff every root of $\Phi(z) = 1-\phi_1 z - \cdots -\phi_p z^p = 0$ satisfies $|z|>1$.
- $\mathrm{ARMA}(p,q)$ is **invertible** iff every root of $\Theta(z) = 1+\theta_1 z+\cdots+\theta_q z^q = 0$ satisfies $|z|>1$.

### ARIMA(p,d,q) as a generalisation
Applying the [[Difference Operator|difference operator]] $\nabla = 1-L$ $d$ times to a non-stationary series before fitting an $\mathrm{ARMA}(p,q)$ model to the differenced series gives the **$\mathrm{ARIMA}(p,d,q)$ process**:
$$\left(1-\sum_{k=1}^p \phi_k L^k\right)\nabla^d y_t = \alpha + \left(1+\sum_{k=1}^q \theta_k L^k\right) e_t.$$
Special cases: $\mathrm{ARIMA}(p,0,0) = \mathrm{AR}(p)$; $\mathrm{ARIMA}(0,0,q) = \mathrm{MA}(q)$; $\mathrm{ARIMA}(0,0,0)$ is white noise plus a constant; $\mathrm{ARIMA}(0,1,0)$: $y_t-y_{t-1}=\alpha+e_t \Rightarrow y_t = \sum_{i\le t}(\alpha+e_i)$, i.e. a [[Random Walk|random walk]].

## Examples
**Stationarity/invertibility check, ARMA(2,2):** for $y_t = -\tfrac1{10}y_{t-1}+\tfrac15 y_{t-2}+e_t-\tfrac56 e_{t-1}+\tfrac16 e_{t-2}$, $\Phi(z)=1+\tfrac1{10}z-\tfrac15z^2=0$ has roots $z=\tfrac52,\,-2$ (both $|z|>1\Rightarrow$ stationary); $\Theta(z)=1-\tfrac56z+\tfrac16z^2=0$ has roots $z=2,\,3$ (both $|z|>1\Rightarrow$ invertible).

**Covariances with the driving noise:** for the same process, using bilinearity of covariance, uncorrelatedness of $e_t$ with $y_{t-1},y_{t-2}$, and stationarity to identify $\operatorname{cov}(y_{t-1},e_{t-1})=\operatorname{cov}(y_t,e_t)$, one finds $\operatorname{cov}(y_t,e_t)=\sigma^2$, $\operatorname{cov}(y_t,e_{t-1})=-\tfrac{14}{15}\sigma^2$, $\operatorname{cov}(y_t,e_{t-2})=\tfrac{69}{150}\sigma^2$ — a pattern useful for MSE-type derivations in exam questions.

**Rewriting an AR(2) via a unit-root factor:** $y_t=\tfrac32 y_{t-1}-\tfrac12 y_{t-2}+e_t+\tfrac15 e_{t-1}$, an $\mathrm{ARMA}(2,1)$, factors as $\left(1-\tfrac12L\right)(1-L)y_t = e_t+\tfrac15e_{t-1}$, i.e. $\left(1-\tfrac12L\right)\nabla y_t = e_t+\tfrac15 e_{t-1}$ — an $\mathrm{ARIMA}(1,1,1)$ process, and letting $w_t=\nabla y_t$, $w_t = \tfrac12 w_{t-1}+e_t+\tfrac15e_{t-1}$ is $\mathrm{ARMA}(1,1)$.

## See also
- [[Autoregressive Process]]
- [[Moving Average Process]]
- [[Invertibility]]
- [[Stationarity]]
- [[Prediction]]
- [[Weak Stationarity]]
- [[Lag Operator]]
- [[Difference Operator]]
- [[Random Walk]]
