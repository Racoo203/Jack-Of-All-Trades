---
title: "Credible interval vs Confidence interval"
domain: "Probability & Statistics"
course: "Bayesian Statistics"
unit: "Chapter 3 - Bayesian Inference"
level: MSc
status: drafted
confidence: 0
tags: [bayesian-statistics, classical-statistics, foundations]
---
## Definition
A [[Credible Interval]] is Bayesian: it is a fixed interval that contains a stated posterior *probability* mass of the random parameter $\theta$, conditional on the observed data. A [[Confidence Interval]] is frequentist: $\theta$ is fixed and unknown, and the interval itself is random (a function of the not-yet-observed data); "95% confidence" means 95% of intervals constructed this way, across repeated sampling, would contain the true $\theta$.

## Properties
### The credible interval converges to the confidence interval as the prior becomes vague
For $x\sim N(\theta,\sigma^2)$ with prior $\theta\sim N(\mu,\tau^2)$, the posterior is $N(\mu_1,\sigma_1^2)$ with $\sigma_1^2 = (1/\tau^2+1/\sigma^2)^{-1}$ and $\mu_1 = \sigma_1^2(\mu/\tau^2+x/\sigma^2)$ (see [[Posterior distribution]]). As $\tau^2 \to \infty$ (an increasingly non-informative/flat prior), $\sigma_1^2 \to \sigma^2$ and $\mu_1 \to x$, so
$$
P\left[x-z_{\alpha/2}\sigma < \theta < x+z_{\alpha/2}\sigma \mid x\right] \to 1-\alpha
$$
which is numerically the *same interval* as the classical $100(1-\alpha)\%$ [[Confidence Interval]] for $\theta$ — but the interpretation differs:
- **Frequentist**: the statement $P(x-z_{\alpha/2}\sigma<\theta<x+z_{\alpha/2}\sigma)$ is made *before* $x$ is observed; the randomness is in $x$ (and hence the interval endpoints), not in $\theta$.
- **Bayesian** (flat prior): the analysis is conditional on the observed $x$; the randomness is entirely in $\theta$.

## See also
[[Credible Interval]], [[Confidence Interval]], [[Prior distribution]], [[Posterior distribution]]
