---
title: "Credible Interval"
domain: "Probability & Statistics"
course: "Bayesian Statistics"
unit: "Chapter 3 - Bayesian Inference"
level: MSc
status: drafted
confidence: 0
tags: [bayesian-statistics, foundations]
---
## Definition
A $(1-\alpha)$ (posterior) credible interval is an interval of $\theta$-values within which $(1-\alpha)$ of the [[Posterior distribution|posterior probability]] lies:
$$
P(\theta \in \text{CI} \mid x) = 1-\alpha
$$

## Properties
### Worked derivation: Normal model
With $x\sim N(\theta,\sigma^2)$ ($\sigma^2$ known) and prior $\theta\sim N(\mu,\tau^2)$, the posterior is $\theta|x \sim N(\mu_1,\sigma_1^2)$ (see [[Posterior distribution]]). Standardizing,
$$
P\left[-z_{\alpha/2} < \frac{\theta-\mu_1}{\sigma_1} < z_{\alpha/2}\right] = 1-\alpha
$$
where $z_{\alpha/2}$ is the $1-\alpha/2$ quantile of $N(0,1)$, so $(\mu_1 - z_{\alpha/2}\sigma_1,\ \mu_1+z_{\alpha/2}\sigma_1)$ is a $100(1-\alpha)\%$ credible interval for $\theta$.

## See also
[[Credible interval vs Confidence interval]], [[Posterior distribution]], [[Confidence Interval]]
