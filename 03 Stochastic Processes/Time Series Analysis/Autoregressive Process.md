---
title: Autoregressive Process
domain: Stochastic Processes
course: Stochastic Processes
unit: Time Series Analysis
level: MSc
status: seeding
confidence: 0
tags: [seeding]
---
## Definition
An **autoregressive process of order $p$**, $\mathrm{AR}(p)$, is defined by
$$y_t = \alpha + \phi_1 y_{t-1} + \phi_2 y_{t-2} + \cdots + \phi_p y_{t-p} + e_t,$$
where $\alpha$ is a constant and $\{e_t\}$ is a [[White Noise|white noise]] process. Using the [[Lag Operator|lag operator]] $L$,
$$y_t = \alpha + \sum_{k=1}^p \phi_k L^k y_t + e_t \quad\Longrightarrow\quad \Phi(L) y_t = \alpha + e_t, \qquad \Phi(L) := 1 - \phi_1 L - \cdots - \phi_p L^p,$$
where $\Phi(L)$ is the **characteristic polynomial** of the process.

## Properties
### Stationarity condition
See [[Stationarity]] for the full statement and proofs: an $\mathrm{AR}(p)$ process is (weakly) stationary iff every root of $\Phi(z) = 1-\phi_1 z - \cdots - \phi_p z^p = 0$ satisfies $|z|>1$.

### AR(1) as an MA($\infty$) process
For $y_t = \alpha + \phi_1 y_{t-1} + e_t$, repeatedly back-substituting $y_{t-k} = \alpha + \phi_1 y_{t-k-1} + e_{t-k}$ gives, after $k = 1, 2, 3, \ldots$ steps,
$$y_t = (1+\phi_1+\phi_1^2+\cdots)\alpha + (e_t + \phi_1 e_{t-1} + \phi_1^2 e_{t-2} + \cdots) = \sum_{k=0}^\infty \phi_1^k \alpha + \sum_{k=0}^\infty \phi_1^k e_{t-k},$$
i.e. $y_t = \mu + \sum_{k=0}^\infty \theta_k e_{t-k}$ with $\theta_k = \phi_1^k$ and $\mu = \sum_{k=0}^\infty \phi_1^k \alpha$ — an $\mathrm{MA}(\infty)$ representation, which converges (in mean square) precisely when $|\phi_1| < 1$.

### Mean, variance, autocovariance of stationary AR(1)
If $|\phi_1| < 1$, summing the geometric series above:
$$E(y_t) = \mu = \frac{\alpha}{1-\phi_1}, \qquad \operatorname{var}(y_t) = \sigma^2\sum_{k=0}^\infty \phi_1^{2k} = \frac{\sigma^2}{1-\phi_1^2}, \qquad \gamma_s = \operatorname{cov}(y_t,y_{t-s}) = \frac{\sigma^2 \phi_1^{s}}{1-\phi_1^2}.$$
If $|\phi_1|\ge 1$, $E(y_t)\to\infty$, so the process cannot be stationary — this is why $|\phi_1|<1$ is exactly the AR(1) stationarity condition (consistent with the characteristic-root criterion: $\Phi(z)=1-\phi_1 z=0 \Rightarrow z = 1/\phi_1$, and $|z|>1 \iff |\phi_1|<1$).

### Mean of a stationary AR(p)
Assuming stationarity ($E(y_t)=\mu$ for all $t$), taking expectations of the defining recursion:
$$\mu = \alpha + \phi_1\mu + \cdots + \phi_p\mu \quad\Longrightarrow\quad \mu = \frac{\alpha}{1-\phi_1-\phi_2-\cdots-\phi_p}.$$

