---
title: "Bayesian Linear Regression Model"
domain: "Probability & Statistics"
course: "Bayesian Statistics"
unit: "Chapter 9 - Bayesian linear regression model"
level: MSc
status: drafted
confidence: 0
tags: [bayesian-statistics, regression]
---
## Definition
For response $y=(y_1,\dots,y_n)^T$ and $n\times(p+1)$ predictor matrix $X$ (first column all $1$s), the normal linear model assumes
$$
y \mid \beta,\sigma,X \sim N(X\beta,\ \sigma^2 I), \qquad \mu_i = E(y_i|\beta,X) = \beta_0+x_{i1}\beta_1+\cdots+x_{ip}\beta_p,\ \ \text{Var}(y_i|\sigma,X)=\sigma^2
$$
with $y_i$ conditionally independent given $(\beta,\sigma^2,X)$, and $\theta=(\beta_0,\dots,\beta_p,\sigma)^T$ the full parameter vector.

## Properties
### Classical MLE
The log-likelihood is
$$
\log L(\beta,\sigma|y,X) = -\frac n2\log(2\pi) - \frac n2\log(\sigma^2) - \frac{1}{2\sigma^2}(y-X\beta)^T(y-X\beta)
$$
Differentiating w.r.t. $\beta$ and setting to zero gives the normal equations $X^TX\beta = X^Ty$, so
$$
\hat\beta = (X^TX)^{-1}X^Ty
$$
(unbiased for $\beta$). Differentiating w.r.t. $\sigma^2$ at $\beta=\hat\beta$ gives $\hat\sigma^2 = \frac1n(y-X\hat\beta)^T(y-X\hat\beta)$, which is **biased**; the unbiased version is
$$
s^2 = \frac{1}{n-p-1}(y-X\hat\beta)^T(y-X\hat\beta)
$$
Under normality: $\hat\beta\sim N_{p+1}(\beta,\sigma^2(X^TX)^{-1})$; $\frac{(n-p-1)s^2}{\sigma^2}\sim\chi^2(n-p-1)$; and $\hat\beta$, $s^2$ are independent.

### Standard non-informative prior
The convenient non-informative prior (a [[Jeffrey's prior]]-type choice, matching the $\sigma^{-2}$ result for the Normal model derived in [[Jeffrey's prior]]) is uniform on $(\beta,\log\sigma)$, equivalently
$$
\pi(\beta,\sigma^2|X) \propto \sigma^{-2}
$$

### Posterior factorization and conditional posterior of $\beta$
The joint posterior factors as $\pi(\beta,\sigma^2|y,X) = \pi(\beta|\sigma^2,y,X)\cdot\pi(\sigma^2|y,X)$. Given $\sigma^2$, the posterior for $\beta$ (exponential of a quadratic form in $\beta$, by the same completing-the-square technique as the scalar Normal-Normal case in [[Posterior distribution]]) is
$$
\beta \mid \sigma^2,y,X \sim N(\hat\beta,\ V_\beta\sigma^2), \qquad \hat\beta=(X^TX)^{-1}X^Ty,\ \ V_\beta=(X^TX)^{-1}
$$
i.e. under this non-informative prior, the Bayesian posterior mean for $\beta$ **coincides exactly** with the classical MLE.

### Marginal posterior of $\sigma^2$
$$
\sigma^2 \mid y,X \sim \text{Inv-}\chi^2(n-p-1,\ s^2)
$$
a scaled inverse-$\chi^2$ distribution, with $s^2$ as defined above — again matching the classical unbiased variance estimate. The joint posterior is proper (integrable) provided $n>p$ and $X$ has full column rank $p+1$ (all coefficients identifiable).

### Posterior predictive distribution for new data
For new predictors $\tilde X$ with unobserved outcomes $\tilde y \sim N(\tilde X\beta,\sigma^2 I)$ (given $\beta,\sigma^2$), the posterior predictive distribution $\pi(\tilde y|y,X,\tilde X)$ averages over the posterior uncertainty in $(\beta,\sigma^2)$ (see [[Posterior predictive distribution]] for the general construction). Conditioning first on $\sigma$:
$$
E[\tilde y|\sigma,y,X,\tilde X] = E\big[E[\tilde y|\beta,\sigma,\dots]\,\big|\,\sigma,\dots\big] = E[\tilde X\beta|\sigma,\dots] = \tilde X\hat\beta
$$
$$
\text{Var}[\tilde y|\sigma,y,X,\tilde X] = E[\text{Var}[\tilde y|\beta,\sigma,\dots]|\sigma,\dots] + \text{Var}[E[\tilde y|\beta,\sigma,\dots]|\sigma,\dots] = \sigma^2 I + \sigma^2\tilde X V_\beta \tilde X^T = (I+\tilde X V_\beta \tilde X^T)\sigma^2
$$
— two variance sources: $\sigma^2 I$ (pure sampling noise) and $\sigma^2\tilde XV_\beta\tilde X^T$ (posterior parameter uncertainty in $\beta$, which vanishes only as $n\to\infty$). Averaging further over the marginal (scaled inverse-$\chi^2$) posterior of $\sigma^2$, $\pi(\tilde y|y,X,\tilde X)$ is a **multivariate $t$** distribution centred at $\tilde X\hat\beta$ with scale matrix $s^2(I+\tilde XV_\beta\tilde X^T)$ and $n-p-1$ degrees of freedom (stated in the course as non-examinable detail).

## See also
[[Posterior distribution]], [[Posterior predictive distribution]], [[Jeffrey's prior]], [[Maximum Likelihood Estimate]]
