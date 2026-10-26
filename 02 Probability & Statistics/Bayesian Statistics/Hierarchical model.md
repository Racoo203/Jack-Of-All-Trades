---
title: "Hierarchical model"
domain: "Probability & Statistics"
course: "Bayesian Statistics"
unit: "Chapter 6 - Empirical Bayes and Bayesian Credibility"
level: MSc
status: seeding
confidence: 0
tags: [bayesian-statistics, credibility-theory]
---
<!-- UNVERIFIED: check against course slides — Chapter 6's lecture material covers Empirical Bayes and Bayesian credibility but does not present multi-level hierarchical models explicitly; this note is drafted from standard theory to contrast with the course's Empirical Bayes treatment, and should be verified against any later course material (e.g. MA322 Bayesian Computational Statistics) before treating it as reviewed. -->

## Definition
A hierarchical (multi-level) Bayesian model places a prior not just on the parameter $\theta$, but on the hyperparameters $\tau$ of $\theta$'s prior as well:
$$
x \mid \theta \sim f(x|\theta), \qquad \theta \mid \tau \sim \pi(\theta|\tau), \qquad \tau \sim \pi(\tau)
$$
Inference proceeds by treating the *joint* posterior $\pi(\theta,\tau|x) \propto f(x|\theta)\pi(\theta|\tau)\pi(\tau)$ as the object of interest, typically reporting the marginal posterior of $\theta$, $\pi(\theta|x) = \int \pi(\theta,\tau|x)\,d\tau$.

## Properties
### Contrast with Empirical Bayes
[[Empirical Bayes]] avoids specifying $\pi(\tau)$ by instead plugging in a point estimate $\hat\tau$ (e.g. the MLE from the marginal/predictive distribution of $x$) and treating $\pi(\theta|x,\hat\tau)$ as the posterior. A hierarchical model is "more Bayesian": it propagates the *uncertainty* in $\tau$ through to the posterior for $\theta$, rather than conditioning on a single estimated value. Empirical Bayes can be viewed as an approximation to a hierarchical model that ignores the extra uncertainty coming from estimating $\tau$.

### Motivation
Hierarchical models are natural whenever data arise in groups (e.g. multiple related risks/subjects, each with its own $\theta_j$, but the $\theta_j$ themselves are believed to be drawn from a common population distribution) — this is the same structure underlying [[Bayesian Credibility Theory]], where a risk's own experience and the wider population's experience are combined; a hierarchical model formalizes this by putting a prior on the population-level hyperparameters too.

## See also
[[Empirical Bayes]], [[Prior distribution]], [[Bayesian Credibility Theory]]
