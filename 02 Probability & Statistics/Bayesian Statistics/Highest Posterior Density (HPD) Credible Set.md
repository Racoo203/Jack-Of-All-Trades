---
title: "Highest Posterior Density (HPD) Credible Set"
domain: "Probability & Statistics"
course: "Bayesian Statistics"
unit: "Chapter 5 - Bayesian Hypothesis Testing"
level: MSc
status: drafted
confidence: 0
tags: [bayesian-statistics, foundations]
---
## Definition
A $100(1-\alpha)\%$ credible set for $\theta$ is any subset $C\subseteq\Theta$ with
$$
1-\alpha \le P[C|x] = \begin{cases}\int_C \pi(\theta|x)\,d\theta & \text{continuous}\\ \sum_{\theta\in C}\pi(\theta|x) & \text{discrete}\end{cases}
$$
This generalizes the (interval-shaped) [[Credible Interval]] to arbitrary subsets of $\Theta$. Because the posterior is a genuine probability distribution, $P[C|x]$ can be interpreted directly as "the probability $\theta \in C$" — unlike a classical [[Confidence Interval]], which can only be given a pre-data coverage-probability interpretation.

To make the credible set as small (informative) as possible, it should contain only the values of $\theta$ with the highest posterior density — this is the **highest posterior density (HPD)** credible set:
$$
C = \{\theta\in\Theta : \pi(\theta|x) \ge k(\alpha)\}
$$
where $k(\alpha)$ is the largest constant with $P(C|x)\ge 1-\alpha$.

## Properties
### Worked derivation: Normal HPD set
For $x\sim N(\theta,\sigma^2)$, prior $\theta\sim N(\mu,\tau^2)$, the posterior is $N(\mu(x), w^2)$ (see [[Posterior distribution]]; here $\mu(x)$, $w^2$ denote the posterior mean/variance in the notation of this chapter). Since the Normal density is unimodal and symmetric, the region of highest density around $\mu(x)$ is automatically an interval, so the HPD set coincides with the ordinary [[Credible Interval]]:
$$
C = \left(\mu(x) - z_{\alpha/2}\,w,\ \ \mu(x) + z_{\alpha/2}\,w\right)
$$

### When HPD sets are not simple intervals
For skewed or multimodal posteriors, the HPD set need not be a single interval, and computing it may require numerical methods — but it remains straightforward to compute even for models with no closed-form sufficient statistics (e.g. a Cauchy location-parameter model with a flat, non-informative prior): the posterior density can be evaluated pointwise and thresholded, even when no equivalent closed-form classical confidence procedure is available.

## See also
[[Credible Interval]], [[Credible interval vs Confidence interval]], [[Posterior distribution]]
