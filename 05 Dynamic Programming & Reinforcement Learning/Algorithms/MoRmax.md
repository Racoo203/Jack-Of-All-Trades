---
title: MoRmax
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
unit: Algorithms
level: MSc
status: seeding
confidence: 0
tags: [reinforcement-learning, algorithms, theory, pac-mdp, model-based]
---
## Definition
<!-- UNVERIFIED: check against Szita & Szepesvári (2010), "Model-based reinforcement learning with nearly tight exploration complexity bounds"; not covered in the MA338 slide decks -->
MoRmax ("Model-based or R-max") is a refinement of [[Algorithms/R-MAX|R-MAX]] achieving, at the time of its publication, the best known [[Sample Complexity of Exploration|PAC-MDP sample-complexity]] bound for tabular discounted MDPs — in particular a substantially better (near-tight, matching known lower bounds up to log factors) dependence on the accuracy parameter $1/\epsilon$ than R-MAX's original analysis.

## Properties
### The key technical improvement
Where R-MAX and standard [[Algorithms/Model-based Interval Estimation (MBIE)|MBIE]] analyses require the empirical model at *every* known state-action pair to be accurate to within $\epsilon$ (a strong, essentially per-transition condition), Szita & Szepesvári's analysis exploits a weaker sufficient condition: overall *value-function* accuracy is what actually matters for near-optimal behaviour, not pointwise transition-model accuracy everywhere. Exploiting this weaker requirement lets MoRmax use a smaller per-state-action visit threshold before declaring a pair "known", directly tightening the $1/\epsilon$-dependence of the resulting sample-complexity bound relative to R-MAX.

### Positioning among PAC-MDP algorithms
MoRmax sits at the tightest end of the classical (batch-known-unknown-threshold style) PAC-MDP algorithm family that begins with [[Algorithms/R-MAX|R-MAX]] and continues through [[Algorithms/Model-based Interval Estimation (MBIE)|MBIE]]'s confidence-interval refinement — MoRmax can be read as combining R-MAX's simple algorithmic structure (a hard known/unknown threshold, rather than MBIE's continuously-shrinking confidence intervals) with a substantially sharper proof technique, showing that algorithmic sophistication and proof sophistication are somewhat separable axes of improvement in this literature.

## See also
[[Algorithms/R-MAX]], [[Algorithms/Model-based Interval Estimation (MBIE)|MBIE]], [[Sample Complexity of Exploration]], [[Regret Analysis]]
