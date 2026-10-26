---
title: "Graphical and Statistical Tests for Normality"
domain: "Machine Learning & AI"
course: "Multivariate Data Analysis"
unit: "Módulo I, Unit 2 - Normalidad"
level: BSc
status: drafted
confidence: 0
tags: [multivariate-data-analysis, normality, hypothesis-testing]
---
## Definition
Before applying a technique that assumes normality — or after applying [[Data Transformations for Normality (Box-Cox and Yeo-Johnson)|a transformation]] meant to induce it — normality must be checked, not assumed. The course teaches a battery of complementary checks: descriptive measures (mean vs. median vs. mid-range; symmetric quartiles $Q_1,Q_3$ about the median; [[Skewness and Kurtosis|skewness and kurtosis]] coefficients), a graphical method (the **QQ plot**, "gráfica de normalidad"), and formal hypothesis tests, all sharing
$$
H_0: X \sim N(\mu,\sigma) \qquad\text{vs.}\qquad H_1: X \not\sim N(\mu,\sigma)
$$

## Properties
### Construction of the QQ (normal probability) plot
The construction exploits that if $X\sim N(\mu_x,\sigma_x)$ and $Z=\frac{X-\mu_x}{\sigma_x}$, then $Z\sim N(0,1)$ and $P(X\le x)=P(Z\le z)$: the $(z,x)$ pair with matching cumulative probability lies on a line, since $x=\sigma_x z + \mu_x$. Given a sample, order the data $x_{(1)}\le\cdots\le x_{(n)}$, assign each rank $i$ an estimated cumulative probability
$$
p_i = \frac{i-0.5}{n}
$$
(the "$-0.5$" is a continuity correction), and find $z_i=\Phi^{-1}(p_i)$ (e.g. `qnorm(p_i)` in R). Plotting $x_{(i)}$ against $z_i$: **if $X$ is normal, the points fall approximately on a straight line** $x = \sigma_x z + \mu_x$, whose slope and intercept are estimates of $\sigma_x$ and $\mu_x$. In practice one only needs the accumulated-percentage scale, not $Z$ itself, so R's `qqnorm(x); qqline(x)` (or `library(car); qqPlot(x)` for confidence bands) implement this directly.

### Formal tests, compared
All test $H_0:X\sim N(\mu,\sigma)$ against $H_1$: not normal.

- **Anderson–Darling.** Based on the empirical CDF $F_n(x_i)$ vs. the normal CDF, weighting deviations in the tails more heavily. Statistic $A^2=-n-S$, $S=\frac1n\sum_{i=1}^n (2i-1)\big[\ln F(X_i)+\ln(1-F(X_{n+1-i}))\big]$. Small $A^2$ favors $H_0$; critical values are tabulated (e.g. $A^2_{0.1}=0.631$, $A^2_{0.05}=0.752$). One of the most powerful tests; recommended for $n>50$. R: `library(nortest); ad.test(x)`.
- **Ryan–Joiner.** Correlates the ordered sample with the expected normal scores, with an adjustment ($p_i=\Phi^{-1}\big(\tfrac{i-0.375}{n+0.25}\big)$) that increases sensitivity to the tails. Statistic $RJ$ close to $1$ favors $H_0$; the exact distribution of $RJ$ is unknown, so only tabulated cutoffs (by $n$ and $\alpha=0.1,0.05,0.01$) are available, not an exact $p$-value.
- **Kolmogorov–Smirnov.** Statistic $D=\max\{F_n(x)-F_0(x),\, F_0(x)-F_n(x)\}$, the maximum absolute gap between empirical and theoretical CDFs. Small $D$ favors $H_0$. The *Lilliefors* correction (`lillie.test`) is needed when $\mu,\sigma$ are estimated from the same sample (the usual case), since this invalidates the classical K–S critical values; even so, K–S/Lilliefors is comparatively weak for normality testing.
- **Shapiro–Wilk** (`shapiro.test`). Most efficient for small samples, $n<50$.
- **Cramér–von Mises** (`cvm.test`). Efficient for large samples, $n>50$; similar spirit to Anderson–Darling but without the tail up-weighting.
- **Jarque–Bera** (`jarque.test`). Based purely on sample skewness and kurtosis; see [[Skewness and Kurtosis]] for the full derivation.

Rule of thumb from the course: **Anderson–Darling for $n>50$, Shapiro–Wilk for $n<50$**, though some authors prefer Kolmogorov–Smirnov for large samples. No single test is uniformly best: different normality tests can disagree, and none reliably detects non-normality caused specifically by excess kurtosis when the underlying distribution is a $t$-distribution — so the recommendation is to triangulate: descriptive measures, QQ plot, *and* at least one formal test, never a $p$-value in isolation.

## Examples
A 20-observation sample with $\bar x=27.79$, $s=1.462$ is walked through by hand: ranks $1,\dots,20$ give $p_i=(i-0.5)/20 \in\{0.025,0.075,\dots,0.975\}$, and $z_i=\Phi^{-1}(p_i)$ ranges from $-1.96$ to $1.96$; the fitted line is $x=1.4553z+27.793$ with $R^2=0.979$, and the same sample passes Anderson–Darling ($A^2=0.189$, $p=0.888$), Ryan–Joiner ($RJ=0.988 > $ the $\alpha=0.1$, $n=20$ cutoff of $0.96$, so $H_0$ is not rejected), and Kolmogorov–Smirnov ($D=0.090 < 0.26473$, $p>0.15$).

Raúl's own graded exercise "Actividad 1.2 Normalidad univariada" (2024-08-08) runs exactly this battery on the built-in `cars$speed` dataset: `shapiro.test` ($W=0.978$, $p=0.458$), `ad.test` ($A=0.261$, $p=0.693$), `lillie.test` ($D=0.069$, $p=0.807$), and `jarque.test` ($JB=0.802$, $p=0.670$) — all four fail to reject $H_0$, concluding there is not enough statistical evidence to deny that `speed` is normally distributed.

## See also
[[Skewness and Kurtosis]], [[Data Transformations for Normality (Box-Cox and Yeo-Johnson)]], [[The Multivariate Normal Distribution]], [[Validation of Multivariate Normality]]
