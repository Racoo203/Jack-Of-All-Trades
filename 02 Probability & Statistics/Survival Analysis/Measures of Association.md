---
title: "Measures of Association"
domain: Probability & Statistics
course: Survival Analysis
unit: "Chapter 10 - Copulas & Measures of Association"
level: MSc
status: drafted
confidence: 0
tags: [survival-analysis, kendalls-tau, spearmans-rho, dependence]
---
## Definition
There are three principal classes of measures of dependence between two random variables $X,Y$:
1. **Pearson's correlation**: $\rho(X,Y) = \dfrac{\text{Cov}(X,Y)}{\sqrt{\text{Var}(X)\text{Var}(Y)}}$ — only measures *linear* association ($Y=aX+b$); fails to capture nonlinear dependence (e.g. if $X\sim U[-1,1]$ and $Y=X^2$, $\text{Cov}(X,Y)=0$ despite perfect functional dependence). It can be shown that if $C$ is the [[Copula|copula]] of $X,Y$: $\rho(X,Y) = 12\int_0^1\int_0^1 (u-\tfrac12)(v-\tfrac12)c(u,v)\,du\,dv$.
2. **Rank measures** (Kendall's $\tau$, Spearman's $\rho$): depend only on the ranks of $x_i,y_i$, not their values directly; invariant to monotonic transformations of the variables; and depend only on the copula $C(u,v)$ of $X,Y$, not on the marginals.

## Properties
### Kendall's $\tau$
For $(X_i,Y_i),(X_j,Y_j)$ i.i.d. copies, Kendall's $\tau$ measures the proportion of **concordant** pairs:
$$
\tau_{X,Y} = \mathbb{E}\left[\text{sign}\big((X_i-X_j)(Y_i-Y_j)\big)\right]
$$
equivalently $\tau_{X,Y}=\int \text{sign}((x_1-x_2)(y_1-y_2))f(x_1,y_1)f(x_2,y_2)\,dx_1dx_2dy_1dy_2$ for joint density $f$.

**Property.** In terms of the copula $C$ and density $c$:
$$
\tau_{X,Y} = 4\int_0^1\int_0^1 C(u,v)\,c(u,v)\,du\,dv - 1
$$

**Example.** For $C(u,v)=uv$ (density $c=1$, the independence copula):
$$
\tau_{X,Y} = 4\int_0^1\int_0^1 uv\,du\,dv - 1 = 4\left[\frac{u^2}{2}\right]_0^1\left[\frac{v^2}{2}\right]_0^1 - 1 = 4\times\frac14-1 = 0
$$
consistent with independence.

### Spearman's $\rho$
Let $R_X=F_X(X)$, $R_Y=F_Y(Y)$ (the probability-integral-transformed, rank-like variables). **Spearman's $\rho$** is the (Pearson) correlation between $R_X$ and $R_Y$:
$$
\rho_{X,Y} = 12\int_0^1\int_0^1 C(u,v)\,du\,dv - 3
$$

**Example.** For $C(u,v)=\min(u,v)$ (the [[Copula|minimum/comonotonicity copula]]):
$$
\rho_{X,Y} = 12\int_0^1\int_0^1 \min(u,v)\,du\,dv - 3 = 12\int_0^1\left[\int_0^v u\,du + \int_v^1 v\,du\right]dv - 3
$$
$$
= 12\int_0^1\left(\frac{v^2}{2}+v(1-v)\right)dv-3 = 12\int_0^1\left(v-\frac{v^2}{2}\right)dv-3 = 12\left[\frac{v^2}{2}-\frac{v^3}{6}\right]_0^1-3 = 12\times\frac13-3 = 1
$$
consistent with perfect positive dependence.

### Properties of $\tau$ and $\rho$
1. $-1\leq\tau_{X,Y}\leq1$ and $-1\leq\rho_{X,Y}\leq1$.
2. If $X,Y$ are independent, $\tau_{X,Y}=0$ and $\rho_{X,Y}=0$ (the converse need not hold in general).
3. Values close to $\pm1$ indicate strong association.
4. Unlike Pearson's correlation, both $\tau_{X,Y}$ and $\rho_{X,Y}$ can capture nonlinear (monotonic) association, not just linear.

## Examples
Epidemiological data on lifetime and age at heart-transplant: $\tau_{X,Y}\approx-0.306$, $\rho_{X,Y}\approx-0.626$ — a moderate negative association (longer lifetime associated with younger age at transplant).

## See also
[[Copula]], [[Archimedean Copula]], [[Tail Dependence]]
