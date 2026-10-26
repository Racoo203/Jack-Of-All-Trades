---
title: "Hazard Function"
domain: Probability & Statistics
course: Survival Analysis
unit: "Chapter 1 - Concept of survival models"
level: MSc
status: drafted
confidence: 0
tags: [survival-analysis, hazard-function]
---
## Definition
The **hazard function** (hazard rate, or **force of mortality** in actuarial science) is defined as
$$
h(t) = \lim_{\Delta t \to 0} \frac{P(t \leq T < t + \Delta t \mid T \geq t)}{\Delta t}
$$
For small $\Delta t$, $h(t)\Delta t \approx P(t \leq T < t+\Delta t \mid T \geq t)$: the (approximate) probability of the event occurring in $[t, t+\Delta t)$ given survival to $t$, with $h(t)$ the constant of proportionality.

The **cumulative hazard function** is
$$
H(t) = \int_0^t h(u)\,du
$$

## Properties
### Relation to $f(t), F(t), S(t)$
Starting from the definition and using $P(T \geq t) = S(t)$ (continuity of $T$ makes $P(T\geq t)=P(T>t)$):
$$
h(t) = \lim_{\Delta t \to 0} \frac{P(t \leq T < t+\Delta t)}{P(T\geq t)\Delta t} = \lim_{\Delta t \to 0}\frac{F(t+\Delta t) - F(t)}{S(t)\Delta t} = \frac{f(t)}{S(t)}
$$
Since $S(t) = 1-F(t) \implies \dfrac{dS(t)}{dt} = -\dfrac{dF(t)}{dt} \implies f(t) = -\dfrac{dS(t)}{dt}$, substituting gives
$$
h(t) = -\frac{S'(t)}{S(t)} = -\frac{d\ln S(t)}{dt}
$$

### Survival function in terms of the hazard
Integrating the previous identity,
$$
H(t) = \int_0^t h(u)\,du = -\ln S(t) \quad\Longrightarrow\quad S(t) = \exp(-H(t)) = \exp\left(-\int_0^t h(u)\,du\right)
$$

### Why model the hazard rather than the density
The hazard gives a more direct representation of instantaneous risk, and is easier to specify: modelling $h$ only requires $h(t) > 0$, whereas modelling $f$ requires $f(t) > 0$ and $\int f(t)\,dt = 1$.

## See also
[[Lifetime Function]], [[Force of Mortality and Actuarial Notation]], [[Parametric Survival Models]]
