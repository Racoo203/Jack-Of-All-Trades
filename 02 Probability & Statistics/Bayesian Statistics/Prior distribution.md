---
title: "Prior distribution"
domain: "Probability & Statistics"
course: "Bayesian Statistics"
unit: "Chapter 3 - Bayesian Inference"
level: MSc
status: drafted
confidence: 0
tags: [bayesian-statistics, foundations]
---
## Definition
In the Bayesian framework the parameter $\theta$ is treated as random. The prior distribution $\pi(\theta)$ specifies the beliefs about $\theta$ *before* any data is observed. Combined with the [[Likelihood function]] via [[Bayes' theorem]], it produces the [[Posterior distribution]]:
$$
\pi(\theta|x) \propto f(x|\theta)\,\pi(\theta), \qquad \text{posterior} \propto \text{likelihood} \times \text{prior}
$$

## Properties
### Proper vs. improper priors
A prior is **proper** if $\int_\Theta \pi(\theta)\,d\theta < \infty$ (it can be normalized to a genuine probability distribution). A prior is **improper** if this integral is infinite (e.g. a "flat" prior $\pi(\theta) \propto 1$ over an unbounded $\Theta$). Improper priors are still useful as long as the resulting posterior is proper. Reasons to use an improper prior:
1. Genuinely non-informative priors are often improper (informative priors necessarily favour some values of $\theta$).
2. Bayesian analyses with specific improper priors often reproduce classical (frequentist) estimators.
3. Improper priors arise as natural limits of proper priors and can be a good approximation.

### Choice of prior family
- **Subjective priors** encode an expert's genuine belief about $\theta$.
- **[[Conjugate prior|Conjugate priors]]** are chosen for computational convenience: the posterior stays in the same distributional family as the prior.
- **Non-informative priors** (e.g. [[Jeffrey's prior]]) aim to "favour no particular value" of $\theta$, for an ostensibly "objective" analysis.

## Examples
Uniform prior $\pi(p) = 1$ for $p \in [0,1]$ on the success probability of a Bernoulli/Binomial model — see [[Conjugate prior]] for how this becomes a Beta posterior.

## See also
[[Posterior distribution]], [[Conjugate prior]], [[Jeffrey's prior]], [[Bayes' theorem]], [[Likelihood function]]
