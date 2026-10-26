---
title: "Validation of Multivariate Normality"
domain: "Machine Learning & AI"
course: "Multivariate Data Analysis"
unit: "Módulo I, Unit 2 - Normalidad"
level: BSc
status: drafted
confidence: 0
tags: [multivariate-data-analysis, normality, hypothesis-testing]
---
## Definition
Checking whether a sample plausibly comes from a [[The Multivariate Normal Distribution|multivariate normal]] $N_p(\boldsymbol\mu,\Sigma)$ combines dedicated multivariate tests with checks derived directly from the multivariate normal's defining properties: if $X\sim N_p(\boldsymbol\mu,\Sigma)$, then (i) every marginal distribution is univariate normal, (ii) every linear combination is univariate normal, and (iii) the constant-density contours are elliptical with a known chi-square relationship — so violating any of these is evidence against multivariate normality.

## Properties
### Univariate (marginal) validation
Since each component $X_j$ must itself be normal, apply [[Graphical and Statistical Tests for Normality|univariate normality checks]] — histograms/box-plots (looking for symmetry, unimodality), descriptive measures (symmetric $Q_1,Q_3$; mean $\approx$ median $\approx$ mid-range), and the QQ plot — to each variable separately. For $n>20$, plotting the ordered statistics $X_{(i)}$ against $q_i=\Phi^{-1}\left(\tfrac{i-0.5}{n}\right)$ should give an approximately straight line if $X_j\sim N(\mu_j,\sigma_{jj})$.

### Linear-combination validation
Any linear combination of $X$ is a univariate random variable and can be checked with univariate techniques; the combinations formed from the eigenvectors of $\Sigma$, $\hat{\mathbf{e}}_i'\mathbf{X}_i$ (i.e. the [[Principal Component Analysis|principal component]] scores), are the natural ones to check because they are the directions along which the data varies most and least.

### Bivariate contour validation
If $X\sim N_p(\boldsymbol\mu,\Sigma)$, $(\mathbf{X}-\boldsymbol\mu)'\Sigma^{-1}(\mathbf{X}-\boldsymbol\mu)\sim\chi^2_p$, so $P\big[(\mathbf{X}-\boldsymbol\mu)'\Sigma^{-1}(\mathbf{X}-\boldsymbol\mu)\le\chi^2_p(\alpha)\big]=1-\alpha$. Substituting sample estimates, for large $n$ one expects approximately $(1-\alpha)\times100\%$ of observations to satisfy $(\mathbf{X}-\bar{\mathbf{x}})'S^{-1}(\mathbf{X}-\bar{\mathbf{x}})\le\chi^2_{(p,\alpha)}$; computing the actual proportion inside the ellipse for several $\alpha$ and comparing to the nominal $1-\alpha$ is a direct validation check (see [[Constant Density Contours]]).

### Multivariate chi-square QQ plot
A direct multivariate analogue of the univariate QQ plot: for each observation $i$, compute the squared [[Statistical Distance and Mahalanobis Distance|Mahalanobis distance]] to the sample mean,
$$
d_i^2 = (\mathbf{X}_i-\bar{\mathbf{x}})'S^{-1}(\mathbf{X}_i-\bar{\mathbf{x}}) \approx \chi^2_{(p)}
$$
and plot the ordered $d_{(i)}^2$ against the expected quantiles of $\chi^2_p$. If $\mathbf{X}\sim N_p(\boldsymbol\mu,\Sigma)$, the points should fall approximately on a straight line through the origin with slope $1$.

### Detecting extreme observations
Points that fall well off the chi-square QQ line, or whose $d_i^2$ is unusually large relative to $\chi^2_p(\alpha)$ for small $\alpha$, are candidate multivariate outliers — worth investigating before proceeding with normal-theory techniques such as [[Principal Component Analysis]] or [[Factor Analysis - The Orthogonal Factor Model|Factor Analysis]].

### Formal multivariate normality tests
- **Mardia's test.** Based on multivariate generalizations of skewness and kurtosis (extending [[Skewness and Kurtosis]] to $p$ dimensions).
- **Generalized Shapiro–Wilk.** Compares an observed $Z$-statistic against its empirically-derived distribution across all variables jointly.
- **Royston's test.** Combines a multivariate Shapiro–Wilk-type statistic for platykurtic data (kurtosis below $0$ or $3$) with a Shapiro–Francia-type statistic for leptokurtic data.
- **Henze–Zirkler test.** Based on the distance between the empirical characteristic function and the theoretical one under multivariate normality.

R: `library(MVN); mvn()` runs several of these together along with the graphical checks above.

## Examples
No single numeric example runs the full battery in the source slides; the individual pieces are illustrated separately in [[Graphical and Statistical Tests for Normality]] (univariate QQ plot and tests) and [[Constant Density Contours]] (the chi-square-ellipse coverage check). In practice, the course's own workflow (as in the `G301_Análisis discriminante.rmd` template, which calls `mvn()` before fitting an LDA model — see [[Linear Discriminant Analysis]]) runs `library(MVN); mvn()` on each class/group before proceeding.

## See also
[[The Multivariate Normal Distribution]], [[Constant Density Contours]], [[Graphical and Statistical Tests for Normality]], [[Skewness and Kurtosis]], [[Linear Discriminant Analysis]]
