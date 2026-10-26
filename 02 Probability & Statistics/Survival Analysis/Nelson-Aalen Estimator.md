---
title: "Nelson-Aalen Estimator"
domain: Probability & Statistics
course: Survival Analysis
unit: "Chapter 4 - Kaplan-Meier and Nelson-Aalen estimator"
level: MSc
status: drafted
confidence: 0
tags: [survival-analysis, nelson-aalen, nonparametric, cumulative-hazard]
---
## Definition
Suggested by Nelson (1972) and independently re-discovered by Aalen (1978), the **Nelson–Aalen (N–A) estimator** targets the [[Hazard Function|cumulative hazard function]] $H(t)$ directly, using the same discrete hazard estimate $\hat h_i = d_i/n_i$ as the [[Kaplan-Meier estimate|Kaplan–Meier]] estimator:
$$
\hat H(t) = \sum_{t_i \leq t} \frac{d_i}{n_i}
$$
The corresponding survival estimate — the **Fleming–Harrington (F–H) estimator** — is
$$
\hat S(t) = \exp(-\hat H(t))
$$

## Properties
### Recursive form
Since $d_i/n_i$ estimates the discrete hazard $\hat h_i \approx P(T=t_i\mid T\geq t_i)$,
$$
\hat H(t_i) = \sum_{j\leq i}\hat h_j = \hat H(t_{i-1}) + \hat h_i
$$
As with K–M, $\hat S(t)=\hat S(t_i)$ for $t_{i-1}<t\leq t_i$ — the estimate jumps only at observed event times.

### Relationship between K–M and N–A
The K–M estimate is $\hat S_{KM}(t) = \prod_{t_j\leq t}(1-d_j/n_j)$. When $d_j/n_j$ is small (e.g. $n_j$ large), $1-x \approx \exp(-x)$, so
$$
\hat S_{KM}(t) \approx \prod_{t_j\leq t}\exp\left(-\frac{d_j}{n_j}\right) = \exp\left(-\sum_{t_j\leq t}\frac{d_j}{n_j}\right)
$$
which is exactly the N–A survival estimator $\hat S(t)=\exp(-\hat H(t))$: the two estimators agree asymptotically, differing more when $d_j/n_j$ is not small (e.g. small risk sets).

### Variance
$$
\hat\Lambda(t) \approx \sum_{t_i\leq t}\frac{d_i(n_i-d_i)}{n_i^3}
$$
used to construct a confidence interval $(H_l(t),H_u(t))$ for $\hat H(t)$, which can be exponentiated to give a CI for $\hat S(t)$.

## See also
[[Kaplan-Meier estimate]], [[Hazard Function]], [[Log-rank test]]
