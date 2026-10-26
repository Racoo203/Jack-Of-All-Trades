---
title: "Skewness and Kurtosis"
domain: "Machine Learning & AI"
course: "Multivariate Data Analysis"
unit: "Módulo I, Unit 2 - Normalidad"
level: BSc
status: drafted
confidence: 0
tags: [multivariate-data-analysis, normality, descriptive-statistics]
---
## Definition
For a random variable $X$ with mean $\mu$, the $k$-th **moment centered on the mean** is $E[(X-\mu)^k]$ (discrete: $\sum_x (x-\mu)^k P(x)$; continuous: $\int (x-\mu)^k f(x)\,dx$). The first centered moment is always $0$; the second is the variance $\operatorname{Var}(X)=E[(X-\mu)^2]$. The third and fourth centered moments, standardized, characterize the *shape* of a distribution beyond its center and spread:

**Skewness** (third moment, standardized):
$$
\alpha_3 = \frac{E[(X-\mu)^3]}{\sigma^3}
$$
$\alpha_3=0$ for a symmetric distribution; $\alpha_3<0$ indicates left (negative) skew — the mean is pulled left of the bulk of the data — and $\alpha_3>0$ indicates right (positive) skew.

**Kurtosis** (fourth moment, standardized):
$$
\alpha_4 = \frac{E[(X-\mu)^4]}{\sigma^4}
$$
For the normal distribution, $\alpha_4=3$; distributions with $\alpha_4>3$ are **leptokurtic** (more peaked, heavier tails), and with $\alpha_4<3$ are **platykurtic** (flatter, lighter tails), relative to the normal. The **excess kurtosis** (kurtosis coefficient centered at zero) subtracts this reference value:
$$
K = \alpha_4 - 3 = \frac{E[(X-\mu)^4]}{\sigma^4} - 3
$$
so $K=0$ is **mesokurtic** (normal-like), $K>0$ leptokurtic, $K<0$ platykurtic.

## Properties
### Reading skew and kurtosis off a normal probability plot
On a [[Graphical and Statistical Tests for Normality|QQ plot]], departures from the ideal straight line have characteristic shapes: heavy tails (platykurtic, low kurtosis) bow the plot outward at both ends; light tails (leptokurtic, high kurtosis) bow it inward; positive skew bends the plot upward on the right; negative skew bends it downward on the left. Reading these patterns is often a faster diagnostic than computing $\alpha_3,\alpha_4$ directly.

### Jarque–Bera test
Skewness and kurtosis can be combined into a single formal goodness-of-fit test for normality:
$$
H_0: \text{the sample's skewness and kurtosis match a normal distribution} \quad\text{vs.}\quad H_1: \text{they do not}
$$
computed in R with `library(moments); jarque.test(datos)`. It is one of the tests compared in [[Graphical and Statistical Tests for Normality]].

## Examples
A simulated example draws $n=100$ observations from a Weibull($\alpha=2,\beta=100$) distribution: the sample skewness is $0.4459$, kurtosis (excess, via the `moments` package convention) is $-0.6122$, and the Jarque–Bera statistic is $JB=4.7391$ with $p\text{-value}=0.0935$ — at $\alpha=0.05$ the test does not reject normality despite the data being generated from a (moderately normal-looking, for these parameters) Weibull distribution, illustrating that Jarque–Bera is a necessary-but-not-definitive check.

A second set of four simulated samples $y_1,y_2,y_3,y_4$ illustrates the range of shapes: $y_1$ has skew $2.06$, kurtosis $6.31$ (strongly right-skewed, leptokurtic); $y_2$ has skew $0.013$, kurtosis $0.084$ (approximately symmetric and close to mesokurtic, i.e. approximately normal); $y_3$ has skew $0.70$, kurtosis $0.55$ (moderate right skew); $y_4$ has skew $-0.92$, kurtosis $1.20$ (left-skewed).

## See also
[[Graphical and Statistical Tests for Normality]], [[Data Transformations for Normality (Box-Cox and Yeo-Johnson)]], [[Chebyshev's Theorem]], [[The Multivariate Normal Distribution]]
