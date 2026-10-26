---
title: "Accelerated Failure Time Model"
domain: Probability & Statistics
course: Survival Analysis
unit: "PGT Lectures"
level: MSc
status: drafted
confidence: 0
tags: [survival-analysis, aft-model, parametric-model, pgt-extension]
---
## Definition
The [[Proportional Hazards Model|proportional hazards (PH) assumption]] states that covariates act **multiplicatively on the hazard**. The **accelerated failure time (AFT)** assumption instead states that covariates act **multiplicatively on the survival time itself**: covariates "stretch" or "compress" the time axis. Comparing two groups with survival functions $S_1,S_2$, the AFT assumption is
$$
S_2(t) = S_1(\gamma t), \qquad \gamma>0 \text{ the acceleration factor},
$$
i.e. living to time $t$ in group 2 is equivalent to living to time $\gamma t$ in group 1. Equivalently, for the underlying lifetimes, $T_1 = \gamma T_2$ (a pure time-rescaling), since
$$
S_1(t) = P(T_1\le t) = P(\gamma T_2 \le t) = P\Big(T_2 \le \tfrac{t}{\gamma}\Big) = S_2\Big(\tfrac{t}{\gamma}\Big).
$$

**Dog-year analogy.** If a 10-year-old dog is "equivalent" to a 70-year-old human, and a 6-year-old dog to a 42-year-old human ($42 = 6\times 7$), then $S_{\text{dogs}}(t) = S_{\text{human}}(7t)$ — a constant acceleration factor of 7 applied to time itself, exactly the AFT structure.

### General log-linear form
Writing $\gamma = e^{-\alpha}$ (parametrised through a linear predictor), $T_1=\gamma T_2 \iff \log T_1 = \alpha + \log T_2$, so more generally an AFT model assumes covariates act **additively on log-survival time**:
$$
\log T = X\beta + \sigma\epsilon,
$$
where $\epsilon$ follows some standard error distribution and $\sigma$ is a scale parameter. Different choices of the error distribution for $\epsilon$ generate different parametric AFT models.

## Properties

### Exponential AFT model
Take the [[Parametric Survival Models|exponential model]] $S(t)=e^{-\lambda t}$ and set $\lambda = e^{X\beta}$: this is the exponential AFT model. It can equivalently be derived from $\log T = X\beta + \epsilon$ (i.e. $\sigma=1$) with $\epsilon$ following a **Gumbel distribution** with survival function $S_\epsilon(s) = e^{-e^{s}}$. Indeed:
$$
S(t) = P(T\ge t) = P(\log T \ge \log t) = P(X\beta+\epsilon \ge \log t) = P\big(\epsilon \ge \log t - X\beta\big) = e^{-e^{\log t - X\beta}} = e^{-t\,e^{-X\beta}},
$$
which is exponential with rate $\lambda = e^{-X\beta}$ (up to sign convention on $\beta$), confirming the AFT/Gumbel-error equivalence.

**The exponential model is both PH and AFT.** For two groups with $S_1(t)=e^{-\lambda_1 t}$, $S_2(t)=e^{-\lambda_2 t}$: setting $\gamma=\lambda_1/\lambda_2$ gives $S_1(t) = S_2(\gamma t)$ (AFT holds), while the hazards $h_1(t)=\lambda_1,\ h_2(t)=\lambda_2$ have constant ratio $h_1(t)/h_2(t)=\lambda_1/\lambda_2=C$ (PH also holds). This double membership is special to the (constant-hazard) exponential model.

### Weibull AFT model
Take the Weibull survival function $S(t)=e^{-\lambda t^\alpha}$ and set $\lambda=e^{X\beta}$: the Weibull AFT model. One can check directly that $S_1(t) = S_2(\gamma t)$ for a suitable $\gamma$, so the Weibull model satisfies AFT — but **only when the shape parameter is shared across groups**.

**Proof that the Weibull model requires a common shape parameter to be AFT.** Let $S_1(t)=e^{-\lambda_1 t^{p_1}}$, $S_2(t)=e^{-\lambda_2 t^{p_2}}$. If AFT holds, there is $\gamma$ with $S_1(t)=S_2(\gamma t)$, i.e.
$$
e^{-\lambda_1 t^{p_1}} = e^{-\lambda_2 (\gamma t)^{p_2}} \iff \lambda_1 t^{p_1} = \lambda_2\gamma^{p_2} t^{p_2}.
$$
For this identity to hold for **all** $t$, the powers of $t$ must match, forcing $p_1=p_2$.

