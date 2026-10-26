---
title: "Mid-Square Method"
domain: "Optimization & Control"
course: "Stochastic Optimization"
level: BSc
status: drafted
confidence: 0
tags: [simulation, pseudorandom-numbers, stochastic-optimization]
---
## Definition
The **mid-square method** (proposed by Von Neumann and Metropolis in 1946) is a non-congruential [[Pseudorandom Number Generator]]: given an $n$-digit seed, square it and take the $n$ middle digits of the (up to $2n$-digit) result as the next number in the sequence.

## Properties
### Worked example
Starting from seed $R_0 = 154$ (3 digits), squaring gives $R_0^2 = 23{,}716$; padding/aligning to 6 digits and taking the middle digits yields $R_1 = 371$. Iterating:

| $n$ | $R(n)$ | $R(n)^2$ | middle digits |
|---|---|---|---|
| 0 | 154 | 23,716 | 371 |
| 1 | 371 | 137,641 | 764 |
| 2 | 764 | ... | ... |
| ... | ... | ... | ... |
| 11 | 300 | 90,000 | 0 |
| 12 | 0 | 0 | 0 |

By step 12 the sequence has collapsed to a fixed point at 0 — a **degenerate** sequence.

### Rapid degeneration is the method's central flaw
Depending on the seed, the method can degenerate after as few as $\approx 20$ terms. For example, starting a 4-digit sequence at $R_i = 3500$: $R_i^2 = 12{,}250{,}000$, middle 4 digits $= 2500$; then $R_{i+1}=2500 \Rightarrow R_{i+1}^2 = 6{,}250{,}000$, middle digits again $2500$ — the sequence is already fixed at $2500$. Because of this, any implementation must actively check for degeneration rather than assume it away.

## See also
[[Pseudorandom Number Generator]], [[Mid-Product Method]]
