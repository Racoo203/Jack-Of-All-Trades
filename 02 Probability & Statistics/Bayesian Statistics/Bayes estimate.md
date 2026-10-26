---
title: "Bayes estimate"
domain: "Probability & Statistics"
course: "Bayesian Statistics"
unit: "Chapter 4 - Bayesian Decision Theory"
level: MSc
status: drafted
confidence: 0
tags: [bayesian-statistics, decision-theory]
---
## Definition
Given a prior $\pi$ and [[Loss function]] $L$, a **Bayes estimator** $\delta^\pi$ is any decision rule that minimizes the [[Bayes risk]] $r(\pi,\delta)$. By Proposition 4.1 (see [[Bayes risk]]), this is achieved, for every $x$, by choosing $\delta^\pi(x)$ to minimize the **posterior expected loss**:
$$
\rho(\pi,d\mid x) = \int_\Theta L(\theta,d)\,\pi(\theta\mid x)\,d\theta, \qquad \delta^\pi(x) = \arg\min_{d\in D}\ \rho(\pi,d\mid x)
$$
where $\pi(\theta\mid x)$ is the [[Posterior distribution]]. This turns Bayesian estimation into a simple pointwise optimization for each observed $x$, rather than the harder frequentist problem of finding a rule with good risk $R(\theta,\delta)$ *uniformly* across all $\theta$.

## Properties
### Standard loss functions and their Bayes estimates
(Full derivations in [[Loss function]].)
- **Squared error loss** $L(\theta,a)=(\theta-a)^2$: the Bayes estimate is the **posterior mean** $E[\theta|x]$.
- **Absolute error loss** $L(\theta,a)=|\theta-a|$: the Bayes estimate is the **posterior median**.
- **0-1 loss**: the Bayes estimate is the **posterior mode** (or, for a binary decision "$\theta\in\Theta_0$?", the rule $\delta^\pi(x)=1 \iff P[\theta\in\Theta_0|x]>1/2$).

These results explain why the posterior mean is the "default" Bayesian point estimate — it corresponds to the most commonly used (quadratic) loss function — but the choice of loss function is itself a modelling decision, just as the choice of prior is.

### Relationship to frequentist estimators
Bayes estimators need not only be justified from "genuine" prior belief: the Proposition in [[Bayes risk]] shows that Bayes estimators (even under improper/generalized priors) often have good frequentist risk properties, and several classical estimators (e.g. the [[Maximum Likelihood Estimate]] as $\tau^2\to\infty$ in a Normal-Normal model, see [[Posterior distribution]]) arise as limiting Bayes estimators under vague priors.

## See also
[[Posterior distribution]], [[Loss function]], [[Bayes risk]], [[Maximum Likelihood Estimate]], [[Point estimation]]
