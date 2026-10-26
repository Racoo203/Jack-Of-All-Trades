---
title: "Force of Mortality and Actuarial Notation"
domain: Probability & Statistics
course: Survival Analysis
unit: "Chapter 1 - Concept of survival models"
level: MSc
status: drafted
confidence: 0
tags: [survival-analysis, actuarial-notation, force-of-mortality]
---
## Definition
Suppose an individual is alive at age $x$. Denote their remaining lifetime by $T_x$ (a random variable; $x$ is a fixed constant), and note $T = x + T_x$ for the lifetime-from-birth [[Lifetime Function|$T$]].

The survival function of $T_x$ is
$$
S_x(t) = P(T_x > t) = P(T > x+t \mid T > x) = \frac{P(T>x+t)}{P(T>x)} = \frac{S(x+t)}{S(x)}
$$
the probability that a person alive at $x$ survives $t$ further years. Its cdf is $F_x(t) = 1 - S_x(t)$, and its pdf is
$$
f_x(t) = \frac{dF_x(t)}{dt} = \frac{f(x+t)}{S(x)} = \frac{-dS_x(t)}{dt}
$$
The **hazard function** of $T_x$ (equivalently the hazard of $T$ evaluated at $x+t$) is
$$
h_x(t) = h(x+t) = \frac{f(x+t)}{S(x+t)} = \frac{f_x(t)}{S_x(t)} = -\frac{d\ln S_x(t)}{dt}
$$

## Properties
### Actuarial notation for $S_x, F_x$
$$
{}_tp_x = P(T_x > t) = S_x(t), \qquad {}_tq_x = P(T_x \leq t) = 1 - S_x(t) = F_x(t)
$$
By convention ${}_1p_x = p_x$ and ${}_1q_x = q_x$: the probability a life aged $x$ survives (resp. dies within) one year. $q_x$ (or ${}_tq_x$) is the **mortality rate**.

### The force of mortality $\mu_x$
The actuarial equivalent of the hazard rate is the **force of mortality**:
$$
\mu_{x+t} = \lim_{h\to0^+} \frac{1}{h}P(T \leq x+t+h \mid T > x+t) = \lim_{h\to0^+}\frac{1}{h}P(T_x \leq t+h \mid T_x > t)
$$
so $\mu_{x+t} = h_x(t) = h(x+t)$, and
$$
h_x(t) = \mu_{x+t} = -\frac{d\ln S_x(t)}{dt} = -\frac{d\ln({}_tp_x)}{dt}, \qquad {}_tp_x = S_x(t) = \exp\left(-\int_0^t \mu_{x+u}\,du\right)
$$

### Composition rule (Chapman–Kolmogorov for lifetimes)
For $u,t\geq0$,
$$
{}_{u+t}p_x = P(T_x > u+t) = P(T_x>u)P(T_{x+u}>t) = {}_up_x \cdot {}_tp_{x+u} = {}_tp_x\cdot {}_up_{x+t}
$$
i.e. surviving $u+t$ years from $x$ is equivalent to surviving $u$ years then $t$ more (in either order).

### Deferred mortality
The probability that a life aged $x$ dies between $u$ and $u+t$ years from now:
$$
{}_{u|t}q_x = P(u < T_x < u+t) = P(T_x>u) - P(T_x>u+t) = {}_up_x - {}_{u+t}p_x = F_x(u+t)-F_x(u) = {}_{u+t}q_x - {}_uq_x
$$

### Summary identities
$$
{}_tp_0 + {}_tq_0 = S(t)+F(t) = 1, \qquad {}_tp_x + {}_tq_x = S_x(t)+F_x(t) = 1
$$
$$
{}_{t+u}p_x = ({}_tp_x)({}_up_{x+t}) = ({}_up_x)({}_tp_{x+u})
$$

## Examples
Is ${}_5p_{34}$ or ${}_7p_{33}$ larger? The probability of surviving 33 to 40 must be less than or equal to surviving 34 to 39 (a strict subset of the required survival years plus one more year of risk), so ${}_5p_{34} > {}_7p_{33}$.

## See also
[[Lifetime Function]], [[Hazard Function]], [[Life Table]], [[Mean and Variance of Survival Time]]
