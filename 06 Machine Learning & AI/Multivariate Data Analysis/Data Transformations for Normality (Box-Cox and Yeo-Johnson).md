---
title: "Data Transformations for Normality (Box-Cox and Yeo-Johnson)"
domain: "Machine Learning & AI"
course: "Multivariate Data Analysis"
unit: "Módulo I, Unit 2 - Normalidad"
level: BSc
status: drafted
confidence: 0
tags: [multivariate-data-analysis, normality, data-preprocessing]
---
## Definition
A **transformation** modifies the *distribution* of a variable — typically to make it closer to Normal, since normality is an assumption behind [[One-Way ANOVA|ANOVA]], [[Multiple Linear Regression|regression]], and much of the rest of the course — and the transformed variable can behave very differently from the original. (Contrast with [[Data Scaling and Standardization|scaling]], which only shifts/rescales a variable without touching its distributional shape.)

**Box–Cox transformation.** A one-parameter family indexed by $\lambda$, defined only for $x>0$:
$$
f(x,\lambda) = \begin{cases}\dfrac{x^\lambda-1}{\lambda} & \lambda\neq 0\\[4pt] \log(x) & \lambda=0\end{cases}
$$
$\lambda$ is chosen by maximizing the likelihood of the transformed data under normality (`boxcox()` in R's `MASS` package). If $x$ can be $\le 0$, a translation ($x+a$) is applied first.

**Yeo–Johnson transformation.** Extends Box–Cox to variables that can take any real value (no positivity restriction):
$$
f(x,\lambda) = \begin{cases} \dfrac{(x+1)^\lambda-1}{\lambda} & x\ge 0,\ \lambda\neq 0\\ \log(x+1) & x\ge 0,\ \lambda=0\\ -\dfrac{(-x+1)^{2-\lambda}-1}{2-\lambda} & x<0,\ \lambda\neq 2\\ -\log(-x+1) & x<0,\ \lambda=2\end{cases}
$$
also fit by maximum likelihood (R: `library(VGAM); yeo.johnson(x, lambda = l)`), with $\lambda\in[-2,2]$ typically searched by grid (choosing the $\lambda$ that maximizes the $p$-value of a normality test on the transformed data, e.g. Anderson–Darling).

**Power transformations, generally.** A unifying family includes logarithmic ($y=\log_b(x+a)$), radical ($y=\sqrt[b]{x+a}$), inverse ($y=a/x^b$), power ($y=(x+a)^b$), and the Box–Cox/Yeo–Johnson forms above as special/limiting cases. R's `car::powerTransform(x, family="yjPower")` searches this family directly by maximum likelihood.

## Properties
### Why Box–Cox needs positivity and a translation
Because $\log(x)$ and $x^\lambda$ are undefined or ill-behaved for $x\le 0$, any variable with zero or negative values needs a shift $x+a$ (commonly $a=1$) before Box–Cox can be applied — or, if the zeros are conceptually distinct from the rest of the distribution (e.g. representing a different underlying process), they can instead be removed from the sample entirely before transforming.

### Choosing among transformations empirically
Once several transformed variables are computed, comparing their goodness-of-fit to normality (via [[Graphical and Statistical Tests for Normality|the formal tests]]) and their skewness/kurtosis (see [[Skewness and Kurtosis]]) selects the best one for the specific dataset — there is no transformation that is uniformly best; the choice is data-dependent and made by comparison.

## Examples
The worked example transforms the `Calories` variable from a McDonald's nutrition dataset, which contains some exact-zero values (water, sugar-free soft drinks).
1. **With the zeros included**, after translating ($x+1$), Box–Cox finds $\lambda=0.5858586$ ($\approx0.59$), giving $\text{cal}_2 = \frac{(x+1)^{0.59}-1}{0.59}$. But the transformed variable still fails Anderson–Darling ($p=4.17\times10^{-7}$), because the zeros (structurally different from the rest) distort the fit.
2. **Removing the zero-calorie items** and re-running Box–Cox on the remainder gives $\lambda=0.34343434$, $\text{cal}_2=\frac{x^{0.343434}-1}{0.343434}$.
3. **Yeo–Johnson** on the zero-free data (searching $\lambda$ to maximize the Anderson–Darling $p$-value) gives $\lambda=0.373$, $\text{cal}_3=\frac{(x+1)^{0.373}-1}{0.373}$.
4. **`powerTransform` with the `yjPower` family** gives $\lambda=0.348$, $\text{cal}_4=\frac{(x+1)^{0.348}-1}{0.348}$.

Comparing all four models (the original Calories variable, and $\text{cal}_2,\text{cal}_3,\text{cal}_4$) across five normality tests, every transformed version dramatically improves the $p$-value relative to the raw variable — e.g. Anderson–Darling goes from statistic $3.776$ ($p<0.001$) on the raw variable to statistic $\approx 0.28$–$0.29$ ($p\approx0.61$–$0.65$) on the transformed versions — with the exact-value Yeo–Johnson transformation ($\lambda_3=0.373$) edging out the others on most tests in this particular dataset.

## See also
[[Skewness and Kurtosis]], [[Graphical and Statistical Tests for Normality]], [[Data Scaling and Standardization]], [[The Multivariate Normal Distribution]]
