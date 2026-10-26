---
title: "Exposed to Risk"
domain: Probability & Statistics
course: Survival Analysis
unit: "Chapter 6 - Exposed To Risk and Two-State model"
level: MSc
status: drafted
confidence: 0
tags: [survival-analysis, exposed-to-risk, mortality-estimation]
---
## Definition
To estimate mortality rates over a study period at a specific age $x$, we need $d_x$ (deaths between ages $x$ and $x+1$) and a measure of **exposure**: the time spent under observation at age $[x,x+1)$. Individuals typically enter the study at different points within age $x$, so exposure is only partial for many of them. For each individual define:
- $a_i$: the time at which they enter the study, measured from age $x$ (so they enter at age $x+a_i$)
- $b_i$: the time they would leave the study at age $x+b_i$, **had death not occurred**
- $b_i^*$: the time they actually leave (at age $x+b_i^*$), accounting for death if it occurred
- $\delta_i$: death indicator ($1$ if death observed in the study period, $0$ otherwise)

## Properties
### Initial exposed to risk, $E_x$
$E_x$ is the total number exposed to risk at the start of the study at exact age $x$ (if every subject entered the study at exactly age $x$ and was observed to at least $x+1$, this reduces to a simple headcount). In general,
$$
E_x = \sum_i (b_i - a_i)
$$
using $b_i$ (not $b_i^*$) — the exact time of death is not used for $E_x$.

### Central exposed to risk, $E_x^C$
$$
E_x^C = \sum_i (b_i^* - a_i)
$$
the total observed waiting time in $[x,x+1)$, ending at death, censoring, or end of study. $E_x^C$ is typically easier to compute than $E_x$; the two are related by the approximation
$$
E_x \approx E_x^C - \tfrac{1}{2}d_x
$$
where $d_x = \sum_i \delta_i$ is the total number of deaths observed in $[x,x+1)$.

### Two-state model estimation of $\mu_x$
Assuming a constant force of mortality $\mu_{x+t}\equiv\mu_x$ for $t\in[0,1)$ (see [[Two-State Model]]), the waiting time $v_i=b_i^*-a_i$ of individual $i$ has pdf $\mu_x e^{-\mu_x v_i}$ if death is observed and survival probability $e^{-\mu_x v_i}$ if censored, so each individual contributes $\mu_x^{\delta_i}\exp(-\mu_x v_i)$ to the likelihood. Multiplying over all individuals:
$$
L \propto \mu_x^{d_x}\exp(-\mu_x V), \qquad V=\sum_i v_i = E_x^C
$$
giving $\hat\mu_x = d_x/E_x^C$ (see [[Two-State Model]] for the full derivation and variance).

### Practical estimation from aggregate census data (CMI)
In practice, insurers rarely report individual entry/exit times $a_i,b_i$; instead they report $P_{x,t}$, the number of lives aged $x$ under observation at census date $t$ (submitted, e.g., to the Continuous Mortality Investigation, CMI — a UK research initiative led by the Institute and Faculty of Actuaries tracking mortality experience). Over a short interval $dt$, $P_{x,t}$ lives each contribute $dt$ of exposure, so
$$
E_x^C = \int_K^{K+N+1} P_{x,t}\,dt
$$
Since only $P_{x,t}$ at integer census times $t=K,K+1,\dots$ is known, this integral is approximated by the **trapezium rule**:
$$
\int_K^{K+1} P_{x,t}\,dt \approx \tfrac{1}{2}(P_{x,K}+P_{x,K+1}) \quad\Longrightarrow\quad E_x^C \approx \sum_{t=K}^{K+N} \tfrac{1}{2}(P_{x,t}+P_{x,t+1})
$$

## Examples
Data example (6 lives, age band $[80,81)$ in calendar year 2013): $a_i,b_i,\delta_i$ tabulated per life give $E_x = \sum(b_i-a_i) = 43/12 \approx 3.583$. Using $b_i^*$ instead gives $E_x^C = 36/12 = 3$, and the approximation checks out: $E_x \approx E_x^C + \tfrac12 d_x = 3 + \tfrac12(2) = 4$, close to the exact $43/12$.

Census example: population aged 55 on 1 Jan of 2015–2018 is $46233, 42399, 42618, 42020$. Trapezium approximation:
$$
E_{55}^C = \tfrac12(46233)+42399+\tfrac12(42618)+\tfrac12(42020) = 129{,}143.5
$$

### Practical considerations: heterogeneity
These models assume the population under observation is homogeneous (similar mortality characteristics), which is rarely true (e.g. mixing smokers and non-smokers averages two different mortality experiences). Two remedies: **stratify** the data by category (sex, policy type — at the cost of smaller samples per stratum), or use a **[[Cox Proportional Hazards Model|Cox model]]**, which incorporates groups as covariates directly.

## See also
[[Two-State Model]], [[Binomial Model for Mortality]], [[Poisson Model for Mortality]], [[Uniform Distribution of Deaths (UDD)]]