### Variance of a stationary AR(p)
Writing $\operatorname{var}(y_t)=\sigma_y^2$ for all $t$ and expanding $\operatorname{var}\!\left(\sum_k \phi_k y_{t-k} + e_t\right)$,
$$\sigma_y^2 = \sigma^2 + \sigma_y^2\sum_{k=1}^p \phi_k^2 + \sigma_y^2\!\!\sum_{1\le i\neq j\le p}\!\!\phi_i\phi_j\rho_{(i-j)} \quad\Longrightarrow\quad \sigma_y^2 = \frac{\sigma^2}{1-\sum_{k=1}^p \phi_k^2 - \sum_{i\neq j}\phi_i\phi_j\rho_{(i-j)}},$$
where the $\rho_s$ come from the Yule–Walker equations below.

### Yule–Walker equations
For a stationary $\mathrm{AR}(p)$, taking $\operatorname{cov}(\cdot, y_{t-s})$ of the defining recursion,
$$\operatorname{cov}(y_t,y_{t-s}) = \phi_1\operatorname{cov}(y_{t-1},y_{t-s}) + \cdots + \phi_p\operatorname{cov}(y_{t-p},y_{t-s}) + \operatorname{cov}(e_t,y_{t-s}) = \sum_{i=1}^p \phi_i \gamma_{s-i},$$
(the $\operatorname{cov}(e_t,y_{t-s})$ term vanishes for $s>0$ since $e_t$ is uncorrelated with the past). Dividing through by $\gamma_0$ gives the **Yule–Walker equations**:
$$\rho_s = \sum_{i=1}^p \phi_i \rho_{s-i}, \qquad s \ge 1,$$
a $p$-th order linear difference equation in $s$ (with $\rho_0=1$, $\rho_{-k}=\rho_k$), whose general solution is a linear combination of $z_i^{-s}$ built from the roots $z_i$ of the characteristic polynomial $\Phi(z)=0$.

### ACF/PACF signature
For any $\mathrm{AR}(p)$: the ACF $\rho_k$ **decays geometrically** (or as a mixture of decaying/oscillating geometric terms, for $p\ge2$) as $k\to\infty$, while the PACF $\beta_k$ **cuts off** for $k>p$ — mirror image of the [[Moving Average Process|MA]] signature; this is the standard Box–Jenkins identification rule.

## Examples
**AR(1), $\phi_1=0.7$:** Yule–Walker gives $\rho_s = \phi_1^s$, e.g. $\rho_1=0.7,\ \rho_2=0.49,\ \rho_3=0.343,\ldots$; PACF is $\beta_1=0.7$, $\beta_k=0$ for $k\ge2$.

**AR(2) Yule–Walker, worked example:** For $y_t = \tfrac{1}{12}y_{t-1}+\tfrac{1}{24}y_{t-2}+e_t$: characteristic polynomial $\Phi(z)=1-\tfrac1{12}z-\tfrac1{24}z^2=0$ has roots $z_1=-6,\ z_2=4$, both $|z_i|>1$, so stationary. Yule–Walker: $\rho_s = \tfrac1{12}\rho_{s-1}+\tfrac1{24}\rho_{s-2}$; solving for $s=1$ with $\rho_0=1,\ \rho_{-1}=\rho_1$ gives $\rho_1 = 2/23$; solving the resulting second-order linear difference equation in closed form gives $\rho_s = \tfrac{9}{23}\left(-\tfrac16\right)^s + \tfrac{14}{23}\left(\tfrac14\right)^s$, $s\ge0$.

**AR(3) non-stationary example:** $y_t = 3y_{t-1}-2.75y_{t-2}+0.75y_{t-3}+e_t$ has characteristic roots $z_1=1,\ z_2=\tfrac23,\ z_3=2$; since $z_1,z_2$ don't satisfy $|z|>1$, the process is not stationary (and $z=1$ signals a **unit root**).

## See also
- [[Moving Average Process]]
- [[ARMA Process]]
- [[Stationarity]]
- [[Invertibility]]
- [[Prediction]]
- [[Weak Stationarity]]
- [[Autocovariance function]]
- [[Mean function]]
- [[Lag Operator]]
- [[Random Walk]]
