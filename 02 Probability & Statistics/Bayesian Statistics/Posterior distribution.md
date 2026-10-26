---
title: "Posterior distribution"
domain: "Probability & Statistics"
course: "Bayesian Statistics"
unit: "Chapter 3 - Bayesian Inference"
level: MSc
status: drafted
confidence: 0
tags: [bayesian-statistics, foundations]
---
## Definition
The posterior distribution combines the [[Prior distribution]] $\pi(\theta)$ with the information in the data (the [[Likelihood function]] $f(x|\theta)$) into a single distribution describing the updated beliefs about $\theta$ after observing $x$:
$$
\pi(\theta|x) = \frac{f(x|\theta)\pi(\theta)}{\int f(x|\theta)\pi(\theta)\,d\theta} \propto f(x|\theta)\pi(\theta)
$$
The denominator (normalizing constant) does not involve $\theta$ and can often be ignored when only the shape of $\pi(\theta|x)$ is needed.

Posterior summaries: the **posterior mean** $E[\theta|x] = \int_{\theta \in \Theta} \theta\,\pi(\theta|x)\,d\theta$, plus the posterior mode, posterior median, posterior variance and posterior percentiles — all unavailable in classical (point-estimate-only) statistics.

## Properties
### Posterior for a Normal mean with a Normal prior (known variance)
Let $x \sim N(\theta, \sigma^2)$ with $\sigma^2$ known, and prior $\theta \sim N(\mu, \tau^2)$. Then
$$
\pi(\theta|x) \propto \exp\left(-\frac{(\theta-\mu)^2}{2\tau^2}\right)\exp\left(-\frac{(x-\theta)^2}{2\sigma^2}\right)
$$
Expanding and collecting terms in $\theta$ (dropping anything not containing $\theta$):
$$
\pi(\theta|x) \propto \exp\left[-\frac{1}{2}\left(\theta^2\left(\frac{1}{\tau^2}+\frac{1}{\sigma^2}\right) - 2\theta\left(\frac{\mu}{\tau^2}+\frac{x}{\sigma^2}\right)\right)\right]
$$
Writing $\frac{1}{\sigma_1^2} = \frac{1}{\tau^2}+\frac{1}{\sigma^2}$ and $\mu_1 = \sigma_1^2\left(\frac{\mu}{\tau^2}+\frac{x}{\sigma^2}\right)$, this is $\propto \exp\left(-\frac{(\theta-\mu_1)^2}{2\sigma_1^2}\right)$, i.e.
$$
\theta | x \sim N(\mu_1, \sigma_1^2)
$$
The posterior mean is a **precision-weighted average** of the prior mean and the data:
$$
\mu_1 = \mu\frac{\sigma^2}{\tau^2+\sigma^2} + x\frac{\tau^2}{\tau^2+\sigma^2}
$$
If the prior variance $\tau^2$ is large relative to $\sigma^2$ (a vague prior), $\mu_1 \to x$: the data dominate. As $\tau^2 \to \infty$, $\sigma_1^2 \to \sigma^2$ and $\mu_1 \to x$, recovering the classical [[Maximum Likelihood Estimate]].

## Examples
Bernoulli/Binomial data with a uniform prior gives a Beta posterior — see [[Conjugate prior]] for the full derivation.

## See also
[[Prior distribution]], [[Likelihood function]], [[Bayes estimate]], [[Credible Interval]], [[Conjugate prior]], [[Posterior predictive distribution]]
