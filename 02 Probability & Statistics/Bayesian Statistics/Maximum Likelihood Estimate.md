---
title: "Maximum Likelihood Estimate"
domain: "Probability & Statistics"
course: "Bayesian Statistics"
unit: "Chapter 2 - Classical Methods of Statistics"
level: MSc
status: drafted
confidence: 0
tags: [bayesian-statistics, classical-statistics, foundations]
---
## Definition
The Maximum Likelihood Estimator (MLE) $\hat\theta$ is the value of $\theta$ that maximizes the [[Likelihood function]] $L(\theta|x)$ (equivalently the log-likelihood $\ell(\theta|x)$) for the observed data:
$$
\hat\theta_{\text{MLE}} = \arg\max_\theta L(\theta|x)
$$
Intuitively, it selects the parameter value under which the observed data was "most likely" to occur.

## Properties
### Worked derivation: Bernoulli MLE
For $X_1,\dots,X_n$ i.i.d. Bernoulli$(p)$, $\ell(p|x) = \left(\sum_i x_i\right)\log p + \left(n-\sum_i x_i\right)\log(1-p)$. Setting the derivative to zero:
$$
\frac{d\ell}{dp} = \frac{\sum_i x_i}{p} - \frac{n-\sum_i x_i}{1-p} = 0 \;\Longrightarrow\; (1-p)\sum_i x_i = p\left(n-\sum_i x_i\right) \;\Longrightarrow\; \hat p = \frac{1}{n}\sum_i x_i = \bar x
$$
The second derivative $\frac{d^2\ell}{dp^2} = -\frac{\sum_i x_i}{p^2}-\frac{n-\sum_i x_i}{(1-p)^2} < 0$ confirms this is a maximum.

### Worked derivation: Normal MLE (known variance)
For $X_1,\dots,X_n$ i.i.d. $N(\theta,\sigma^2=1)$,
$$
\log L(\theta|x) = -\frac{n}{2}\log(2\pi) - \frac{1}{2}\left(\sum_i x_i^2 - 2\theta\sum_i x_i + n\theta^2\right)
$$
$$
\frac{\partial \log L}{\partial \theta} = \sum_i x_i - n\theta = 0 \;\Longrightarrow\; \hat\theta_{\text{MLE}} = \bar x
$$
with $\frac{\partial^2\log L}{\partial\theta^2}=-n<0$ confirming a maximum.

### The MLE is a function of sufficient statistics
In both examples above, $\hat\theta$ depends on the data only through $\sum_i x_i$ — a [[Sufficient statistic]] for the parameter. This is not a coincidence: for exponential-family models, the MLE is always a function of the natural sufficient statistics (see [[Exponential family]]).

### The MLE need not be unbiased
See [[Point estimation]] for worked examples (Uniform$(0,\theta)$, and the "marathon runner" problem) where the MLE is biased.

## Examples
**Insurance claims (Poisson).** Monthly accident counts $212,190,\dots,201$ over 9 months, assumed i.i.d. $\text{Poisson}(\lambda)$: $\hat\lambda = \bar x = 174$, used directly as the prediction for the next month.

**Survey (Bernoulli).** 65 independent Yes/No responses with 17 "Yes": $\hat p = 17/65 \approx 0.26$.

## See also
[[Likelihood function]], [[Point estimation]], [[Fisher Information]], [[Sufficient statistic]]
