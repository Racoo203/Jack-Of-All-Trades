---
title: "Upper Bounding the Expected Next State Value (UBEV)"
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
unit: Algorithms
level: MSc
status: seeding
confidence: 0
tags: [reinforcement-learning, algorithms, theory, pac-mdp, episodic]
---
## Definition
<!-- UNVERIFIED: check against Dann, Lattimore & Brunskill (2017), "Unifying PAC and Regret: Uniform PAC Bounds for Episodic Reinforcement Learning"; not covered in the MA338 slide decks -->
UBEV is a model-based algorithm for the **episodic, finite-horizon** MDP setting (fixed horizon $H$, no discount factor $\gamma$ needed), constructing high-probability upper confidence bounds directly on the *expected value of the next state* at every step of planning, and acting greedily with respect to these optimistic bounds — analogous in spirit to [[Algorithms/Model-based Interval Estimation (MBIE)|MBIE]]'s confidence-interval-based optimism, but adapted to the finite-horizon/episodic structure rather than the infinite-horizon discounted setting.

## Properties
### Uniform-PAC: unifying PAC and regret guarantees
UBEV's central contribution is a **uniform-PAC** bound: a single guarantee that simultaneously implies both a PAC-style [[Sample Complexity of Exploration|sample-complexity]] bound (few $\epsilon$-suboptimal episodes, for *every* $\epsilon$ simultaneously, not just one fixed target accuracy) and a [[Regret Analysis|regret]] bound of matching order — where earlier algorithms in this literature typically proved only one guarantee type at a time (PAC *or* regret, with distinct, non-interchangeable proof techniques). This resolved a previously-open gap between the PAC-MDP and regret-minimisation traditions in episodic RL theory.

### Episodic vs. discounted setting
The switch from a discount factor $\gamma$ to a fixed episode length $H$ changes the bookkeeping (bounds scale in $H$ rather than $1/(1-\gamma)$, which is the standard "effective horizon" translation between the two settings) but preserves the same underlying optimism-under-uncertainty mechanism seen throughout [[Algorithms/R-MAX|R-MAX]], [[Algorithms/Model-based Interval Estimation (MBIE)|MBIE]], and [[Algorithms/MoRmax|MoRmax]] — UBEV can be read as this same family of ideas, re-derived and tightened specifically for the episodic-horizon regime, alongside [[Algorithms/Upper-Confidence Fixed-Horizon (UCFH)|UCFH]].

## See also
[[Algorithms/Upper-Confidence Fixed-Horizon (UCFH)|UCFH]], [[Regret Analysis]], [[Sample Complexity of Exploration]], [[Algorithms/Model-based Interval Estimation (MBIE)|MBIE]]
