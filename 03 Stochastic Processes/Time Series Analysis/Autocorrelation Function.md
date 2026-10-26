---
title: Autocorrelation Function
domain: Stochastic Processes
course: Stochastic Processes
unit: Time Series Analysis
level: MSc
status: seeding
confidence: 0
tags: [seeding]
---
## Definition
For a (weakly) [[Weak Stationarity|stationary]] [[Stochastic Process|process]] $\{y_t\}$ with [[Autocovariance function|autocovariance function]] $\gamma_s = \operatorname{cov}(y_t, y_{t-s})$, the **autocorrelation function** (ACF) at lag $s$ is
$$
\rho_s = \frac{\gamma_s}{\gamma_0} = \operatorname{corr}(y_t, y_{t-s}),
$$
the correlation between observations $s$ steps apart, normalized so that $\rho_0 = 1$ and $|\rho_s| \leq 1$.

The **partial autocorrelation function** (PACF), denoted $\beta_k$ (or $\phi_{kk}$), measures the correlation between $y_t$ and $y_{t-k}$ *after removing* the linear dependence explained by the intermediate observations $y_{t-1}, \dots, y_{t-k+1}$. Equivalently, $\beta_k$ is the coefficient of $y_{t-k}$ in the population linear regression of $y_t$ on $y_{t-1}, \dots, y_{t-k}$.

## Properties
### ACF/PACF as a diagnostic pair
The ACF and PACF have complementary "signatures" for the two basic linear models, used in practice to identify a model's order from a sample plot:
- For an [[Moving Average Process|$\mathrm{MA}(q)$]] process: the ACF **cuts off** after lag $q$ (i.e. $\rho_s = 0$ for $s > q$, since $\gamma_s = 0$ there), while the PACF **decays** (geometrically or in a damped sinusoid) as $k \to \infty$.
- For an [[Autoregressive Process|$\mathrm{AR}(p)$]] process: the ACF **decays** as $s \to \infty$ (geometrically, or as a damped sinusoid, depending on the roots of the characteristic polynomial), while the PACF **cuts off** after lag $p$ (i.e. $\beta_k = 0$ for $k > p$).

This "mirrored cutoff/decay" behaviour is the standard tool for reading off a candidate order $(p, q)$ from sample ACF/PACF plots when fitting an [[ARMA Process|ARMA]] model.

### Worked example (MA(1))
For $y_t = e_t + \theta e_{t-1}$, the ACF is $\rho_1 = \dfrac{\theta}{1+\theta^2}$, $\rho_s = 0$ for $s \geq 2$ — a clean cutoff at lag $1$. The PACF instead decays geometrically:
$$
\beta_k = (-1)^{k+1} \frac{(1-\theta^2)\theta^k}{1 - \theta^{2(k+1)}}, \qquad k \geq 1.
$$

## See also
- [[Autocovariance function]]
- [[Moving Average Process]]
- [[Autoregressive Process]]
- [[ARMA Process]]
- [[Weak Stationarity]]
- [[White Noise]]
