---
title: "Mortality Projection Models"
domain: Probability & Statistics
course: Survival Analysis
unit: "PGT Lectures"
level: MSc
status: drafted
confidence: 0
tags: [survival-analysis, mortality-forecasting, lee-carter, pgt-extension]
---
## Definition
Static laws such as [[Gompertz' Law|Gompertz/Makeham]] estimate mortality $\mu_x$ as a function of age alone. In practice insurers and governments need mortality to vary jointly by **age $x$ and calendar year (period) $t$**, $m_{x,t}$, so that future rates can be *forecast*. Accurate forecasts matter both ways: underestimating future mortality improvement threatens an annuity/pension provider's solvency, while overestimating it makes products uncompetitive; governments need it to budget health and social care.

## Properties

### Age-period model
The simplest two-way model is
$$
\ln(m_{x,t}) = a_x + k_t + \epsilon_{x,t}
$$
where $a_x$ is the general shape of mortality by age and $k_t$ tracks the (age-independent) change in mortality over time.

**Identifiability.** The model is invariant under $k_t \to k_t + c$, $a_x \to a_x - c$, so a constraint such as $\sum_t k_t = 0$ must be imposed to pin down a unique solution.

*Advantage*: easy to interpret. *Disadvantage*: it forces every age to experience the **same** absolute improvement $k_t$ each period, which is empirically false (mortality improvements are age-dependent).

### Lee-Carter model
The Lee-Carter model introduces an age-period **interaction**:
$$
\ln(m_{x,t}) = a_x + b_x k_t + \epsilon_{x,t}
$$
- $a_x$: overall age-shape of (log) mortality.
- $k_t$: mortality index tracking the change over time.
- $b_x$: sensitivity of age $x$ to changes in $k_t$ (how much each age benefits from the general trend).

**Identifiability.** Three transformations leave $m_{x,t}$ unchanged: (i) $k_t \to k_t + c,\ a_x \to a_x - b_x c$; (ii) simultaneously $b_x \to \lambda b_x,\ k_t \to k_t/\lambda$. Two constraints are therefore imposed:
$$
\sum_t k_t = 0, \qquad \sum_x b_x = 1.
$$

**Interpretation of $a_x$.** Averaging the model over the $Y$ observed years and using $\sum_t k_t = 0$:
$$
\frac{1}{Y}\sum_{t=1}^{Y} \ln(m_{x,t}) = \frac{1}{Y}\sum_{t=1}^{Y}(a_x + b_x k_t) = \frac{1}{Y}\Big(Y a_x + b_x \cdot 0\Big) = a_x,
$$
so $a_x$ is exactly the age-$x$ average log-mortality over the fitted period, while $b_x$ governs how much that age deviates from its average as $k_t$ moves.

#### Rough (least-squares) estimation
A quick, non-likelihood-based fit proceeds in three steps:
1. **Estimate $a_x$**: $\hat a_x = \frac{1}{Y}\sum_{t=1}^{Y}\ln(m_{x,t})$ (the age-$x$ time average, as derived above).
2. **Estimate $k_t$**: sum the model over ages $x$ and use $\sum_x b_x = 1$:
$$
\sum_x \ln(m_{x,t}) = \sum_x a_x + k_t\sum_x b_x + \sum_x \epsilon_{x,t} \implies \hat k_t = \sum_x \ln(m_{x,t}) - \sum_x \hat a_x.
$$
3. **Estimate $b_x$**: minimise the residual sum of squares $\sum_t \epsilon_{x,t}^2 = \sum_t\big(\ln(m_{x,t}) - \hat a_x - b_x\hat k_t\big)^2$ over $b_x$ for each age, an ordinary least-squares problem giving
$$
\hat b_x = \frac{\sum_t \hat k_t\big(\ln(m_{x,t}) - \hat a_x\big)}{\sum_t \hat k_t^2}.
$$

#### Maximum-likelihood fitting
In practice the rough method above is not used; instead deaths are modelled as Poisson counts driven by the Lee-Carter rate:
$$
d_{x,t} \sim \mathrm{Poisson}\big(E_{x,t}\, m_{x,t}^c\big), \qquad \ln(m_{x,t}) = a_x + b_x k_t,
$$
(cf. the [[Poisson Model for Mortality|Poisson model for a single age]]). The joint likelihood is
$$
L(a,b,k) \propto \prod_{x=1}^{X}\prod_{t=1}^{T} e^{-e^{a_x+b_x k_t}}\,\big(e^{a_x+b_x k_t}\big)^{d_{x,t}},
$$
which has no closed form in $(a_x,b_x,k_t)$ jointly and is solved numerically (e.g. via iterative Newton-Raphson cycling through the three parameter sets). This is the approach implemented in the R package `StMoMo`, used e.g. to fit the Lee-Carter model to UK mortality data 1841-2021 (CMI, Continuous Mortality Investigation).

### Forecasting
Once $\hat a_x, \hat b_x$ are fixed from the fitted period, only $k_t$ needs to be projected forward, typically with a **random walk with drift**:
$$
k_t = k_{t-1} + \mu + e_t,
$$
appropriate when $k_t$ trends roughly linearly in $t$ (a simple linear regression $k_t = \alpha + \beta t + e_t$ is a common alternative). The drift is estimated from consecutive fitted values, e.g. from $n$ intervals:
$$
\hat\mu = \frac{1}{n}\big(\hat k_{t_{\text{last}}} - \hat k_{t_{\text{first}}}\big),
$$
and then $\hat k_{t^\star} = \hat k_{t_{\text{last}}} + (t^\star - t_{\text{last}})\hat\mu$ for a future year $t^\star$.

**Worked example.** Fitted parameters $a_{60}=-2,\ a_{61}=-2.2,\ b_{60}=0.0025,\ b_{61}=0.002$, with $k_t = k_{t-1}+\mu,\ \mu=-0.12$, and $k_{2023}=0.1$:
$$
k_{2025} = k_{2023}+2\mu = 0.1 - 0.24 = -0.14, \qquad m_{60,2025} = \exp(a_{60}+k_{2025}b_{60}) = \exp(-2 - 0.14\times 0.0025) \approx 0.1349,
$$
$$
k_{2026} = k_{2023}+3\mu = 0.1 - 0.36 = -0.26, \qquad m_{61,2026} = \exp(a_{61}+k_{2026}b_{61}) = \exp(-2.2 - 0.26\times 0.002) \approx 0.1108.
$$

### Advantages and disadvantages
*Advantage*: once parameters are estimated, forecasting reduces to a standard univariate time-series problem for $k_t$.

*Disadvantages*:
- Projections become progressively rougher (wider, less reliable) the further ahead one forecasts.
- The model imposes a constant ratio of successive mortality rates, $m_{x,t}/m_{x,t-1}=C$ for all $x$ (since only $k_t$ moves), which does not hold empirically.
- There is **no cohort effect**: the model cannot capture that people born in the same year may share mortality experience as they age together.

### Cohort effect and the Renshaw-Haberman extension
A **cohort effect** is a shared mortality pattern attributable to year of birth (e.g. wartime nutrition, smoking prevalence of a generation). The Lee-Carter model is extended to include it as
$$
\ln(m_{x,t}) = a_x + b_x k_t + \gamma_{t-x},
$$
where $t-x$ is the birth year of an individual aged $x$ in year $t$, and $\gamma_{t-x}$ is that cohort's effect.

### Spline-based forecasting
A **spline** is a piecewise polynomial with continuity conditions imposed at the join points (**knots**). A natural cubic spline basis has the form
$$
f(x) = \alpha_0+\alpha_1 x + \sum_{j=1}^n \beta_j \phi_j(x), \qquad \phi_j(x)=\begin{cases}0 & x<x_j\\ (x-x_j)^3 & x\geq x_j\end{cases},
$$
which is continuous up to the second derivative at each knot $x_j$. A spline can replace a rigid parametric age-shape (e.g. the linear $\ln(\mu_x)=\alpha+\beta x$ of [[Gompertz' Law]]) with a more flexible one, either:
- **by year**, fitting $\ln(m_{x,t}) = \sum_{j=1}^s \theta_j B_j(t)$ separately for each age and evaluating the basis functions $B_j$ at future years $t_1^\star,\dots,t_m^\star$ to forecast; or
- **combined with Lee-Carter**, replacing the single term $b_x k_t$ with a flexible sum $\sum_{j=1}^J k_{t,j} b_j(x)$, giving $\ln(m_{x,t}) = a_x + \sum_{j=1}^J k_{t,j} b_j(x)$ — using all the data jointly across ages, as in Lee-Carter, while allowing a richer age-interaction than a single $b_x$.

### Alternative (simpler) models
A model with fewer parameters than Lee-Carter, assuming the age effect is **linear**:
$$
\ln(m_{x,t}) = k_t^1 + k_t^2(x-\bar x),
$$
where $k_t^1$ is a level term and $k_t^2$ a slope term (both indexed by year), and $\bar x$ is a reference age. This trades flexibility for parsimony relative to Lee-Carter's freely-estimated $b_x$.

### Sources of error in mortality forecasts
Even given a correctly specified model, forecasts carry several distinct sources of uncertainty:
1. **Prediction/process error**: the intrinsic variability in the data (deaths are a random count, not a deterministic function of the rate) is not fully accounted for.
2. **Parameter error**: the fitted $\hat a_x,\hat b_x,\hat k_t$ are themselves estimates subject to sampling variability, which can be quantified via bootstrap confidence intervals or a Bayesian credible interval.
3. **Model error**: the wrong structural model may have been chosen (e.g. true dynamics are age-period-cohort but Lee-Carter was fitted); addressed by fitting several candidate models and ranking them with a model-selection criterion such as AIC or BIC.
4. **Data error**: the data used for fitting may not be representative of the population being projected.

## See also
- [[Gompertz' Law]]
- [[Graduation of Mortality Rates]]
- [[Poisson Model for Mortality]]
- [[Multi-State Markov Model]]
- [[Two-State Model]]
