---
title: "Bayesian Credibility Theory"
domain: "Probability & Statistics"
course: "Bayesian Statistics"
unit: "Chapter 6 - Empirical Bayes and Bayesian Credibility"
level: MSc
status: drafted
confidence: 0
tags: [bayesian-statistics, credibility-theory, actuarial]
---
## Definition
Credibility theory combines a risk's own (limited) experience with wider population experience to forecast an uncertain future quantity (e.g. an insurance premium), via a weighted average
$$
\text{estimate} = \delta \times (\text{own experience}) + (1-\delta) \times (\text{population/prior experience})
$$
where $\delta\in[0,1]$ is the **credibility factor**. Under the Bayesian framework, this weighted-average structure emerges *exactly* from the [[Posterior distribution|posterior mean]]:
$$
E^{\pi(\theta|x)}[\theta|x] = \delta \cdot \bar x + (1-\delta)\cdot E^\pi[\theta]
$$
i.e. the posterior mean of $\theta$ is a weighted average of the sample mean $\bar x$ (own experience) and the prior mean $E^\pi[\theta]$ (population experience, from the prior's hyperparameters) — $\delta$ falls out automatically once the likelihood and prior are specified.

## Properties
### Worked derivation: Poisson/Gamma model (claim frequency)
Claims $x_1,\dots,x_n \sim \text{Poisson}(\lambda)$ i.i.d., prior $\lambda\sim\text{Gamma}(\alpha,\beta)$. The posterior is
$$
\pi(\lambda|x) \propto \lambda^{\sum_i x_i}e^{-n\lambda}\cdot\lambda^{\alpha-1}e^{-\beta\lambda} = \lambda^{\alpha+\sum_i x_i - 1}e^{-(n+\beta)\lambda}
$$
i.e. $\text{Gamma}(\alpha+\sum_i x_i,\ \beta+n)$ (matching the general [[Conjugate prior]] update). Its mean is
$$
E^{\pi(\lambda|x)}[\lambda] = \frac{\alpha+\sum_i x_i}{\beta+n} = \frac{n}{\beta+n}\cdot\frac{\sum_i x_i}{n} + \left(1-\frac{n}{\beta+n}\right)\cdot\frac{\alpha}{\beta}
= \delta\cdot\bar x + (1-\delta)\cdot\frac{\alpha}{\beta}
$$
with credibility factor $\delta = \dfrac{n}{\beta+n}$ (note $\alpha/\beta = E^\pi[\lambda]$, the Gamma prior mean). As $n\to\infty$, $\delta\to1$ and the estimate is dominated by the data, as expected.

### Worked derivation: Normal/Normal model (pure premium)
$X\sim N(\mu,\sigma_1^2)$ (aggregate claims), prior $\mu\sim N(\theta,\sigma_2^2)$, both variances known, $n$ past observations $x_1,\dots,x_n$ with sample mean $\bar x$. Multiplying likelihood and prior and completing the square in $\mu$ gives $\mu|x \sim N(\mu_1,\sigma_1'^2)$ with
$$
\mu_1 = \frac{n\bar x\,\sigma_2^2 + \sigma_1^2\theta}{n\sigma_2^2+\sigma_1^2} = \frac{n\sigma_2^2}{n\sigma_2^2+\sigma_1^2}\bar x + \frac{\sigma_1^2}{n\sigma_2^2+\sigma_1^2}\theta = \delta\cdot\bar x + (1-\delta)\cdot\theta
$$
with credibility factor $\delta = \dfrac{n\sigma_2^2}{n\sigma_2^2+\sigma_1^2}$ (writing $\tau^2=\sigma_2^2$ for the prior variance in the notation of [[Posterior distribution]]). The larger $n$ or the smaller $\sigma_1^2$ (less sample noise), the closer $\delta$ is to 1, i.e. the more the estimate trusts the risk's own data over the population prior.

### General pattern
In both models, $\delta$ has the form $\dfrac{(\text{amount of own data})}{(\text{amount of own data}) + (\text{prior/population "pseudo-data" weight})}$ — the credibility factor is exactly the same object as the precision-weighting seen in [[Posterior distribution]]'s Normal-Normal example, specialized to a premium-rating context.

## Examples
A bus fleet's own claims average £1,600/year (own experience); the wider UK fleet average is £2,500/year (population experience). The credibility premium is $\delta\times1600+(1-\delta)\times2500$, with $\delta$ determined by how much the fleet's own data is trusted relative to the (more numerous, but less directly relevant) population data — formalized by the Poisson/Gamma or Normal/Normal derivations above.

## See also
[[Empirical Bayes]], [[Conjugate prior]], [[Posterior distribution]], [[Hierarchical model]]
