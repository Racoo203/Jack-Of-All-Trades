---
title: "Uniform Distribution of Deaths (UDD)"
domain: Probability & Statistics
course: Survival Analysis
unit: "Chapter 2 - Lifetime after age x and lifetable"
level: MSc
status: drafted
confidence: 0
tags: [survival-analysis, udd, fractional-age-assumption]
---
## Definition
The **uniform distribution of deaths (UDD)** assumption states that deaths are distributed uniformly (linearly) across each year of age $[x, x+1)$ — in general not true, but a standard fractional-age assumption used throughout survival and mortality modelling (see [[Life Table]], [[Binomial Model for Mortality]], [[Exposed to Risk]]). Under UDD, for $0\leq t\leq 1$,
$$
l_{x+t} = (1-t)l_x + tl_{x+1}
$$
by linear interpolation between $l_x$ and $l_{x+1}$.

## Properties
### $_tq_x = t\,q_x$ under UDD
**Proposition.** If deaths are uniformly distributed across the year of age, ${}_tq_x = t\,q_x$.

**Proof.** Using linear interpolation:
$$
{}_tq_x = 1-\frac{l_{x+t}}{l_x} = 1-\frac{(1-t)l_x+tl_{x+1}}{l_x} = \frac{tl_x - tl_{x+1}}{l_x} = t(1-p_x) = t\,q_x
$$

### Consequence for fractional exposure
UDD is the assumption typically paired with the **binomial model** of mortality (see [[Binomial Model for Mortality]]), as opposed to the constant-force assumption paired with the Poisson/two-state models.

## See also
[[Life Table]], [[Force of Mortality and Actuarial Notation]], [[Binomial Model for Mortality]], [[Exposed to Risk]]
