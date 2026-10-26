---
title: "Statistical Tests for Graduation"
domain: Probability & Statistics
course: Survival Analysis
unit: "Chapter 8 - Graduation"
level: MSc
status: drafted
confidence: 0
tags: [survival-analysis, chi-square-test, graduation, goodness-of-fit]
---
## Definition
To test whether a set of mortality rates (crude, or [[Graduation of Mortality Rates|graduated]]) is consistent with a reference — a standard table or the graduated formula itself — we need: data, a reference (standard table or graduated rates), and a probabilistic model ([[Binomial Model for Mortality|Binomial]] or [[Poisson Model for Mortality|Poisson]]). The general null hypothesis is
$$
H_0: \text{the tested mortality rates are consistent with the reference}
$$

## Properties
### Standardised deviation
Under the Poisson model, testing $H_0:\mu_{x+1/2}=\mu_{x+1/2}^s$ uses the standardised quantity
$$
z_x = \frac{d_x - E_x^C\mu_{x+1/2}^s}{\sqrt{E_x^C\mu_{x+1/2}^s}}
$$
Under the Binomial model, testing $H_0:q_x=q_x^s$ uses
$$
z_x = \frac{d_x - E_x q_x^s}{\sqrt{E_x q_x^s(1-q_x^s)}}
$$
By the central limit theorem, $z_x\sim N(0,1)$ (approximately) for large numbers of individuals at each age. When comparing against **graduated** rates $\mu_x^o$ rather than a standard table, the same formula is used with $\mu_x^o$ in place of $\mu_x^s$.

### The chi-square test
The overall test statistic aggregates $z_x^2$ across $m$ ages $x_1,\dots,x_m$:
$$
X = \sum_{x=x_1}^{x_m} z_x^2 \sim \chi^2(m)
$$
Reject $H_0$ if $X > \chi^2_{m,1-\alpha}$ (e.g. $\alpha=0.05$). This is a specific instance of the general chi-square goodness-of-fit statistic $\chi^2=\sum_i (O_i-E_i)^2/E_i$ comparing observed to expected counts.

**Degrees of freedom**: start with the number of age groups $m$; subtract 1 if the groups are mutually exclusive categories; subtract 1 more for each parameter estimated from the data (e.g. for parametric graduation, one per fitted parameter; for standard-table graduation, one per link-function parameter plus additional constraints from the choice of table; for splines, one per fitted constant).

### Worked example (vs. standard table)
Recent data and standard table by age $x=50,\dots,59$: at $x=50$, $d_{50}^s = l_{50}-l_{51} = 32669-32513=156$, $q_{50}^s = 156/32669 = 0.00478$. Expected deaths $E_{50}q_{50}^s = 2381\times0.00478=11.369$. $z_{50} = (16-11.369)/\sqrt{2381\times0.00478(1-0.00478)} = 1.376$, $z_{50}^2=1.895$. Summing $z_x^2$ over $x=50,\dots,59$ gives $X=3.84$ on $m=10$ degrees of freedom; since $\chi^2_{10,0.95}=18.31 > 3.84$, $H_0$ is not rejected.

### Worked example (graduated rates)
Insurance company data graduated with a 2-parameter model: at $x=40$, $E_x\mu_x^o = 1248\times0.0024=3.0816$, observed $d_x=4$, so $z_{40} = (4-3.0816)/\sqrt{3.0816}=0.5232$, $z_{40}^2=1.2737$. Summing $z_x^2$ over $x=40,\dots,49$ gives $X=13.62$; with $m=10$ age groups and 2 degrees of freedom lost to the graduation, $\text{df}=8$, $\chi^2_{8,0.95}=15.51 > 13.62$, so $H_0$ is not rejected.

### Limitations of the chi-square test, and follow-up tests
1. When the test rejects $H_0$, it gives no information on *where* the discrepancy originates.
2. A few large deviations can be offset by many small ones, masking a real problem.
3. Even an unbiased-looking test can hide a run of consecutive age groups biased in the same direction.

Follow-up tests address these: the **standardised deviations test** addresses (2), the **signs test** addresses (3); other named tests include the cumulative deviations test, the grouping of signs test, and the serial correlations test.
<!-- UNVERIFIED: the signs test, cumulative deviations test, grouping of signs test, and serial correlations test are named but not derived in the lecture slides — check the course material for their exact test statistics before treating this section as complete. -->

### Standardised deviations test
Tests whether the $z_x$'s (from the standardised-deviation formula above) look like a random sample of size $m$ from $N(0,1)$ — i.e. tests for normality/correct centring of the distribution of deviations, rather than testing the deviations' magnitude directly. Method: compute $z_x$ for each age (or age group); partition the real line into convenient intervals; compare observed vs. expected counts of $z_x$ falling in each interval (expected proportions taken from the standard normal cdf, e.g. $0.34m$ in $(0,1)$, $0.14m$ in $(1,2)$, $0.02m$ in $(2,3)$, by symmetry likewise on the negative side). Forming
$$
X = \sum_{\text{all intervals}} \frac{(\text{Actual}-\text{Expected})^2}{\text{Expected}}
$$
gives (with 8 intervals) a statistic $\sim\chi^2_7$ — a different use of the chi-square distribution from the main chi-square test above: there, we test whether observed deaths match expected deaths; here, whether the *pattern* of the individual standardised deviations matches a standard normal distribution.

## See also
[[Graduation of Mortality Rates]], [[Binomial Model for Mortality]], [[Poisson Model for Mortality]], [[Likelihood Ratio Test]]
