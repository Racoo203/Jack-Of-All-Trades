---
title: "Ruin Theory"
domain: "Probability & Statistics"
course: "Bayesian Statistics"
unit: "Chapter 8 - Risk Theory"
level: MSc
status: drafted
confidence: 0
tags: [bayesian-statistics, actuarial, risk-theory]
---
## Definition
Extending the [[Collective Risk Model]] to continuous time: the **claim number process** $\{N(t)\}_{t\ge0}$ is a **Poisson process** with rate $\lambda$ if (i) $N(t)\sim\text{Poisson}(\lambda t)$; (ii) stationary increments: $N(t)-N(s) \overset{d}{=} N(t-s)$; (iii) independent increments: $N(t)-N(s) \perp N(s)$ for $s<t$. Equivalently, inter-arrival times $T\sim\text{Exp}(\lambda)$, $P(T>t)=e^{-\lambda t}$.

The **surplus (risk) process** is
$$
U(t) = u + ct - S(t), \qquad t\ge0
$$
where $u=U(0)$ is initial capital, $c$ is premium income per unit time, and $S(t)=\sum_{i=1}^{N(t)}X_i$ is a **compound Poisson process** (claims $X_i$ i.i.d., independent of $N(t)$, $N(t)$ Poisson rate $\lambda$).

**Ruin** occurs at time $\tau = \min\{t: U(t)<0\}$ (or $\tau=\infty$ if $U(t)\ge0$ for all $t$). Two ruin probabilities:
$$
\psi(u) = P[\tau<\infty] = P\left[\inf_{t\in[0,\infty)}U(t)<0\right] \quad\text{(infinite-horizon)}
$$
$$
\psi(u,T) = P[\tau\le T] \quad\text{(finite-horizon, $T$ fixed)}
$$
with $\psi(u,T)$ increasing in $T$ and $\lim_{T\to\infty}\psi(u,T)=\psi(u)$.

## Properties
### Premium loading and solvency
$E[U(t)] = u + ct - \lambda t\mu_1 = u+(c-\lambda\mu_1)t$. For the insurer to expect a profit, $c>\lambda\mu_1$ is required; writing $c=(1+\theta)\lambda\mu_1$ defines the **premium loading factor** $\theta>0$. Then:
- $\psi(u)=1$ if $\theta\le0$ (ruin is certain — the insurer is charging too little on average),
- $\psi(u)<1$ if $\theta>0$.

### Normal approximation for a one-period ruin check
For a portfolio with aggregate claims $S$ (mean and variance obtained via [[Collective Risk Model]]), checking ruin only at year-end, the initial capital $U$ needed for ruin probability $\alpha$ solves
$$
P(U+c<S) = \alpha \iff \frac{U+c-E[S]}{\sqrt{\text{Var}(S)}} = z_{1-\alpha}
$$
using the [[Central Limit Theorem (CLT)]]-justified Normal approximation to $S$.

## See also
[[Collective Risk Model]], [[Adjustment Coefficient and Lundberg's Inequality]], [[Central Limit Theorem (CLT)]]
