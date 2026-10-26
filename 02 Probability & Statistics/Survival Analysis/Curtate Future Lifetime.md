---
title: "Curtate Future Lifetime"
domain: Probability & Statistics
course: Survival Analysis
unit: "Chapter 2 - Lifetime after age x and lifetable"
level: MSc
status: drafted
confidence: 0
tags: [survival-analysis, curtate-lifetime, expectation-of-life]
---
## Definition
The **curtate future lifetime** of a person aged $x$ is the number of complete integer years lived after age $x$:
$$
K_x = \lfloor T_x \rfloor
$$
where $T_x$ is the (complete) [[Force of Mortality and Actuarial Notation|future lifetime]] and $\lfloor\cdot\rfloor$ denotes rounding down. E.g. if $T_{20}=45.3$ then $K_{20}=\lfloor 45.3\rfloor = 45$.

$K_x$ is a discrete random variable taking values $0,1,2,\dots$, with pmf
$$
P(K_x=k) = P(k\leq T_x < k+1) = {}_{k|1}q_x = {}_kp_x - {}_{k+1}p_x = {}_kp_x\,q_{x+k}
$$

## Properties
### Curtate expectation of life
$$
e_x = \mathbb{E}(K_x) = \sum_{k=0}^\infty k\,P(K_x=k) = \sum_{k=0}^\infty k({}_kp_x - {}_{k+1}p_x)
$$
Expanding by summation by parts (telescoping):
$$
e_x = ({}_1p_x-{}_2p_x)+2({}_2p_x-{}_3p_x)+3({}_3p_x-{}_4p_x)+\cdots = {}_1p_x+{}_2p_x+{}_3p_x+\cdots = \sum_{k=1}^\infty {}_kp_x
$$
Also $\mathbb{E}(K_x^2) = 2\sum_{k=1}^\infty k\cdot{}_kp_x - e_x$.

### Relation between complete and curtate expectation of life
**Proposition.** $\overset{\circ}{e}_x \approx e_x + \tfrac{1}{2}$: the complete expectation of life at age $x$ is approximately the curtate expectation plus half a year.

**Proof.** From [[Life Table]],
$$
\overset{\circ}{e}_x = \int_0^\infty {}_tp_x\,dt = \sum_{t=0}^\infty\int_t^{t+1}{}_up_x\,du \approx \sum_{t=0}^\infty \frac{1}{2}({}_tp_x+{}_{t+1}p_x) \quad\text{(trapezoidal rule, UDD)}
$$
$$
= \frac{1}{2}\,{}_0p_x + \sum_{t=1}^\infty {}_tp_x = \frac{1}{2}+e_x
$$
since ${}_0p_x=1$.

## Examples
A man with a terminal disease has survival probabilities $p_x=0.8$, ${}_2p_x=0.4$, ${}_3p_x=0.1$, ${}_kp_x=0$ for $k\geq4$. His curtate expectation of life is
$$
e_x = \sum_{k=1}^\infty {}_kp_x = 0.8+0.4+0.1 = 1.3 \text{ years}
$$

Given $F_x(t) = \dfrac{t}{100-x}$ for $0\leq x+t<100$ (so ${}_tp_x = 1-\dfrac{t}{100-x}$), the complete expectation of life at $x=20$:
$$
\overset{\circ}{e}_{20} = \int_0^{100-x}\left(1-\frac{t}{100-x}\right)dt = (100-x) - \frac{(100-x)^2}{2(100-x)} = \frac{100-x}{2} = \frac{80}{2}=40
$$
so $\overset{\circ}{e}_{20}=40$, and $e_{20}\approx 40-0.5=39.5$.

## See also
[[Life Table]], [[Mean and Variance of Survival Time]], [[Force of Mortality and Actuarial Notation]]
