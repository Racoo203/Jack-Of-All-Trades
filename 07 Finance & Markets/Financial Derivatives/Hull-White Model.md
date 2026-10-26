---
title: "Hull-White Model"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "Chapter 9 - Interest Rate Models"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, interest-rate-models, hull-white]
---
## Definition
The **Hull-White model** extends the [[Vasicek Model]] by letting the long-run mean-reversion level become a **deterministic function of time**, $\mu(t)$, rather than a constant:
$$
dr_t = \alpha\!\left(\mu(t)-r_t\right)dt+\sigma\,dW_t.
$$
There is likewise a CIR-type extension with time-dependent mean and square-root volatility, $dr_t=\alpha(\mu(t)-r_t)dt+\sigma\sqrt{r_t}\,dW_t$ (see the comparison table in [[Interest rate models]]).

## Properties
### Why time-dependence matters
Allowing $\mu(t)$ to vary lets the model be **calibrated exactly to the currently-observed yield curve** — the constant-$\mu$ Vasicek/CIR models generally cannot reproduce every observed bond price simultaneously, whereas choosing $\mu(t)$ appropriately can match the initial term structure exactly. This is the main practical motivation for the extension; the mean-reversion mechanism itself is otherwise identical to Vasicek/CIR.

### Shares the parent model's shortcomings
As a one-factor model, Hull-White inherits the general shortcomings of [[Interest rate models|one-factor short-rate models]] (all maturities driven by a single source of randomness); as the normal-mean-reversion variant, it also shares the Vasicek model's possibility of negative rates unless the CIR-type square-root volatility variant is used instead.

## See also
[[Vasicek Model]], [[Cox-Ingersoll-Ross (CIR) Process]], [[Interest rate models]]
