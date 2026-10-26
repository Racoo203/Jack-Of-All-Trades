---
title: "Gompertz' Law"
domain: Probability & Statistics
course: Survival Analysis
unit: "Chapter 3 - Curtate future lifetime, laws of mortality"
level: MSc
status: drafted
confidence: 0
tags: [survival-analysis, gompertz, laws-of-mortality]
---
## Definition
**Laws of mortality** are simple parametric equations describing the [[Force of Mortality and Actuarial Notation|force of mortality]] experienced by a population. **Gompertz' law** (1825) is
$$
\mu_x = Bc^x, \qquad B>0,\; c>0
$$
Mortality grows exponentially with age, which is reasonable for middle and older ages (roughly 30–80 years). **Makeham's law** (1860) adds an age-independent constant, e.g. to account for accident risk:
$$
\mu_x = A + Bc^x, \qquad A>0,\;B>0,\;c>0
$$

## Properties
### Survival function under Gompertz' law
**Claim.** Under $\mu_x = Bc^x$, the survival function of $T_x$ is
$$
S_x(t) = \exp\left(-\frac{B}{\ln c}c^x(c^t-1)\right)
$$
and the pdf is $f_x(t) = Bc^{x+t}\exp\left(-\frac{B}{\ln c}c^x(c^t-1)\right)$.

**Proof.** From [[Force of Mortality and Actuarial Notation]], $S_x(t) = \exp\left(-\int_0^t \mu_{x+u}\,du\right)$. Substituting $\mu_{x+u}=Bc^{x+u}$ and using $c^u = \exp(u\ln c)$, $\int c^u\,du = c^u/\ln c$:
$$
S_x(t) = \exp\left(-\int_0^t Bc^{x+u}\,du\right) = \exp\left(-Bc^x\int_0^t \exp(u\ln c)\,du\right) = \exp\left(-\frac{B}{\ln c}c^x(c^t-1)\right)
$$
Differentiating $S_x(t)$ with respect to $t$ and negating (or equivalently $f_x(t)=h_x(t)S_x(t)=\mu_{x+t}S_x(t)$):
$$
f_x(t) = -\frac{\partial S_x(t)}{\partial t} = \frac{Bc^x}{\ln c}\cdot c^t\ln c\cdot\exp\left(-\frac{B}{\ln c}c^x(c^t-1)\right) = Bc^{x+t}\exp\left(-\frac{B}{\ln c}c^x(c^t-1)\right)
$$

### Makeham's survival function
Confirmed against Exercises & Solutions (Ch. 3, Q3): by the same integration, under $\mu_x = A+Bc^x$:
$$
S_x(t) = \exp\left(-At - \frac{B}{\ln c}c^x(c^t-1)\right)
$$
since $\int_0^t (A+Bc^{x+u})\,du = At + \frac{B}{\ln c}c^x(c^t-1)$.

## See also
[[Force of Mortality and Actuarial Notation]], [[Parametric Survival Models]], [[Graduation of Mortality Rates]]
