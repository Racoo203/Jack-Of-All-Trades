---
title: "Reduced-Form Credit Risk Model"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "Chapter 10 - Credit Risk"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, credit-risk, hazard-rate, intensity-based]
---
## Definition
Unlike [[Merton Model (Credit Risk)|Merton's structural model]], a **reduced-form (intensity-based) model** does not look inside the firm; default is triggered by an exogenous **hazard rate** $\lambda$ (also called the default **intensity**), exactly the [[Hazard Function|hazard-rate]] framework from survival analysis applied to a "lifetime until default" rather than a lifetime until death.

## Properties
### Poisson/hazard-rate default counting
Treating default as a rare event with rate $\lambda$ per unit time over a loan of $T$ days, the number of defaults in $T$ days is (approximately) Poisson, and — restricting to at most one default — the risk-neutral expected value of a loan of principal $L$ with no recovery is
$$
E^Q[\text{value of loan}] = Le^{-\lambda T}.
$$
To make the expected repayment equal $L$, the lender must charge $Le^{\lambda T}$ up front, so $(Le^{\lambda T})e^{-\lambda T}=L$: the hazard rate directly inflates the required loan rate.

### Including a recovery rate
Let default occur at a (random) time $\tau$. If default occurs by $T$ ($\tau\le T$), the investor receives a recovery fraction $\delta$ at $T$; otherwise the full payment. The payoff is
$$
\mathbb 1_{\{T<\tau\}} + \delta\,\mathbb 1_{\{\tau\le T\}}.
$$
Treating the credit-risky asset as a derivative and applying [[Risk-neutral pricing]] (with $C_t$ the money-market account, $r$ constant, and assuming default is independent of $C_t$):
$$
v(t,T) = P(t,T)\left[1-(1-\delta)q(t,T)\right],
$$
where $P(t,T)=e^{-r(T-t)}$ is the risk-free ZCB price and $q(t,T)$ is the risk-neutral probability that default occurs before $T$. Writing the risk-neutral **survival probability** as $e^{-\int_t^T\lambda(s)\,ds}$ (directly analogous to the survival function $S(t)=e^{-\int_0^tH'(u)du}$ of [[Hazard Function|survival analysis]]),
$$
v(t,T) = P(t,T)\left[1-(1-\delta)\left(1-e^{-\int_t^T\lambda(s)\,ds}\right)\right],
$$
and inverting for the implied default probability,
$$
q(t,T) = \frac{1}{1-\delta}\left[1-\frac{v(t,T)}{P(t,T)}\right].
$$

## See also
[[Credit Risk]], [[Merton Model (Credit Risk)]], [[Hazard Function]], [[Risk-neutral pricing]]
