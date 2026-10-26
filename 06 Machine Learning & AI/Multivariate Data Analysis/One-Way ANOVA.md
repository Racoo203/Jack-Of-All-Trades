---
title: "One-Way ANOVA"
domain: "Machine Learning & AI"
course: "Multivariate Data Analysis"
unit: "Módulo II, Unit 2 - ANOVA"
level: BSc
status: drafted
confidence: 0
tags: [multivariate-data-analysis, anova, dependence-analysis, hypothesis-testing]
---
## Definition
**Analysis of variance (ANOVA)** decides whether observed differences among more than two sample means can be attributed to chance, or whether they reflect real differences among the sampled populations. A **factor** is an independent (categorical) variable that can be controlled in an experiment; its levels are called **treatments**. **One-way ANOVA** applies when there is a single factor and the goal is to test whether its levels have a measurable effect on a quantitative dependent variable; a significant result indicates *at least one pair* of group means differs, without identifying *which* pair (that requires a follow-up post-hoc comparison).

Notation: $x_{ij}$ = the $j$-th observation from the $i$-th population/treatment ($i=1,\dots,k$ populations, $j=1,\dots,n$ observations each). Model assumption: the $nk$ observations $X_{ij}$ are mutually independent and normally distributed with population-specific means $\mu_i$ and a **common variance** $\sigma^2$:
$$
X_{ij} \sim N(\mu_i,\sigma)
$$

## Properties
### The linear model and hypotheses
Writing $x_{ij}=\mu_i+e_{ij}$ with $e_{ij}\sim N(0,\sigma^2)$, and substituting $\mu_i=\mu+\alpha_i$ (the **grand mean** $\mu$ plus a **treatment effect** $\alpha_i$):
$$
x_{ij} = \mu+\alpha_i+e_{ij}
$$
The hypothesis test is equivalently stated as
$$
H_0:\mu_1=\mu_2=\cdots=\mu_k=\mu \quad\text{vs.}\quad H_1: \text{not all }\mu_i\text{ equal} \qquad\Longleftrightarrow\qquad H_0:\alpha_i=0\ \forall i \quad\text{vs.}\quad H_1:\alpha_i\neq0\text{ for at least one }i
$$

### Variance decomposition
ANOVA detects mean differences by comparing **between-group variance** (how spread out the group means are from each other) against **within-group variance** (how spread out individual observations are within their own group). Formally, Total Sum of Squares splits as
$$
\text{TSS} = \text{SSTr} + \text{SSE}
$$
$$
\text{SSTr} = n\sum_{i=1}^k(\bar X_i-\bar X)^2 \ \text{(between groups)}, \qquad \text{SSE} = \sum_{i=1}^k\sum_{j=1}^n (x_{ij}-\bar X_i)^2\ \text{(within groups)}, \qquad \text{TSS}=\sum_{i=1}^k\sum_{j=1}^n(x_{ij}-\bar X)^2
$$
Under $H_0$, the between-group variance and the within-group variance both estimate the same population $\sigma^2$; as the group means drift further apart, the between-group variance grows relative to the (unaffected) within-group variance.

### The ANOVA table and the F-test
| Source | df | Sum of Squares | Mean Square | F statistic |
|---|---|---|---|---|
| Between groups (Treatments) | $k-1$ | $\text{SSTr}=n\sum_i(\bar X_i-\bar X)^2$ | $\text{MSTr}=\dfrac{\text{SSTr}}{k-1}$ | $f=\dfrac{\text{MSTr}}{\text{MSE}}$ |
| Within groups (Error) | $k(n-1)$ | $\text{SSE}=\sum_i\sum_j(x_{ij}-\bar X_i)^2$ | $\text{MSE}=\dfrac{\text{SSE}}{k(n-1)}$ | |
| Total | $kn-1$ | $\text{TSS}$ | | |

MSTr is the *intervarianza* (variance explained by the treatment/group differences); MSE is the *intravarianza* (residual/error variance not explained by group membership). The test statistic
$$
f = \frac{\text{MSTr}}{\text{MSE}} \sim F_{k-1,\,k(n-1)}
$$
**Decision rule:** reject $H_0$ if $f > F_{\alpha,\,k-1,\,k(n-1)}$, equivalently if $p\text{-value}<\alpha$.

### Residual analysis and model verification
The model assumes observations follow a normal distribution, independently, with equal variance across treatments — verified through the residuals $e_{ij}=x_{ij}-\bar X_i$: **normality** via a normal probability plot of the residuals ([[Graphical and Statistical Tests for Normality]]); **constant variance across treatments** by plotting residuals against factor level and comparing their spread; **independence** by plotting residuals against time/run order and checking for a pattern (a visible pattern suggests the observations are not independent).

### Confidence interval for a treatment mean
A $100(1-\alpha)\%$ confidence interval for the $i$-th treatment mean $\mu_i$:
$$
\bar X_i - t_{\alpha/2,\,k(n-1)}\sqrt{\frac{\text{MSE}}{n}} \;\le\; \mu_i \;\le\; \bar X_i + t_{\alpha/2,\,k(n-1)}\sqrt{\frac{\text{MSE}}{n}}
$$

## Examples
**Detergent whiteness study.** Three detergents are compared on whiteness readings ($k=3$, $n=5$ per group): Detergent A: 77, 81, 71, 76, 80; B: 72, 58, 74, 66, 79; C: 76, 85, 82, 80, 77 (group means $77,68,80$). Testing at $\alpha=0.01$ whether these mean differences are statistically significant is the course's worked exercise, following exactly the ANOVA-table procedure above: compute SSTr, SSE, MSTr, MSE, the $f$ statistic, and compare against $F_{0.01,\,2,\,12}$.

## See also
[[Simple Linear Regression and Least Squares]], [[Multiple Linear Regression]], [[Graphical and Statistical Tests for Normality]], [[Confidence and Prediction Intervals in Regression]]
