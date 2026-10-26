---
title: "Chi-Square Goodness-of-Fit Test for Randomness"
domain: "Optimization & Control"
course: "Stochastic Optimization"
level: BSc
status: seeding
confidence: 0
tags: [simulation, pseudorandom-numbers, hypothesis-testing, stochastic-optimization]
---
## Definition
The **chi-square goodness-of-fit test**, applied to a [[Pseudorandom Number Generator|generator]]'s output $X_1,\dots,X_n$, tests whether the sample was actually drawn from a hypothesized distribution $F_0$ against the alternative that it wasn't:
$$
H_0: F_X(x) = F_0(x) \qquad \text{vs.} \qquad H_1: F_X(x) \ne F_0(x).
$$
For validating a PRNG, $F_0 = U(0,1)$. The support is partitioned into $k$ disjoint subsets (bins) $I_1,\dots,I_k$; with $f_i$ the observed count in bin $i$ and $e_i$ the count expected under $H_0$, the test statistic
$$
\chi^2 = \sum_{i=1}^k \frac{(f_i - e_i)^2}{e_i}
$$
is compared against a $\chi^2$ distribution (asymptotically, as $n\to\infty$) with the appropriate degrees of freedom.

<!-- UNVERIFIED: check against course slides/exercises — the slides state the test statistic's asymptotic chi-square distribution and its bin-count setup but do not work a full numeric example or specify the degrees-of-freedom convention used (k-1 vs. k-1-(estimated parameters)) in this course. -->

## Properties
### A weak test: good for rejection, not for acceptance
The course explicitly flags this as a **low-power** goodness-of-fit test: it can justify *rejecting* $H_0$, but provides comparatively weak support for *accepting* it — a non-significant result should not be over-interpreted as proof the generator is good, only as an absence of evidence against it.

### Extends to multi-dimensional uniformity
The same chi-square construction, applied to $s$-tuples built by grouping consecutive draws,
$$
X_1 = (u_1,\dots,u_s),\quad X_2=(u_{s+1},\dots,u_{2s}),\ \dots,\quad X_n = (u_{(n-1)s+1},\dots,u_{ns}),
$$
tests $s$-dimensional uniformity over the hypercube $F_0 = U([0,1]^s)$ — i.e. it can also detect serial correlation between successive draws (the generator's second defining requirement, alongside marginal uniformity — see [[Pseudorandom Number Generator]]), not just marginal non-uniformity.

## See also
[[Pseudorandom Number Generator]], [[Linear Congruential Generator]]
