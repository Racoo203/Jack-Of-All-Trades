---
title: "Data Scaling and Standardization"
domain: "Machine Learning & AI"
course: "Multivariate Data Analysis"
unit: "Módulo I, Unit 2 - Normalidad"
level: BSc
status: drafted
confidence: 0
tags: [multivariate-data-analysis, data-preprocessing]
---
## Definition
**Scaling** modifies the units of a variable (shift and/or rescale) so that variables measured on very different scales become comparable — without touching the shape of the distribution. This is the key distinction from [[Data Transformations for Normality (Box-Cox and Yeo-Johnson)|transformation]]: a transformation can change a variable's distribution entirely (e.g. skewed $\to$ approximately normal); a scaling method always preserves it.

## Properties
### The four scaling methods
- **Min–max scaling.** Maps data to $[0,1]$: $T_{\min-\max}=\dfrac{x-\min(X)}{\max(X)-\min(X)}$. Very sensitive to outliers, since a single extreme value stretches the whole range.
- **Normalized scaling.** Divides by the vector norm $\lVert X\rVert=\sqrt{x_1^2+\cdots+x_n^2}$: $T_{\text{normalizada}}=\dfrac{x}{\lVert X\rVert}$. Guarantees equal "variation" across variables in a vector-length sense, but results in a very small, hard-to-interpret scale, so it is used sparingly.
- **Standard scaling (z-score).** Centers on the mean and divides by the standard deviation: $T_{\text{estándar}}=\dfrac{x-\bar x}{s}$. Produces mean $0$, standard deviation $1$; other than the shift/rescale, the distribution is exactly the original one. This is the recommended default when the goal is comparing distance from the mean across variables.
- **Robust scaling.** Centers on the interquartile range (rather than the mean) and divides by the standard deviation: $T_{\text{robusto}}=\dfrac{x-IQ}{s}$. Sets the median (rather than the mean) near zero and is comparatively insensitive to outliers.

### Practical guidance
- Min–max is heavily affected by outliers; robust scaling is largely unaffected by them.
- Normalized scaling produces an inconveniently small scale and is used less often in practice.
- Standard scaling is the only one that simultaneously guarantees mean $0$ and standard deviation $1$, giving the transformed values a direct interpretation (number of standard deviations from the mean).
- **All variables must be scaled with the same method** so that they end up on a comparable range — mixing scaling methods across variables defeats the purpose.
- The right method is context-dependent and is typically chosen by experimentation with the specific dataset.

## Examples
In R, a reusable function plus `lapply` standardizes an entire data frame at once:
```r
min_max_norm <- function(x){(x-min(x))/(max(x)-min(x))}
M1 <- as.data.frame(lapply(M, min_max_norm))   # M is the data frame

z_norm <- function(x){(x-mean(x))/sd(x)}
M1 <- as.data.frame(lapply(M, z_norm))
```
Standardization (z-score scaling) is the default preprocessing step recommended before [[Principal Component Analysis|standardized PCA]] (using the correlation matrix $R$ instead of the covariance matrix $S$) whenever the original variables are on very different scales — see [[Principal Component Analysis]]'s "Standardized principal components" property.

## See also
[[Data Transformations for Normality (Box-Cox and Yeo-Johnson)]], [[Principal Component Analysis]], [[Hierarchical Cluster Analysis]]
