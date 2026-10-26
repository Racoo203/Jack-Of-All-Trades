---
title: Stationarity
domain: Stochastic Processes
course: Stochastic Processes
unit: Time Series Analysis
level: MSc
status: seeding
confidence: 0
tags: [seeding]
---
## Definition
This note does **not** redefine stationarity from scratch — the general probabilistic definitions live at [[Weak Stationarity]] (mean constant, autocovariance a function of lag only, finite second moments) and [[Strong Stationarity]] (finite-dimensional distributions invariant under time shifts), and the time-series lecture's own statements match those exactly:
- **Strictly stationary:** $\Pr(y_{t_1}\le b_1,\ldots,y_{t_n}\le b_n) = \Pr(y_{t_1+m}\le b_1,\ldots,y_{t_n+m}\le b_n)$ for all $n,m>0,\ t_1,\ldots,t_n,\ b_1,\ldots,b_n$ — this **is** [[Strong Stationarity]] restated for a discrete-time series $\{y_t\}$.
- **Weakly stationary:** $E(y_t)=\mu$ for all $t$, and $\operatorname{cov}(y_{t_2},y_{t_1})=\gamma(t_2-t_1)$ for all $t_1,t_2$ — this **is** [[Weak Stationarity]] restated, with $\gamma$ the [[Autocovariance function|autocovariance function]] at lag $s=t_2-t_1$ (so $\gamma_s=\gamma_{-s}$ by symmetry of covariance), and it implies $\operatorname{var}(y_t)=\sigma^2<\infty$ for all $t$.

What's genuinely **specific to the time-series unit** is not the definition itself but *checkable algebraic conditions* for when an $\mathrm{AR}$/$\mathrm{MA}$/$\mathrm{ARMA}$ process (built from parameters $\phi_i,\theta_j$) satisfies weak stationarity — that is the content below.

## Properties
### The characteristic-root criterion for AR(p)
**Lemma.** An $\mathrm{AR}(p)$ process $\Phi(L)y_t = \alpha+e_t$, with characteristic polynomial $\Phi(z)=1-\phi_1z-\phi_2z^2-\cdots-\phi_pz^p$, is (weakly) stationary if and only if every root of $\Phi(z)=0$ satisfies $|z|>1$ (lies outside the unit circle).

*Why (sketch, standard textbook argument beyond what the slides prove explicitly for general $p$; the slides prove only the $p=1$ case in full — see [[Autoregressive Process]]):* factor $\Phi(z) = \prod_{i=1}^p(1-z/z_i)$ over the roots $z_1,\ldots,z_p$ of $\Phi$. By partial fractions, $1/\Phi(L)$ can (when the $z_i$ are distinct) be written as $\sum_i c_i/(1-L/z_i)$, and each term expands as a convergent geometric series $\sum_k (L/z_i)^k$ **iff** $|1/z_i|<1$, i.e. $|z_i|>1$. When all roots satisfy this, $y_t = \Phi(L)^{-1}(\alpha+e_t)$ has a legitimate $\mathrm{MA}(\infty)$ representation with mean-square-summable coefficients, which is stationary; if any root has $|z_i|\le1$ the inversion fails (diverges or is non-causal), and $y_t$ is not stationary. The $p=1$ case makes this concrete: $\Phi(z)=1-\phi_1z=0 \Rightarrow z=1/\phi_1$, and $|z|>1\iff|\phi_1|<1$, exactly the condition under which the AR(1)-as-MA($\infty$) series converges (derived in full in [[Autoregressive Process]]).

### Unit roots
If $\Phi(z)=0$ has a root exactly on the unit circle (most commonly $z=1$), the process has a **unit root** and is non-stationary but not explosive — e.g. $y_t=y_{t-1}+e_t$ (a [[Random Walk|random walk]]) has $\Phi(z)=1-z$, root $z=1$. Unit-root series are typically made stationary by differencing (the $d$ in [[ARMA Process|ARIMA$(p,d,q)$]]): applying the [[Difference Operator|difference operator]] $\nabla=1-L$ removes a unit root from $\Phi(z)$.

### Mirror condition for MA(q): invertibility, not stationarity
An $\mathrm{MA}(q)$ process $y_t=\mu+\Theta(L)e_t$ is **always** weakly stationary for any choice of $\theta_1,\ldots,\theta_q$ (finite sums/linear combinations of white noise are automatically stationary — see the mean/variance/autocovariance derivations in [[Moving Average Process]], none of which required any condition on the $\theta_j$). The analogous characteristic-root condition on $\Theta(z)$ instead governs **[[Invertibility]]** (existence of an $\mathrm{AR}(\infty)$ representation), not stationarity — a common point of confusion.

### ARMA(p,q): stationarity from the AR part only
For $\Phi(L)y_t=\Theta(L)e_t$, stationarity depends **only** on the roots of $\Phi(z)=0$ (the AR/autoregressive polynomial) lying outside the unit circle — the MA part never affects stationarity, only invertibility. See [[ARMA Process]] for the paired statement and worked examples.

## Examples
**AR(3), non-stationary:** $y_t=3y_{t-1}-2.75y_{t-2}+0.75y_{t-3}+e_t \Rightarrow \Phi(z)=1-3z+2.75z^2-0.75z^3=0$ has roots $z_1=1,\ z_2=\tfrac23,\ z_3=2$; since $|z_1|,|z_2|\not>1$, the process is not stationary (and $z_1=1$ flags a unit root).

**AR(2) built from a unit-root factor:** $\nabla y_{t}=0.8\nabla y_{t-1}+e_t$ rewrites as $y_t=1.8y_{t-1}-0.8y_{t-2}+e_t$, with $\Phi(z)=1-1.8z+0.8z^2=0$ having roots $z_1=1,\ z_2=1.25$; $z_1=1$ fails $|z|>1$, so $\{y_t\}$ is non-stationary — consistent with it being defined as the *first difference* of a stationary AR(1) process (i.e. $\{y_t\}$ is $\mathrm{ARIMA}(1,1,0)$).

## See also
- [[Weak Stationarity]]
- [[Strong Stationarity]]
- [[Autoregressive Process]]
- [[Moving Average Process]]
- [[ARMA Process]]
- [[Invertibility]]
- [[Random Walk]]
- [[Autocovariance function]]
- [[Mean function]]
- [[Difference Operator]]
- [[Lag Operator]]
