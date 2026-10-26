---
title: Prediction
domain: Stochastic Processes
course: Stochastic Processes
unit: Time Series Analysis
level: MSc
status: seeding
confidence: 0
tags: [seeding]
---
## Definition
A **filtration** $\mathcal{F}=\{\mathcal{F}_t\}$ is a collection of $\sigma$-algebras associated with a stochastic process, where $\mathcal{F}_t$ records the information gained by observing the process up to time $t$ (all events of the form $\{X_0\in A_0,\ldots,X_t\in A_t\}$ and their unions). As $t$ increases, $\mathcal{F}_s\subseteq\mathcal{F}_t$ for $s\le t$: the information set only grows.

**Forecasting** (prediction) is the process of predicting future outcomes using past/present information. The forecast of $y_{t+s}$ based on information up to time $t$ is
$$\hat y_{t+s} = E(y_{t+s}\mid \mathcal{F}_t), \qquad s>0.$$
This is the [[Conditional Expectation|conditional expectation]] of $y_{t+s}$ given $\mathcal F_t$, characterised as the random variable $\eta$, fully determined by $\mathcal F_t$, minimising mean-square prediction error: $E(y_{t+s}-\eta)^2 = \min_{\zeta:\,\mathcal F_\zeta\subset\mathcal F_t} E(y_{t+s}-\zeta)^2$ — i.e. $\hat y_{t+s}$ is the best (minimum-MSE) $\mathcal F_t$-measurable predictor of $y_{t+s}$.

## Properties
### Basic conditional-expectation facts used in forecasting
Assuming $\mathcal F$ is complete (all $e_i$, $i\le t$, are known):
$$E(e_t\mid \mathcal F_s) = \begin{cases} e_t, & t\le s\\ 0, & t>s\end{cases}, \qquad E(y_t\mid \mathcal F_s) = \begin{cases} y_t, & t\le s\\ \hat y_t, & t>s\end{cases}.$$
These follow from the general properties: $E(\xi\mid\mathcal G)=\xi$ if $\xi$ is $\mathcal G$-measurable; $E(\xi\mid \mathcal G)=E\xi$ if $\xi$ is independent of $\mathcal G$ (white noise $e_t$ for $t>s$ is independent of $\mathcal F_s$ and has mean $0$).

### Forecasting an MA(q) process
For $y_t=\mu+e_t+\sum_{k=1}^q\theta_k e_{t-k}$ (see [[Moving Average Process]]),
$$\hat y_{t+s} = E(y_{t+s}\mid\mathcal F_t) = \mu+\sum_{k=1}^q\theta_k E(e_{t+s-k}\mid\mathcal F_t), \qquad E(e_{t+s-k}\mid\mathcal F_t)=\begin{cases}e_{t+s-k}, & k\ge s\\ 0, & k<s\end{cases}.$$
So the forecast keeps only the noise terms already realised (indices $\le t$) and drops future ones. In particular, once $s>q$, **every** $e_{t+s-k}$ term is unrealised, so $\hat y_{t+s}=\mu$ for all $s>q$: forecasts beyond the memory length collapse to the unconditional mean — reflecting the finite-memory property of MA processes.

### Forecasting an AR(p) process
For $y_t=\alpha+\sum_{k=1}^p\phi_k y_{t-k}+e_t$ (see [[Autoregressive Process]]),
$$\hat y_{t+s} = \alpha+\sum_{k=1}^p\phi_k E(y_{t+s-k}\mid\mathcal F_t)+E(e_{t+s}\mid\mathcal F_t), \qquad E(y_{t+s-k}\mid\mathcal F_t)=\begin{cases}y_{t+s-k}, & k\ge s\\ \hat y_{t+s-k}, & k<s\end{cases}.$$
This gives a **recursive** forecasting scheme: $\hat y_{t+1}$ is computed directly from observed $y_t,\ldots,y_{t-p+1}$; then $\hat y_{t+2}$ plugs in $\hat y_{t+1}$ in place of the not-yet-observed $y_{t+1}$; and in general, for $s\ge p$, $\hat y_{t+s} = \alpha+\sum_{k=1}^p \phi_k \hat y_{t+s-k}$ (with $\hat y_{t+j}:=y_{t+j}$ for $j\le0$), i.e. the AR forecast recursion mimics the defining recursion itself but with observed values replaced by forecasts once they run out. Unlike MA forecasts, AR forecasts generally do **not** collapse to a constant at any finite horizon (they decay towards $\mu$ as $s\to\infty$ when the process is stationary).

### Forecast accuracy metrics
Given $N$ forecasts $\hat y_{t+s}$ of realised values $y_{t+s}$:
$$\mathrm{MSE}=\frac1N\sum_{t=1}^N(y_{t+s}-\hat y_{t+s})^2, \quad \mathrm{MAE}=\frac1N\sum_{t=1}^N|y_{t+s}-\hat y_{t+s}|, \quad \mathrm{MAPE}=\frac1N\sum_{t=1}^N\left|\frac{y_{t+s}-\hat y_{t+s}}{y_{t+s}}\right|\times100\%.$$
A further diagnostic, **% correct sign predictions** $=\frac1N\sum_t z_{t+s}\times100\%$ with $z_{t+s}=1$ if $y_{t+s}$ and $\hat y_{t+s}$ share sign, $0$ otherwise, matters because MSE/MAE/MAPE alone can rate two forecasts as "equally accurate" even when one has the economically/practically wrong sign (e.g. predicting a surplus when a loss occurs).

### Limitations of forecasting
- All statistical forecasting models are essentially extrapolative.
- Forecasting models are prone to break down around turning points.
- Predictive accuracy usually declines with forecasting horizon.
- Forecasting is not a substitute for judgement.
- Practical tensions: "signal" vs "noise", data-mining risk, simple vs complex models, role of financial/economic theory.

## Examples
**AR(1) model comparison (past exam question):** given $\mathcal F_t$ with observed $y_0,\ldots$ and two candidate coefficients $\phi_1^A=1$ (a [[Random Walk|random walk]], i.e. unit root) vs $\phi_1^B=0.7$, one-step forecasts are $\hat y_{t+1}=\phi_1 y_t$ under each model; computing $\mathrm{MSE}$ over the realised path can show the stationary candidate ($\phi_1^B=0.7$) badly out-predicted here (MSE $17.8$) versus the unit-root candidate (MSE $4.9$) for this particular short realisation — illustrating that stationarity of the *true* model doesn't guarantee a stationary *candidate* model forecasts best on any given finite sample, and that model selection by MSE alone needs care.

## See also
- [[Autoregressive Process]]
- [[Moving Average Process]]
- [[ARMA Process]]
- [[Stationarity]]
- [[Conditional Expectation]]
- [[Random Walk]]
- [[Weak Stationarity]]
