---
title: "Log-rank test"
domain: Probability & Statistics
course: Survival Analysis
unit: "Chapter 4 - Kaplan-Meier and Nelson-Aalen estimator"
level: MSc
status: drafted
confidence: 0
tags: [survival-analysis, log-rank-test, hypothesis-testing]
---
## Definition
The **log-rank test** (also known as the **Mantel–Cox test**) tests whether the survival function differs between two groups:
$$
H_0: S_0(t)=S_1(t) \qquad H_1: S_0(t)\neq S_1(t) \text{ for some } t
$$
Let $t_1<\cdots<t_D$ be the ordered distinct event times across both groups combined. At each $t_i$ form the contingency table with counts at risk $n_{i0},n_{i1}$ (total $n_i=n_{i0}+n_{i1}$) and events $d_{i0},d_{i1}$ (total $d_i=d_{i0}+d_{i1}$).

## Properties
### Expected events under $H_0$
Under $H_0$, the expected number of events in group $j$ at $t_i$, treating the hypergeometric draw of $d_i$ events from $n_i$ at risk as evenly split by group size, is
$$
\hat e_{ij} = \frac{d_i}{n_i}n_{ij}, \qquad j=0,1
$$
with variance (hypergeometric variance)
$$
\hat V(\hat e_{ij}) = \frac{n_{i0}n_{i1}\,d_i(n_i-d_i)}{n_i^2(n_i-1)}
$$

### Test statistic
$$
Q_j = \frac{\left(\sum_{i=1}^D d_{ij} - \sum_{i=1}^D \hat e_{ij}\right)^2}{\sum_{i=1}^D \hat V(\hat e_{ij})}, \qquad j=0,1
$$
which follows a $\chi^2_1$ distribution under $H_0$; reject $H_0$ if $Q > \chi^2_{1,1-\alpha}$.

### $Q_0 = Q_1$
Since $d_i=d_{i0}+d_{i1}$, $n_i=n_{i0}+n_{i1}$, and $\hat V(\hat e_{i0})=\hat V(\hat e_{i1})$, the two group-wise statistics are equal, so in practice only one needs to be computed. Sketch: writing $O_0=\sum d_{i0}$, $E_0=\sum\hat e_{i0}$, expand $O_0-E_0$ in terms of $d_{i1}$ and $\hat e_{i1}$ using $d_{i0}=d_i-d_{i1}$ and $\hat e_{i0}=d_i-\hat e_{i1}$: the algebra telescopes to $-(O_1-E_1)$, and squaring removes the sign, giving $Q_0=Q_1$.

## Examples
PhD-completion data by department (10 physics, 12 math). Using $\delta_i=1$ events, $O_0=\sum d_{i0}=6$ (math events observed), $E_0=\sum\hat e_{i0}=7.0395$, $V=3.344805$:
$$
Q_0 = \frac{(O_0-E_0)^2}{V} = \frac{(6-7.0395)^2}{3.344805} = 0.3137
$$
Since $Q_0=0.3137 < \chi^2_{1,0.95}=3.84$, we fail to reject $H_0$: no evidence the survival functions differ between departments.

### Limitations of K–M and the log-rank test
- Can only examine categorical covariates one at a time.
- Continuous covariates must be categorised.
- Does not quantify the size of an effect.
- Cannot explore interactions or combinations of covariates (e.g. gender and race jointly) — this motivates regression approaches such as the [[Proportional Hazards Model]].

### R software note
In R's `survival` package, `survdiff(Surv(time, event) ~ group, data = ...)` performs the log-rank test directly, e.g. `survdiff(Surv(week, arrest) ~ fin, data = Rossi)`; its output reports observed (`N`, `Observed`) vs expected (`Expected`) events per group and the resulting $\chi^2_1$ statistic with p-value — matching $Q_0=Q_1$ above (`survdiff` reports a single combined statistic rather than separate $Q_0,Q_1$).

## See also
[[Kaplan-Meier estimate]], [[Nelson-Aalen Estimator]], [[Proportional Hazards Model]], [[Cox Proportional Hazards Model]]
