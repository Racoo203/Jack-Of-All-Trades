---
title: "Kaplan-Meier estimate"
domain: Probability & Statistics
course: Survival Analysis
unit: "Chapter 4 - Kaplan-Meier and Nelson-Aalen estimator"
level: MSc
status: drafted
confidence: 0
tags: [survival-analysis, kaplan-meier, nonparametric]
---
## Definition
A [[Parametric Survival Models|parametric]] survival model may not fit the data well, motivating **nonparametric** (distribution-free) estimators of $S(t)$. Without censoring, the empirical survival function $\hat S(t) = \dfrac{\#\{\text{individuals} > t\}}{\text{total individuals}}$ would suffice, but with censoring we do not always know whether a censored individual had $T>t$.

Suppose $D$ distinct event times $t_1<t_2<\cdots<t_D$ are observed. Let $d_i$ be the number of individuals experiencing the event at $t_i$, and $n_i$ the **number at risk** at $t_i$ (individuals who have not yet had the event or been censored, including those who experience the event exactly at $t_i$). The **Kaplan–Meier (K–M) estimator**, proposed by Kaplan and Meier (1958), is
$$
\hat S(t) = \begin{cases} 1 & t<t_1 \\ \displaystyle\prod_{t_i\leq t}\left(1-\frac{d_i}{n_i}\right) & t_1\leq t \end{cases}
$$
also called the **product-limit estimator**: a step function, constant between consecutive event times and jumping only at event times, with jump size depending on $d_i$ and on the pattern of censoring.

## Properties
### Motivation via conditional survival
For each event time $t_i$,
$$
S(t_i) = P(T>t_i) = P(T>t_i\mid T>t_{i-1})P(T>t_{i-1}) = (1-h_i)S(t_{i-1})
$$
where $h_i = P(T=t_i\mid T>t_{i-1})$ is the discrete hazard at $t_i$, estimated by $\hat h_i = d_i/n_i$. Unrolling the recursion,
$$
S(t_i) = (1-h_i)(1-h_{i-1})\cdots(1-h_1) \quad\Longrightarrow\quad \hat S(t_i) = \prod_{j\leq i}\left(1-\frac{d_j}{n_j}\right)
$$

### Derivation as an MLE
Assume events can only occur at times $t_1,\dots,t_n$, and let $p_j = P(T>t_j\mid T>t_{j-1})$. The likelihood of observing $n_j-d_j$ survivors and $d_j$ events at each $t_j$ is
$$
L(p_1,\dots,p_n) = \prod_{j=1}^n p_j^{\,n_j-d_j}(1-p_j)^{d_j}
$$
Log-likelihood: $l = \sum_j (n_j-d_j)\ln p_j + d_j\ln(1-p_j)$. Differentiating with respect to $p_j$ and setting to zero:
$$
\frac{n_j-d_j}{p_j} - \frac{d_j}{1-p_j} = 0 \quad\Longrightarrow\quad \hat p_j = \frac{n_j-d_j}{n_j} = 1-\frac{d_j}{n_j}
$$
so the K–M estimator $\hat S(t) = \prod_{t_j\leq t}(1-d_j/n_j)$ is the MLE under this discrete-time construction.

### Greenwood's formula (variance)
$$
\hat V[\hat S(t)] = \hat S(t)^2 \sum_{t_i\leq t} \frac{d_i}{n_i(n_i-d_i)}
$$
used for standard errors $\sqrt{\hat V[\hat S(t)]}$ and (Wald) confidence intervals $\hat S(t) \pm 1.96\sqrt{\hat V[\hat S(t)]}$.

### At a censoring time
At a censoring time (no event, $d_i=0$), $1-d_i/n_i=1$, so $\hat S$ is unchanged from the previous event time — censoring does not itself move the K–M curve, but it removes individuals from the risk set $n_i$ going forward.

### R software note
In R's `survival` package, `survfit(Surv(time, event) ~ group, data = ...)` fits the K-M estimator (per group if a factor is given on the right-hand side), and `summary()` tabulates $\hat S(t)$ with standard errors and a confidence interval at each event time. By default `survfit` reports `conf.type = "log"`, i.e. a confidence interval built on the log scale (using the delta method on $\ln\hat S(t)$) rather than the linear Greenwood interval $\hat S(t)\pm1.96\sqrt{\hat V[\hat S(t)]}$ derived above — the log-transformed interval stays within $[0,1]$ and is generally preferred in practice, while the Greenwood-based linear interval can overshoot below 0 or above 1 for $\hat S(t)$ near the boundary. `plot(fit, conf.int=TRUE, conf.type="log", mark.time=TRUE)` draws the step function with censoring times marked and the chosen CI type shaded.

## Examples
PhD-completion data (22 students, times sorted): $\hat S(3)=1(1-1/21)=0.952$, $\hat S(3.2)=0.952(1-1/20)=0.905$, ..., $\hat S(4.2)=0.706(1-1/13)=0.652$ — a step function decreasing at each completion time and unchanged at censoring times (e.g. $t=3.55$, $d=0$).

## See also
[[Nelson-Aalen Estimator]], [[Log-rank test]], [[Censoring in Survival Analysis]], [[Likelihood Function for Censored Survival Data]], [[Accelerated Failure Time Model]]
