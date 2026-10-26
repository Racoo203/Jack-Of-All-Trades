---
title: "Life Table"
domain: Probability & Statistics
course: Survival Analysis
unit: "Chapter 2 - Lifetime after age x and lifetable"
level: MSc
status: drafted
confidence: 0
tags: [survival-analysis, life-table, actuarial-notation]
---
## Definition
A **life table** shows the expected number of survivors to each age in a hypothetical group of lives, and is used to derive probabilities/expectations for a population. Let $x_0$ be the first age recorded and $\omega$ the last (oldest) age. Define:
- $l_x$: the (expected) number of lives at age $x$ ($x_0 \leq x \leq \omega$)
- $d_x$: the (expected) number of deaths between ages $x$ and $x+1$, so $d_x = l_x - l_{x+1}$
- $l_{x_0}$: the **radix** of the table

The expected number of lives surviving a further $x$ years from $x_0$ is $l_{x_0+x} = l_{x_0}S(x) = l_{x_0}\cdot{}_xp_{x_0}$; taking $x_0=0$ (birth), $l_1 = l_0 p_0$, $l_2 = l_0\cdot {}_2p_0$, etc.

## Properties
### General relationships
For age $x$ and $t$ further years, using [[Force of Mortality and Actuarial Notation|actuarial notation]]:
$$
l_{x+t} = l_x \cdot {}_tp_x, \qquad {}_td_x = l_x - l_{x+t}, \qquad {}_tq_x = \frac{{}_td_x}{l_x} = 1-\frac{l_{x+t}}{l_x}, \qquad {}_tp_x = \frac{l_{x+t}}{l_x}
$$
For $t=1$: $l_{x+1}=l_x p_x$, $d_x = l_x - l_{x+1} = l_x q_x$, $q_x = d_x/l_x$, $p_x = l_{x+1}/l_x$.

### Methodology of constructing a life table
Start with a radix $l_0$ (conventionally 100,000 simultaneous births). Then iteratively:
$$
d_x = q_x l_x, \qquad l_{x+1} = l_x - d_x
$$
using known or assumed mortality rates $q_x$ at each age.

### Non-integer ages and the [[Uniform Distribution of Deaths (UDD)|UDD assumption]]
When $t$ is not an integer, computing ${}_tp_x$ or ${}_tq_x$ requires an assumption on how deaths are distributed within the year of age; the standard choice is the **uniform distribution of deaths (UDD)** assumption, under which $l_{x+t} = (1-t)l_x + tl_{x+1}$ by linear interpolation — see [[Uniform Distribution of Deaths (UDD)]] for the resulting identity ${}_tq_x = tq_x$.

### Expectation of life at age $x$
Recall from [[Mean and Variance of Survival Time]] that $\overset{\circ}{e}_x = \mathbb{E}(T_x) = \int_0^\infty S_x(u)\,du = \int_0^\infty {}_up_x\,du$. Splitting the integral into unit intervals and applying the trapezoidal rule under UDD:
$$
\overset{\circ}{e}_x = \int_0^\infty {}_up_x\,du = \sum_{t=0}^\infty \int_t^{t+1} {}_up_x\,du \approx \sum_{t=0}^\infty \frac{1}{2}({}_tp_x + {}_{t+1}p_x)
$$
$$
= \sum_{t=0}^\infty \frac{1}{2}\left(\frac{l_{x+t}}{l_x} + \frac{l_{x+t+1}}{l_x}\right) = \sum_{t=0}^\infty \frac{\frac{1}{2}(l_{x+t}+l_{x+t+1})}{l_x} = \frac{\sum_{t=0}^\infty L_{x+t}}{l_x} = \frac{T_x}{l_x}
$$
where $L_{x+t} = (l_{x+t}+l_{x+t+1})/2$ is the years lived between ages $x+t$ and $x+t+1$, and $T_x = \sum_{t=0}^{\omega-x} L_{x+t}$ is the total years lived from age $x$ onward. This construction is used to fill life-table columns $L_x, T_x, \overset{\circ}{e}_x$ from $l_x$.

## Examples
Given $l_{58}=88792$, $l_{59}=87805$ and UDD, $d_{58}=987$, so a quarter-year of deaths is $987/4=246.75$ and $l_{58.25} = 88792-246.75 = 88545.25$.

## See also
[[Force of Mortality and Actuarial Notation]], [[Uniform Distribution of Deaths (UDD)]], [[Curtate Future Lifetime]], [[Mean and Variance of Survival Time]]
