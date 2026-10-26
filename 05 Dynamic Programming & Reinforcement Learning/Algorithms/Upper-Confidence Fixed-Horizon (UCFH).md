---
title: "Upper-Confidence Fixed-Horizon (UCFH)"
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
unit: Algorithms
level: MSc
status: seeding
confidence: 0
tags: [reinforcement-learning, algorithms, theory, pac-mdp, episodic]
---
## Definition
<!-- UNVERIFIED: check against Dann & Brunskill (2015), "Sample Complexity of Episodic Fixed-Horizon Reinforcement Learning"; not covered in the MA338 slide decks -->
UCFH (Upper-Confidence Fixed-Horizon) is a model-based algorithm for the fixed-horizon episodic MDP setting, applying the same **optimism-in-the-face-of-uncertainty** principle as [[UCB exploration|UCB]]/[[Algorithms/Model-based Interval Estimation (MBIE)|MBIE]] — confidence bounds on the empirical model, planning optimistically within them — but specifically adapted, and analysed, for the episodic-fixed-horizon case (horizon $H$, no discounting), giving one of the tighter known sample-complexity bounds for this setting at the time of publication.

## Properties
### Why the fixed-horizon setting needs separate analysis
The [[Discount factor|discounted, infinite-horizon]] setting (assumed by R-MAX, MBIE, MoRmax) and the **fixed-horizon episodic** setting are related but not interchangeable: a fixed horizon means the optimal policy is generally [[Stationary & Non-stationary Policies|non-stationary]] (time-step-dependent, since the number of remaining steps matters), whereas discounted infinite-horizon MDPs admit stationary optimal policies. UCFH's analysis is built directly around per-time-step value functions $v_h^*(s)$ (indexed by remaining horizon $h$), rather than a single stationary $v^*(s)$ — a structurally different, though closely related, planning problem to [[Dynamic programming|standard DP]] on discounted MDPs.

### Relation to UBEV
UCFH and [[Algorithms/Upper Bounding the Expected Next State Value (UBEV)|UBEV]] both target the fixed-horizon episodic setting with confidence-bound-based optimism; UBEV additionally unifies its guarantee into a single uniform-PAC bound implying both PAC and regret guarantees, whereas UCFH's original analysis is presented as a (tight, for its time) PAC-style sample-complexity bound. Together they represent the episodic-horizon analogue of the discounted-setting progression from [[Algorithms/R-MAX|R-MAX]] through [[Algorithms/MoRmax|MoRmax]].

## See also
[[Algorithms/Upper Bounding the Expected Next State Value (UBEV)|UBEV]], [[Sample Complexity of Exploration]], [[Regret Analysis]], [[Stationary & Non-stationary Policies]]
