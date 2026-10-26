---
title: "Proportional Hazards Model"
domain: Probability & Statistics
course: Survival Analysis
unit: "Chapter 5 - The proportional hazard model"
level: MSc
status: drafted
confidence: 0
tags: [survival-analysis, proportional-hazards, regression]
---
## Definition
Regression models let the survival distribution differ by individual covariates. The **(parametric) proportional hazards (PH) model** for a single covariate $x$ is
$$
h(t\mid x) = h_0(t)\exp(x\beta)
$$
where $h_0(t)$ is the **baseline hazard** (the hazard when $x=0$), $t$ is time, and $\beta$ is a parameter to estimate, giving the relationship between $x$ and the hazard.

## Properties
### Constant hazard ratio
For two individuals with covariate values $x$ and $x^*$,
$$
\frac{h(t\mid x)}{h(t\mid x^*)} = \frac{h_0(t)\exp(x\beta)}{h_0(t)\exp(x^*\beta)} = \exp[(x-x^*)\beta]
$$
The hazard ratio does not depend on $t$ — "proportional hazards". When $x-x^*=1$, $\beta = \ln\left(\dfrac{h(t\mid x)}{h(t\mid x^*)}\right)$ is the log hazard ratio.

### Parametric baseline choices
- **Gompertz PH model**: baseline $h_0(t)=c^t$, with $B=\exp(\beta x)$ substituted into [[Gompertz' Law|Gompertz' law]] $h(t)=Bc^t$, giving $h(t\mid x) = c^t\exp(\beta x)$. Log-hazard is linear in $t$ and $x$: $\ln h(t\mid x) = t\ln c + \beta x$. (In general, log-hazards of PH models are linear in the covariates.)
- **Weibull PH model**: baseline $h_0(t)=\alpha\lambda t^{\alpha-1}$ (see [[Parametric Survival Models]]), giving $h(t\mid x)=\lambda\alpha t^{\alpha-1}\exp(\beta x)$; writing $\lambda_1=\lambda\exp(\beta x)$, this is a Weibull hazard with rate $\lambda_1$ and shape $\alpha$.

### Survival function and likelihood
$$
S(t\mid x) = \exp\left(-\int_0^t h(u\mid x)\,du\right) = \exp\left(-\exp(\beta x)\int_0^t h_0(u)\,du\right)
$$
With [[Likelihood Function for Censored Survival Data|censoring indicator]] $\delta_i$, the log-likelihood is $\ln L = \sum_i \{\delta_i\ln h(t_i\mid x_i) + \ln S(t_i\mid x_i)\}$. For the Weibull PH model this expands (dropping constants) to
$$
\sum_{i=1}^n \{\delta_i(\beta x_i+\ln(\lambda\alpha)+\alpha\ln t_i) - \lambda\exp(\beta x_i)t_i^\alpha\}
$$
maximised numerically for $\alpha,\lambda,\beta$.

### Multivariate form
With $p$ covariates $x_1,\dots,x_p$:
$$
h(t\mid x_1,\dots,x_p) = h_0(t)\exp(x_1\beta_1+\cdots+x_p\beta_p) = h_0(t)\exp(X\vec\beta)
$$
in matrix form, with covariate matrix $X$ ($n\times p$) and coefficient vector $\vec\beta$.

## See also
[[Cox Proportional Hazards Model]], [[Gompertz' Law]], [[Parametric Survival Models]], [[Likelihood Function for Censored Survival Data]]
