---
subject: Survival Analysis
type: MOC
exam_date: 2026-06-02
status: drafted
confidence: 0
tags:
  - moc
  - exam
  - survival-analysis
domain: Probability & Statistics
---
## Concept narrative

The course opens by formalising **survival time** as a positive random variable $T$, and builds the four equivalent descriptions of its distribution — the **[[Lifetime Function|cdf, pdf and survival function]]** and the **[[Hazard Function|hazard function]]** — before specialising to the actuarial setting via **[[Force of Mortality and Actuarial Notation|lifetime after age $x$, $T_x$, and actuarial notation]]** (${}_tp_x$, ${}_tq_x$, $\mu_x$). **[[Parametric Survival Models]]** (Exponential, Weibull, Log-normal) illustrate constant, monotone, and non-monotone hazard shapes. This machinery is then tabulated as a **[[Life Table]]**, with the **[[Uniform Distribution of Deaths (UDD)|UDD]]** assumption bridging exact and fractional ages, and **[[Curtate Future Lifetime]]** giving the discrete-time analogue used in practice. **[[Gompertz' Law|Gompertz' and Makeham's laws]]** provide closed-form mortality curves, and **[[Censoring in Survival Analysis|censoring]]** together with the general **[[Likelihood Function for Censored Survival Data|likelihood under censoring]]** sets up all subsequent estimation.

Nonparametric estimation follows: the **[[Kaplan-Meier estimate|Kaplan–Meier]]** and **[[Nelson-Aalen Estimator|Nelson–Aalen]]** estimators of $S(t)$ and $H(t)$, and the **[[Log-rank test]]** for comparing survival between groups. Regression enters through the **[[Proportional Hazards Model|(parametric) proportional hazards model]]** and its semi-parametric generalisation, the **[[Cox Proportional Hazards Model|Cox model]]** (partial likelihood, **[[Wald Test]]**, **[[Likelihood Ratio Test]]**, variable selection). The course then turns to population-level mortality estimation: **[[Exposed to Risk]]** (initial vs. central exposure) and the **[[Two-State Model]]** underpin the **[[Binomial Model for Mortality|Binomial]]** and **[[Poisson Model for Mortality|Poisson]]** models for $q_x$/$\mu_x$, and **[[Graduation of Mortality Rates|graduation]]** smooths crude estimates against parametric formulae, standard tables, or splines, assessed via the **[[Statistical Tests for Graduation|chi-square and standardised-deviations tests]]**.

The final third of the course is largely self-contained: **[[Extreme Value Theory]]** studies the limiting distribution of extreme observations, motivated by insurance tail risk — block maxima converge to a GEV distribution, threshold exceedances to a GPD — and **[[Copula|copulas]]** (fundamental, **[[Archimedean Copula|Archimedean]]**, and **[[Gaussian Copula|Gaussian]]**) model dependence between two lifetimes/risks independently of their marginals, quantified via **[[Measures of Association|Kendall's tau and Spearman's rho]]** and, for joint extremes specifically, **[[Tail Dependence]]**.

A set of **PGT (postgraduate-taught) extension lectures** builds on Chapters 5–6 with material not in the undergraduate slides but examinable for PGT-level students: the **[[Two-State Model|two-state model]]** generalises to the **[[Multi-State Markov Model|multi-state Markov model]]** (Chapman–Kolmogorov equations, generator matrix, full MLE for transition intensities); **[[Mortality Projection Models|mortality forecasting]]** extends static laws like [[Gompertz' Law]] to the age-period and **Lee–Carter** models, fitted by Poisson maximum likelihood and forecast via a random walk with drift; the **[[Accelerated Failure Time Model|accelerated failure time (AFT) model]]** offers an alternative to proportional hazards, acting multiplicatively on survival time rather than on the hazard (Exponential and Weibull models can be both AFT and PH; log-logistic is AFT-only); and **[[Time-Varying Covariates and Stratified Cox Models|stratified and time-dependent Cox models]]** relax the PH assumption when it fails, either by allowing a separate baseline hazard per stratum or letting a covariate's effect itself change over time. The **[[Censoring in Survival Analysis|censoring]]** and **[[Likelihood Function for Censored Survival Data|likelihood]]** framework from Chapter 3 also extends here to left- and interval-censored data via parametric likelihoods, since Kaplan-Meier and Cox cannot handle those censoring types directly.

---

## Concept map

### Chapter 1 — Concept of survival models
- [[Lifetime Function]]: $T$, $F(t)$, $f(t)$, $S(t)=1-F(t)$
- [[Hazard Function]]: $h(t)=f(t)/S(t)=-d\ln S(t)/dt$; $S(t)=\exp(-H(t))$
- [[Force of Mortality and Actuarial Notation]]: $T_x$, ${}_tp_x$, ${}_tq_x$, $\mu_x$, ${}_{u|t}q_x$
- [[Mean and Variance of Survival Time]]: $\mathbb{E}(T)=\int_0^\infty S(u)du$, mean residual lifetime
- [[Parametric Survival Models]]: [[Exponential distribution|Exponential]] (constant hazard, memoryless), [[Weibull distribution|Weibull]] (monotone hazard), [[Lognormal distribution|Log-normal]] (non-monotone hazard)

### Chapter 2 — Lifetime after age x and life tables
- [[Life Table]]: $l_x$, $d_x$, radix, construction, expectation of life $\overset{\circ}{e}_x=T_x/l_x$
- [[Uniform Distribution of Deaths (UDD)]]: $l_{x+t}=(1-t)l_x+tl_{x+1}$, ${}_tq_x=tq_x$
- [[Curtate Future Lifetime]]: $K_x=\lfloor T_x\rfloor$, $e_x=\sum_k {}_kp_x$, $\overset{\circ}{e}_x\approx e_x+\tfrac12$

### Chapter 3 — Laws of mortality and censoring
- [[Gompertz' Law]]: $\mu_x=Bc^x$ (Gompertz), $\mu_x=A+Bc^x$ (Makeham)
- [[Censoring in Survival Analysis]]: right (Type I/II), left, interval, non-informative
- [[Likelihood Function for Censored Survival Data]]: $L=\prod h(t_i)^{\delta_i}S(t_i)$, MLE under censoring

### Chapter 4 — Kaplan-Meier and Nelson-Aalen estimators
- [[Kaplan-Meier estimate]]: $\hat S(t)=\prod_{t_i\leq t}(1-d_i/n_i)$, Greenwood's formula
- [[Nelson-Aalen Estimator]]: $\hat H(t)=\sum d_i/n_i$, Fleming–Harrington $\hat S(t)=\exp(-\hat H(t))$
- [[Log-rank test]]: $Q\sim\chi^2_1$, Mantel–Cox test for $S_0(t)=S_1(t)$

### Chapter 5 — The proportional hazards model
- [[Proportional Hazards Model]]: $h(t|x)=h_0(t)\exp(x\beta)$, Gompertz PH, Weibull PH
- [[Cox Proportional Hazards Model]]: partial likelihood $L_p(\beta)$, Breslow estimator, variable selection
- [[Wald Test]]: $z^2=\hat\beta^2 I(\hat\beta)\sim\chi^2_1$
- [[Likelihood Ratio Test]]: nested models, $2|\ln L_2-\ln L_1|\sim\chi^2_k$

### Chapter 6 — Exposed to risk and the two-state model
- [[Exposed to Risk]]: $E_x=\sum(b_i-a_i)$, $E_x^C=\sum(b_i^*-a_i)$, CMI trapezium approximation
- [[Two-State Model]]: alive/dead Markov model, $\hat\mu_x=d_x/E_x^C$

### Chapter 7 — Mortality models
- [[Binomial Model for Mortality]]: naive vs. practical, actuarial estimator $\tilde q_x=d_x/(E_x^C+\tfrac12 d_x)$
- [[Poisson Model for Mortality]]: $d_x\sim\text{Poisson}(\mu_x E_x^C)$, $\hat\mu_x=d_x/E_x^C$

### Chapter 8 — Graduation
- [[Graduation of Mortality Rates]]: parametric formula, standard-table reference, splines
- [[Statistical Tests for Graduation]]: chi-square test, standardised deviations test, degrees of freedom

### Chapter 9 — Extreme Value Theory
- [[Extreme Value Theory]]: block maxima $X_M$, Fisher-Tippett-Gnedenko theorem, GEV domains (Weibull/Gumbel/Fréchet), GPD/threshold exceedances, tail-weight measures (moments, density ratios)

### Chapter 10 — Copulas and measures of association
- [[Copula]]: Sklar's theorem, Fréchet–Hoeffding bounds, fundamental copulas $\Pi,M,W$
- [[Archimedean Copula]]: Clayton, Frank, Gumbel, Joe
- [[Gaussian Copula]]: implicit copula, correlation parameter $\alpha$
- [[Measures of Association]]: Kendall's $\tau$, Spearman's $\rho$
- [[Tail Dependence]]: $\lambda_L$, $\lambda_U$

### PGT Lectures — Extensions beyond the core syllabus
- [[Multi-State Markov Model]]: Chapman–Kolmogorov equations, generator matrix $\{\mu^{ij}\}$, Kolmogorov forward equations, MLE $\hat\mu^{ik}_x=D^{ik}/T^{(i)}$
- [[Mortality Projection Models]]: age-period model, Lee-Carter ($\ln m_{x,t}=a_x+b_xk_t$), Poisson MLE fitting, $k_t$ forecast via random walk with drift, Renshaw–Haberman cohort effect
- [[Accelerated Failure Time Model]]: $S_1(t)=S_2(\gamma t)$, Exponential/Weibull AFT (=PH iff shared shape), log-logistic AFT (not PH), log-log plot diagnostics
- [[Time-Varying Covariates and Stratified Cox Models]]: stratified Cox $h_g(t|X)=h_{0g}(t)\exp(X\beta)$, time-dependent Cox with $X(t)\times\log(t)$ interaction

---

## Key dependency chains

```
T → F(t)/f(t)/S(t) → Hazard h(t) → Force of Mortality μx → Actuarial Notation (tpx, tqx)
    → Parametric Models (Exp/Weibull/Lognormal) → Gompertz/Makeham Laws

Actuarial Notation → Life Table (lx, dx) → UDD → Curtate Future Lifetime (Kx, ex)

Censoring → Likelihood under Censoring → Kaplan-Meier / Nelson-Aalen → Log-rank Test
                                        → Proportional Hazards → Cox Model → Wald/LRT

Two-State Model ← Exposed to Risk (Ex, ExC) → Binomial Model / Poisson Model → Graduation → Chi-square Test
    → Multi-State Markov Model (generator matrix, MLE μ^ik_x = D^ik/T^(i))

Gompertz/Makeham Laws → Mortality Projection Models (age-period, Lee-Carter) → forecast kt (random walk + drift)

Proportional Hazards → Cox Model → Checking PH assumption (log-log plot) → Stratified/Time-Dependent Cox Model
                                                                          → Accelerated Failure Time Model (Exp/Weibull AFT=PH; log-logistic AFT-only)

Censoring (left/interval) → Parametric Survival Models → Likelihood under Censoring (F(x), F(x2)-F(x1) terms)

Block Maxima (XM = max Xi) → Extreme Value Theorem → GEV (Weibull/Gumbel/Fréchet domains) → GEV scaling laws
Threshold Exceedance (X-u|X>u) → GPD → GPD scaling laws

Copula (Sklar's Theorem) → Archimedean / Gaussian Copula → Measures of Association (τ, ρ)
                                                          → Tail Dependence (λL, λU) ← Extreme Value Theory (tail weight)
```

---

## Exam focus

### High priority
- **Derivations from first principles**: $h(t)=f(t)/S(t)$, $S(t)=\exp(-H(t))$; the Kaplan–Meier estimator as an MLE; the Cox partial likelihood derivation; Gompertz' survival function.
- **Actuarial notation manipulation**: converting between ${}_tp_x$, ${}_tq_x$, $\mu_x$, $l_x$, $d_x$; UDD-based fractional-age calculations; curtate vs. complete expectation of life.
- **Censored likelihoods**: constructing $L=\prod h(t_i)^{\delta_i}S(t_i)$ for a given parametric model and finding the MLE (classic: Exponential).
- **Kaplan-Meier / log-rank by hand**: building the risk-set table $(t_i,d_i,n_i)$ and computing $\hat S(t)$, Greenwood's variance, and the log-rank $\chi^2$ statistic for two groups.
- **Cox model interpretation**: reading `coef`, `exp(coef)`, `se(coef)`, `z`, p-value from software output; interpreting hazard ratios; forward/backward variable selection via Wald or LRT.
- **Exposed to risk calculations**: computing $a_i, b_i, b_i^*$ from entry/exit dates and deriving $E_x$, $E_x^C$ by hand.
- **Graduation chi-square tests**: computing $z_x$, $X=\sum z_x^2$, degrees of freedom (accounting for fitted parameters), and comparing to critical values.
- **Copula identities**: verifying $\tau_{X,Y}$ and $\rho_{X,Y}$ from a given copula by direct integration; computing tail dependence coefficients $\lambda_L,\lambda_U$ as limits.
- **Multi-state MLE (PGT)**: partitioning an individual's observed history into intervals, writing the likelihood contribution per interval/transition, and solving $\hat\mu^{ik}_x=D^{ik}/T^{(i)}$ with its variance — confirmed as an exam/exercise question type (sickness-death 3-state model, worked in [[Multi-State Markov Model]]).
- **Mortality forecasting (PGT)**: writing down the Lee-Carter Poisson likelihood; forecasting $m_{x,t}$ at a future age/year given fitted $a_x,b_x$ and a random-walk-with-drift $k_t$ — confirmed exam/exercise question type (worked example in [[Mortality Projection Models]]).
- **PH/AFT assumption checking (PGT)**: producing and interpreting a $\log(-\log\hat S(t))$ vs. $t$ (or $\log t$) plot to check proportional hazards, or the analogous plot to check the Weibull/log-logistic AFT assumption — see [[Cox Proportional Hazards Model]] and [[Accelerated Failure Time Model]].
- **R software fluency**: reading `survfit`/`summary()` output (K-M, log CI by default), `survdiff` output (log-rank), and `coxph`/`logLik()` output (Cox model, LRT via `pchisq`) — confirmed conventions from Lab Materials.
- **Extreme value theory**: deriving the standardising constants $\alpha_n,\beta_n$ and the GEV domain (Weibull/Gumbel/Fréchet) for a named distribution; computing exact vs. GEV-approximated probabilities that a sample maximum exceeds a threshold; computing limiting density ratios to compare tail weight; using GEV/GPD scaling laws to change block size or threshold — all confirmed exam/exercise question types.

### Common question types
- "Derive the survival/hazard/pdf relationship for [a given parametric law]."
- "Given entry/exit data for $n$ lives, compute $E_x$ and $E_x^C$ for the age band $[x,x+1)$."
- "Construct the Kaplan-Meier table and estimate $S(t)$ at a given time; compute a 95% CI using Greenwood's formula."
- "Test $H_0: S_0(t)=S_1(t)$ using the log-rank test for two given groups."
- "Fit a Cox model and interpret the hazard ratio / test significance via the Wald test."
- "Given a standard table and observed deaths, test whether the recent experience is consistent with it via the chi-square test."
- "Given a copula $C(u,v;\theta)$, compute Kendall's tau / Spearman's rho / the tail dependence coefficients."
- "Given a claim-size distribution, compute the exact and GEV-approximated probability that the maximum of $n$ claims exceeds a threshold." *(Chapter 9)*
- "Given two densities, compute $\lim_{x\to\infty} f_1(x)/f_2(x)$ and interpret which has the heavier tail." *(Chapter 9)*
- "Given an individual's transition history in a sickness-death model, write the likelihood contribution and estimate $\mu^{ik}_x$." *(PGT)*
- "Given fitted Lee-Carter parameters and a drift $\mu$, forecast $m_{x,t}$ for a future age/year." *(PGT)*
- "Given survival curves for two groups, assess whether the PH or AFT assumption is more appropriate using a log-log plot." *(PGT)*

## Open questions

- _Chapter 9 (Extreme Value Theory) — **resolved 2026-09-18**: the lecture PDF and both Exercises & Solutions PDFs appeared in `Resources/.../Chapter 9 - Extreme Value Theory/` (they were confirmed absent in an earlier check the same session) and have now been fully incorporated into [[Extreme Value Theory]] — GEV/GPD derivations, scaling laws, tail-weight measures, and both worked exam-style exercises (Pareto and Exponential claims). UNVERIFIED marker removed, `status: drafted`._
- _The signs test, cumulative deviations test, grouping of signs test, and serial correlations test are still named but not derived anywhere in the available material (lecture slides, all Exercises & Solutions, PGT lectures, exams, and the CT4 reference document were all checked) — [[Statistical Tests for Graduation]] remains UNVERIFIED for these four tests specifically._
- _Makeham's law survival function (in [[Gompertz' Law]]) is now **confirmed** against Exercises & Solutions Chapter 3, Q3 — UNVERIFIED marker removed._
- _Past exam papers (2021–2025 solved paper, mock exam, log-rank revision problem, two-state/Markov mock questions), the PGT lecture series (multi-state models, mortality projections, AFT models, stratified/time-dependent Cox), Lab Materials (LAB 1–5, R scripts, mock test), and all per-chapter Exercises & Solutions have now been reviewed (second ingestion pass, 2026-09-18) and incorporated into the relevant notes and this MOC._
- _The PGT lectures use the same two-state/Markov notation as the core course (no conflicting conventions found), and do overlap conceptually with [[MOC - Stochastic Processes|Stochastic Processes]] (Chapman-Kolmogorov, generator matrices) — cross-links added in [[Multi-State Markov Model]]._
