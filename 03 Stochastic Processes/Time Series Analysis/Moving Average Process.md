---
title: Moving Average Process
domain: Stochastic Processes
course: Stochastic Processes
unit: Time Series Analysis
level: MSc
status: seeding
confidence: 0
tags: [seeding]
---
## Definition
Let $\{e_t\}$ be a [[White Noise|white noise]] process with $E(e_t) = 0$ and $\operatorname{var}(e_t) = \sigma^2$, and let $\theta_1, \theta_2, \ldots, \theta_q \in \mathbb{R}$. The process
$$y_t = \mu + e_t + \theta_1 e_{t-1} + \theta_2 e_{t-2} + \cdots + \theta_q e_{t-q}$$
is called a **moving average process of order $q$**, denoted $\mathrm{MA}(q)$.

Using the [[Lag Operator|lag operator]] $L$ (with $Ly_t = y_{t-1}$), writing $\Theta(L) = 1 + \theta_1 L + \cdots + \theta_q L^q$, the process is compactly $y_t = \mu + \Theta(L)e_t$.

## Properties
### Mean
$$E(y_t) = E(\mu) + \sum_{j=0}^q \theta_j E(e_{t-j}) = \mu + \sum_{j=0}^q \theta_j \cdot 0 = \mu, \qquad \theta_0 := 1.$$
This follows since each $e_{t-j}$ is i.i.d. with mean $0$.

### Variance
Since the $e_{t-j}$, $j = 0, \ldots, q$, are i.i.d. with $\operatorname{var}(e_{t-j}) = \sigma^2$ and pairwise uncorrelated,
$$\operatorname{var}(y_t) = \sum_{j=0}^q \operatorname{var}(\theta_j e_{t-j}) = \sum_{j=0}^q \theta_j^2 \sigma^2 = \sigma^2 \sum_{j=0}^q \theta_j^2.$$

### Autocovariance function
$$\gamma_s = \operatorname{cov}(y_t, y_{t-s}) = \operatorname{cov}\!\left(\sum_{i=0}^q \theta_i e_{t-i}, \sum_{j=0}^q \theta_j e_{(t-s)-j}\right) = \sum_{i=0}^q\sum_{j=0}^q \theta_i\theta_j\operatorname{cov}(e_{t-i}, e_{(t-s)-j}).$$
Because $\{e_t\}$ is white noise, $\operatorname{cov}(e_{t-i}, e_{(t-s)-j}) = \sigma^2$ if $t-i = (t-s)-j$, i.e. $i = j+s$, and $0$ otherwise.

**Case $s > q$:** for every $j \ge 0$, $j + s > q$, so $i = j+s$ never holds for $0 \le i \le q$. Hence
$$\gamma_s = 0, \qquad s > q.$$
This is the defining "finite memory" property of $\mathrm{MA}(q)$: observations more than $q$ steps apart are uncorrelated.

**Case $0 \le s \le q$:** the condition $i = j+s$ holds exactly when $0 \le j \le q-s$ (and fails for $j > q-s$), giving
$$\gamma_s = \sigma^2 \sum_{j=0}^{q-s} \theta_j \theta_{j+s}, \qquad 0 \le s \le q,\ \theta_0 := 1.$$

### ACF/PACF signature
For $\mathrm{MA}(q)$: the [[Autocorrelation function|ACF]] $\rho_k$ **cuts off** for $k > q$ (immediate consequence of $\gamma_s = 0$ above), while the [[Autocorrelation Function|PACF]] $\beta_k$ **decays geometrically** as $k \to \infty$. This is the mirror image of the [[Autoregressive Process|AR]] signature and is the standard diagnostic used to identify $q$ from a sample ACF plot.

### Invertibility
An $\mathrm{MA}(q)$ process can (under conditions on $\theta_1,\ldots,\theta_q$) be rewritten as an $\mathrm{AR}(\infty)$ process; see [[Invertibility]].

## Examples
**MA(2):** for $y_t = e_t + \theta_1 e_{t-1} + \theta_2 e_{t-2}$, direct computation (or the formulas above) gives $E(y_t)=0$, $\operatorname{var}(y_t) = (1+\theta_1^2+\theta_2^2)\sigma^2$, $\gamma_1 = \theta_1(1+\theta_2)\sigma^2$, $\gamma_2 = \theta_2\sigma^2$, and $\gamma_s = 0$ for $s \ge 3$.

**MA(1) numeric example:** for $y_t = e_t + \theta e_{t-1}$ with $\theta = 0.7$: $\gamma_0 = 1.49\sigma^2$, $\gamma_1 = 0.7\sigma^2$, $\gamma_s = 0$ for $s \ge 2$, so $\rho_1 = 0.47$. The PACF has the closed form $\beta_k = (-1)^{k+1}\dfrac{(1-\theta^2)\theta^k}{1-\theta^{2(k+1)}}$, decaying geometrically.

## See also
- [[Autoregressive Process]]
- [[ARMA Process]]
- [[Invertibility]]
- [[Stationarity]]
- [[Prediction]]
- [[Weak Stationarity]]
- [[Autocovariance function]]
- [[Mean function]]
- [[Lag Operator]]