**AFT $\iff$ PH duality for Weibull.** If $p_1=p_2=p$, the hazards are $h_1(t)=\lambda_1 p\,t^{p-1}$, $h_2(t)=\lambda_2 p\,t^{p-1}$, giving a constant ratio $h_1(t)/h_2(t)=\lambda_1/\lambda_2$ — so when the Weibull model is AFT it is automatically also PH, and vice versa (this converse holds specifically because both families are indexed by the same $(\lambda,p)$ structure).

| | Exponential | Weibull (common shape) | Weibull (different shape) | Log-logistic |
|---|---|---|---|---|
| AFT? | Yes | Yes | No | Yes |
| PH? | Yes | Yes | No | No |

**Checking the AFT assumption (Weibull).** From $S(t)=e^{-\lambda t^p}$, taking the log twice: $\log(-\log S(t)) = p\log(t) + \log\lambda$. Plotting $\log(-\log\hat S(t))$ (from the [[Kaplan-Meier estimate|Kaplan-Meier estimate]]) against $\log(t)$ for each group: a straight line supports the Weibull assumption; **parallel** lines (equal slope $p$) additionally support AFT; a slope of $p=1$ supports the simpler exponential model.

### Log-logistic model
The log-logistic distribution has hazard and survival functions
$$
h(t) = \frac{\lambda p t^{p-1}}{1+\lambda t^p}, \qquad S(t) = \frac{1}{1+\lambda t^p}.
$$
An AFT model is defined by setting $\lambda=e^{X\beta}$. It arises from $\log T = X\beta+\sigma\epsilon$ when $\epsilon$ follows a **logistic distribution** with survival function $S_\epsilon(s)=\frac{1}{1+e^{s}}$:
$$
S(t) = P(X\beta+\epsilon\ge \log t) = P\big(\epsilon \ge \log t - X\beta\big) = \frac{1}{1+e^{(\log t - X\beta)/\sigma}} = \frac{1}{1+t^{1/\sigma}e^{-X\beta/\sigma}},
$$
matching the log-logistic form with $p=1/\sigma$.

**The log-logistic model is AFT but *not* PH.** Writing $h_1(t) = \frac{\lambda_1 p t^{p-1}}{1+\lambda_1 t^p}$, $h_2(t)=\frac{\lambda_2 p t^{p-1}}{1+\lambda_2 t^p}$, no choice of $\lambda_1,\lambda_2$ makes $h_1(t)/h_2(t)$ constant in $t$ (the $t^p$ term in the denominators does not cancel) — yet the AFT relation $S_1(t)=S_2(\gamma t)$ holds exactly by construction.

**Checking the AFT assumption (log-logistic).** From $S(t)=1/(1+\lambda t^p)$, rearrange to $\frac{1-S(t)}{S(t)}=\lambda t^p$, so
$$
\log\!\left(\frac{1-S(t)}{S(t)}\right) = \log\lambda + p\log t.
$$
Plotting $\log\!\big(\frac{1-\hat S(t)}{\hat S(t)}\big)$ against $\log t$ per group: linearity supports the log-logistic assumption, and parallel lines (equal $p$) additionally support AFT.

### Checking the proportional hazards assumption
The PH assumption implies $S(t|X) = S_0(t)^{e^{X\beta}}$, so taking the log twice:
$$
\log(-\log S(t|X)) = \log(-\log S_0(t)) + X\beta.
$$
Plotting $\log(-\log \hat S(t))$ (Kaplan-Meier, by covariate group) against $t$ (or $\log t$): **parallel** curves support the PH assumption; curves that cross or converge/diverge over time (e.g. an implantable cardioverter defibrillator giving strong short-term protection that fades as other health complications accumulate) indicate it is violated.

## See also
- [[Proportional Hazards Model]]
- [[Cox Proportional Hazards Model]]
- [[Kaplan-Meier estimate]]
- [[Parametric Survival Models]]
- [[Time-Varying Covariates and Stratified Cox Models]]
