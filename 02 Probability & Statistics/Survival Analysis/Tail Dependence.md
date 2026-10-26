---
title: "Tail Dependence"
domain: Probability & Statistics
course: Survival Analysis
unit: "Chapter 10 - Copulas & Measures of Association"
level: MSc
status: drafted
confidence: 0
tags: [survival-analysis, tail-dependence, copulas]
---
## Definition
[[Measures of Association|Correlation-type measures]] summarise association across the whole joint distribution, but insurers are often specifically interested in whether **large losses occur together** — the dependence structure in the extreme tails. **Tail dependence** describes how large (or small) values of $X$ are associated with large (or small) values of $Y$, and can be derived from the [[Copula|copula]] of $X,Y$.

**Lower-tail dependence coefficient:**
$$
\lambda_L = \lim_{u\to0^+} P\left(X\leq F_X^{-1}(u) \mid Y\leq F_Y^{-1}(u)\right)
$$
**Property.** In terms of the copula, $\lambda_L = \lim_{u\to0}\dfrac{C(u,u)}{u}$.

**Upper-tail dependence coefficient:**
$$
\lambda_U = \lim_{u\to1^-} P\left(X> F_X^{-1}(u) \mid Y> F_Y^{-1}(u)\right)
$$
**Property.** In terms of the copula, $\lambda_U = 2-\lim_{u\to1}\dfrac{1-C(u,u)}{1-u} = \lim_{u\to1}\dfrac{1-2u-C(u,u)}{1-u}$.

## Properties
### General properties
1. $0\leq\lambda_L\leq1$ and $0\leq\lambda_U\leq1$.
2. $\lambda_L=0$ indicates weak lower-tail dependence, $\lambda_L=1$ indicates strong lower-tail dependence (similarly for $\lambda_U$).

### Example: Gumbel copula — no lower-tail dependence
For the Gumbel copula $C_\theta(u,v)=\exp\left\{-\left[(-\ln u)^\theta+(-\ln v)^\theta\right]^{1/\theta}\right\}$: $C_\theta(u,u) = \exp\{-2^{1/\theta}(-\ln u)\} = u^{2^{1/\theta}}$. So
$$
\lambda_L = \lim_{u\to0}\frac{u^{2^{1/\theta}}}{u} = \lim_{u\to0} u^{2^{1/\theta}-1} = 0 \quad (\text{since } 2^{1/\theta}>1 \text{ for }\theta\geq1)
$$
No dependence in the lower tail.

### Example: minimum copula — full upper-tail dependence
For $M(u,v)=\min(u,v)$: $M(u,u)=u$, so $\lambda_U = 2-\lim_{u\to1}\dfrac{1-u}{1-u} = 2-1=1$: strong (complete) dependence in the upper tail — consistent with $M$ representing perfect positive dependence.

### Example: FGM copula — no tail dependence
For the Farlie–Gumbel–Morgenstern copula $C_\theta(u,v)=uv+\theta uv(1-u)(1-v)$: $C(u,u)=u^2[1+\theta(1-u)^2]$, so
$$
\lambda_L = \lim_{u\to0}\frac{u^2[1+\theta(1-u)^2]}{u} = \lim_{u\to0} u[1+\theta(1-u)^2] = 0
$$
The FGM copula has neither meaningful upper- nor lower-tail dependence — it can only model weak/moderate overall association.

### Example: Clayton copula (qualitative)
The Clayton copula concentrates observations near $(0,0)$ in the lower tail, suggesting lower-tail dependence, while observations are comparatively spread out near $(1,1)$, suggesting little to no upper-tail dependence — the reverse asymmetry to the Gumbel copula.

## See also
[[Copula]], [[Archimedean Copula]], [[Measures of Association]], [[Extreme Value Theory]]
