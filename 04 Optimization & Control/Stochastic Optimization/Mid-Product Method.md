---
title: "Mid-Product Method"
domain: "Optimization & Control"
course: "Stochastic Optimization"
level: BSc
status: drafted
confidence: 0
tags: [simulation, pseudorandom-numbers, stochastic-optimization]
---
## Definition
The **mid-product method** is a non-congruential [[Pseudorandom Number Generator]] closely related to the [[Mid-Square Method]]: instead of squaring a single seed, it requires **two** seeds $R_0, R_1$, multiplies consecutive terms, and takes the middle digits of the product as the next term: $R_{n+2} = \text{mid-digits}(R_n \cdot R_{n+1})$.

A simplified variant replaces the second running seed with a fixed constant multiplier $K$: $R_{n+1} = K \cdot R_n$ (taking middle digits as usual) — structurally similar to the [[Multiplicative Congruential Generator]] but without an explicit modulus step.

## Properties
### Worked example and degeneration
Starting from $R_0=151, R_1=155$: $R_0 \cdot R_1 = 23{,}405$, middle digits $\Rightarrow R_2 = 340$; continuing the recursion, the example sequence runs $340, 270, 180, 860, 548, 712, 901, 415, 739, 668, 936, 252, 358, 21, 51, 7, 5, 0,\dots$ — again collapsing to $0$, this time after about 18 steps.

### Comparison with the Mid-Square Method
Both methods share the same failure mode (degeneration to a fixed point, typically $0$), but the mid-product and constant-multiplier variants tend to have **longer periods** than the mid-square method and produce sequences that look more uniformly distributed — while still being unsuitable for the volume of pseudorandom numbers a simulation model typically needs, which is why the course moves on to the [[Linear Congruential Generator|congruential generators]].

## See also
[[Pseudorandom Number Generator]], [[Mid-Square Method]], [[Multiplicative Congruential Generator]]
