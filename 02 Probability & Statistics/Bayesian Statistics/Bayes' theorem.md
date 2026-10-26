---
title: "Bayes' theorem"
domain: "Probability & Statistics"
course: "Bayesian Statistics"
unit: "Chapter 3 - Bayesian Inference"
level: MSc
status: drafted
confidence: 0
tags: [bayesian-statistics, foundations]
---
## Definition
For disjoint events $A_1, \dots, A_m$ whose union has probability one, with prior probabilities $P(A_i)$ known and $P(B|A_i)$ known for each $A_i$, Bayes' theorem states
$$
P(A_i|B) = \frac{P(B|A_i)P(A_i)}{\sum_{j=1}^m P(B|A_j)P(A_j)}
$$
Replacing $A_i$ by a parameter value $\theta_i$ and $B$ by observed data $x$ gives the formula for the [[Posterior distribution]] in terms of the [[Likelihood function]] and the [[Prior distribution]]: $\theta$ is treated as a random variable with marginal (prior) probability $P(\theta)$, and Bayes' theorem gives the conditional (posterior) distribution of $\theta$ given $x$.

## Properties
### Law of Total Probability gives the normalizing constant
The denominator is just the Law of Total Probability applied to the partition $\{A_j\}$:
$$
P(B) = \sum_{j=1}^m P(B|A_j)P(A_j)
$$
This term does not depend on $A_i$ (or $\theta$), so it acts purely as a normalizing constant — this is why the [[Posterior distribution]] can often be written as $\pi(\theta|x) \propto f(x|\theta)\pi(\theta)$ without evaluating it explicitly.

### Continuous form
For a continuous parameter $\theta$ with prior density $\pi(\theta)$ and likelihood $f(x|\theta)$,
$$
\pi(\theta|x) = \frac{f(x|\theta)\pi(\theta)}{\int f(x|\theta)\pi(\theta)\,d\theta}
$$

## Examples
**Diagnostic test.** A blood test for a disease has $P(X=1|\theta=1)=0.8$, $P(X=1|\theta=0)=0.3$, with prior $P(\theta=1)=0.05$. By total probability, $P(X=1) = 0.8(0.05) + 0.3(0.95) = 0.325$. Applying Bayes' theorem,
$$
P(\theta=1|X=1) = \frac{0.8 \times 0.05}{0.325} = 0.123
$$
Even with a positive test, the posterior probability of disease is only 12.3% — the low prior prevalence dominates the moderately informative test. This illustrates why the prior cannot be ignored in Bayesian inference.

## See also
[[Prior distribution]], [[Posterior distribution]], [[Likelihood function]], [[Conjugate prior]]
