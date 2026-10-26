---
title: "European Options"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "Chapter 4 - Financial Markets"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, options]
---
## Definition
A **European option** ([[Call option|call]] or [[Put option|put]]) may be exercised **only at the prescribed exercise/expiry date $T$**, not before. This is the style assumed by default throughout most of the course (e.g. the [[Black-Scholes formula]] prices European options); contrast with [[American Options]].

## Properties
### Why "European" pricing is easier
Because exercise can only happen at $T$, the value of a European option is entirely determined by the terminal distribution of $S_T$ (see [[Terminal Share Price Distribution]]) and the payoff function — no path-dependent early-exercise decision needs to be modelled. This is what allows a clean closed-form solution such as the [[Black-Scholes formula]].

### Put-call parity
For European options on a non-dividend-paying stock:
$$
c_t + Ke^{-r(T-t)} = p_t + S_t
$$
— see [[Put-call parity]] for the full replication proof.

## See also
[[Call option]], [[Put option]], [[American Options]], [[Put-call parity]], [[Black-Scholes formula]]
