---
title: "Pseudorandom Number Generator"
domain: "Optimization & Control"
course: "Stochastic Optimization"
level: BSc
status: drafted
confidence: 0
tags: [simulation, pseudorandom-numbers, stochastic-optimization]
---
## Definition
A **pseudorandom number generator (PRNG)** is a deterministic mathematical procedure that, from a starting **seed**, produces a sequence of numbers that behaves *as if* it were drawn independently from a $U(0,1)$ distribution — strictly, the notion of a single "random number" is not meaningful; what is generated is a **sequence** (series) of numbers, and it is the sequence's statistical behavior that is judged. Two working definitions from computational theory: a sequence is random if it cannot be reproduced more compactly than by the sequence itself, and a sequence is random if no observer with reasonable computational resources can distinguish it from a truly random sequence better than by chance.

Random-number generation plays a foundational role in simulation: it supplies the "seeds" from which samples of any random variable are built (see [[Monte Carlo Method]], [[Inverse Transform Sampling]]).

## Properties
### Two defining requirements
A PRNG must satisfy:
1. **Uniform distribution**: every number in the range of interest is equally likely to be drawn.
2. **No serial correlation**: the appearance of one number in the sequence does not affect the probability of any other (or the same) number appearing next.
The sequence $1,2,3,4,5,1,2,3,4,5,\dots$ illustrates the distinction: it is uniform (each digit appears equally often) but obviously correlated, and hence not acceptable as pseudorandom.

### Desirable engineering properties
Beyond the two statistical requirements, a good generator should also be: statistically independent, have a long period (doesn't repeat too soon), be reproducible (repeatable from the same seed) yet mutable (different seeds give different sequences), simple to implement, portable, fast, and low in memory use.

### Generation mechanisms
Three families of mechanisms have historically been used: **tables** (e.g. the RAND table of 1955, 100,000 numbers from electronic noise), **physical phenomena** (electronic white noise, particle-emission counts, coin flips, roulette wheels), and **mathematical procedures** — algorithms that, given a seed, generate successors via a deterministic function. This course's generators ([[Mid-Square Method]], [[Mid-Product Method]], [[Linear Congruential Generator]], [[Multiplicative Congruential Generator]]) are all of the mathematical-procedure type.

### Streams
A generator that starts from the same seed always reproduces the same **stream** (torrente) of numbers; different seeds give different streams. If seeds are chosen far apart in the generator's own cycle, the resulting streams behave as statistically independent of one another — useful for generating independent samples of several random variables in the same simulation.

### Validation
A generator's output must be validated against its two defining statistical properties (uniformity and lack of serial correlation) before it is trusted — see [[Chi-Square Goodness-of-Fit Test for Randomness]]. These validation tests are generic: the same tests apply whether validating the raw uniform generator, a derived random-variable generator, or the inputs to a simulation model.

## See also
[[Mid-Square Method]], [[Mid-Product Method]], [[Linear Congruential Generator]], [[Multiplicative Congruential Generator]], [[Chi-Square Goodness-of-Fit Test for Randomness]], [[Monte Carlo Method]]
