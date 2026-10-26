---
title: "Empirical Bayes"
domain: "Probability & Statistics"
course: "Bayesian Statistics"
unit: "Chapter 6 - Empirical Bayes and Bayesian Credibility"
level: MSc
status: drafted
confidence: 0
tags: [bayesian-statistics, credibility-theory]
---
## Definition
A full Bayesian analysis requires specifying a [[Prior distribution]] $\pi(\theta)$ from pre-data information alone. **Empirical Bayes** instead chooses a convenient (typically [[Conjugate prior|conjugate]]) prior family $\pi(\theta|\tau)$ with hyperparameters $\tau$, and estimates $\tau$ from the data itself — using a frequentist method (e.g. [[Maximum Likelihood Estimate|MLE]]) applied to the prior predictive distribution
$$
p(x|\tau) = \int f(x|\theta)\,\pi(\theta|\tau)\,d\theta
$$
The estimate $\hat\tau$ is then plugged back into Bayes' theorem, giving a **"pseudo" posterior** $\pi(\theta|x,\hat\tau)$. This differs from a fully Bayesian (or [[Hierarchical model|hierarchical Bayes]]) treatment, which would instead place a further prior on $\tau$ and integrate it out rather than plugging in a point estimate.

## Properties
### Worked derivation: Poisson/Exponential
Let $x_i\sim\text{Poisson}(\lambda)$ i.i.d., with prior $\lambda\sim\text{Exp}(\beta)$. The prior predictive distribution is
$$
p(x_i|\beta) = \int_0^\infty \frac{e^{-\lambda}\lambda^{x_i}}{x_i!}\,\beta e^{-\beta\lambda}\,d\lambda = \left(\frac{1}{1+\beta}\right)\left(\frac{\beta}{1+\beta}\right)^{x_i}
$$
i.e. given $\beta$, the $x_i$ are i.i.d. $\text{Geometric}(p)$ with $p=\beta/(1+\beta)$. The (frequentist) MLE of $\beta$ based on $x_1,\dots,x_n$ is $\hat\beta = 1/\bar x$ — an ordinary point estimate computed from the marginal (predictive) distribution, then substituted into the conjugate Gamma-Poisson posterior machinery (see [[Conjugate prior]]) as if it were known in advance.

## See also
[[Prior distribution]], [[Conjugate prior]], [[Hierarchical model]], [[Bayesian Credibility Theory]], [[Maximum Likelihood Estimate]]
