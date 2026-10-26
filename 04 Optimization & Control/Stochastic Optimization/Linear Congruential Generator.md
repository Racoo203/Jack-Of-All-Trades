---
title: "Linear Congruential Generator"
domain: "Optimization & Control"
course: "Stochastic Optimization"
level: BSc
status: drafted
confidence: 0
tags: [simulation, pseudorandom-numbers, stochastic-optimization]
---
## Definition
The **linear congruential generator** (LCG; "método congruencial mixto/lineal") is the workhorse congruential [[Pseudorandom Number Generator]]: each term is generated directly from the previous one by
$$
X_{n+1} = (aX_n + c) \bmod m,
$$
with seed $X_0 > 0$, multiplier $a > 0$, additive constant $c > 0$, and modulus $m > X_0, a, c$. To obtain approximate $U(0,1)$ draws, normalize: $U_n = X_n / m$. An equivalent closed form (useful for jumping ahead without iterating) is
$$
X_n = \left[a^n X_0 + c\,\frac{a^n - 1}{a - 1}\right] \bmod m, \qquad X_{n+k} = \left[a^n X_k + c\,\frac{a^n-1}{a-1}\right]\bmod m.
$$

## Properties
### Advantages
Uses little memory, is very fast, and the same stream can always be reproduced by storing only the seed $X_0$.

### Period depends critically on the parameters
If a value repeats, the entire sequence from that point repeats — so the sequence's **period** is at most $m$, but a badly chosen $(a,c,X_0,m)$ can give a period far shorter than $m$. Worked contrast: with $a=7, c=9, X_0=5, m=11$ the period is $10$ (out of a possible $m=11$) — acceptable; with $a=X_0=c=7, m=10$ the period collapses to just $4$ — unacceptable.

### Full-period selection rules
To guarantee the maximum possible period $m$, the parameters should be chosen as:
- **Modulus $m$**: either random, or (preferred) the largest prime less than $p^d - 1$, where $p$ is the computer's number base and $d$ its word length in bits (e.g. a 16-bit binary machine has $p=2, d=16$).
- **Multiplier $a$**: an odd integer, not divisible by 3 or 5, and satisfying $(a-1) \bmod 4 = 0$ if 4 divides $m$, or $(a-1)\bmod b = 0$ for every prime factor $b$ of $m$. In binary systems, $a = 2^k+1$ with $k \ge 2$ is a common choice.
- **Additive constant $c$**: any value satisfying $c \bmod 8 = 5$, which forces $c$ to be odd and relatively prime to $m$.
- **Seed $X_0$**: essentially irrelevant to the statistical properties of the resulting sequence — any valid starting value works equally well.

## See also
[[Pseudorandom Number Generator]], [[Multiplicative Congruential Generator]], [[Chi-Square Goodness-of-Fit Test for Randomness]]
