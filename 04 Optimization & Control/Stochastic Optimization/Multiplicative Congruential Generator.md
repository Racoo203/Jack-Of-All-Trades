---
title: "Multiplicative Congruential Generator"
domain: "Optimization & Control"
course: "Stochastic Optimization"
level: BSc
status: drafted
confidence: 0
tags: [simulation, pseudorandom-numbers, stochastic-optimization]
---
## Definition
The **multiplicative congruential generator** (MCG) is the special case of the [[Linear Congruential Generator]] with additive constant $c=0$:
$$
X_{n+1} = a X_n \bmod m.
$$
As with the LCG, the parameters $a, X_0, m$ must be chosen carefully to guarantee a maximal period.

## Properties
### Full-period selection rules (binary systems)
- $X_0$ must be an odd integer, relatively prime to $m$.
- $a$ must have the form $a = 8t \pm 3$ for some integer $t$.
- $m$ is taken as $m = 2^d$; the resulting maximum period is $2^{d-2} = m/4$ (note: strictly less than $m$, unlike a well-tuned LCG, because $c=0$ removes one degree of freedom from the period-maximizing conditions).

### Worked example
With $a=5, X_0=5, m=32$: the sequence $5, 25, 29, 17, 21, 9, 13, 1, 5, 25, 29,\dots$ has period $8 = 32/4$, matching the theoretical maximum $m/4$ exactly.

| $n$ | $X_n$ | $aX_n$ | $aX_n \bmod m$ |
|---|---|---|---|
| 0 | 5 | 25 | 25 |
| 1 | 25 | 125 | 29 |
| 2 | 29 | 145 | 17 |
| 3 | 17 | 85 | 21 |
| 4 | 21 | 105 | 9 |
| 5 | 9 | 45 | 13 |
| 6 | 13 | 65 | 1 |
| 7 | 1 | 5 | 5 |
| 8 | 5 | 25 | 25 |

### A commercial generator
The IMSL library's multiplicative congruential generator uses $m = 2^{31}-1$ with any of the multipliers $a \in \{16807,\ 397204094,\ 950706376\}$ — cited as an example of production-quality parameter choices satisfying the full-period rules above.

## See also
[[Linear Congruential Generator]], [[Pseudorandom Number Generator]]
