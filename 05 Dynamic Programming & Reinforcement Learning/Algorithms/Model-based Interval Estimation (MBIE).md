---
title: "Model-based Interval Estimation (MBIE)"
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
unit: Algorithms
level: MSc
status: seeding
confidence: 0
tags: [reinforcement-learning, algorithms, theory, pac-mdp, model-based]
---
## Definition
<!-- UNVERIFIED: check against Strehl & Littman (2008), "An analysis of model-based Interval Estimation for Markov Decision Processes"; not covered in the MA338 slide decks -->
Model-based Interval Estimation (MBIE) refines [[Algorithms/R-MAX|R-MAX]]'s optimism principle: instead of treating a state-action pair as either fully "known" or maximally optimistic ("unknown"), MBIE maintains explicit **confidence intervals** around its empirical transition/reward estimates $\hat p(s'\mid s,a),\hat r(s,a)$, sized by the number of visits (via a Hoeffding-style bound), and plans optimistically **within** those intervals: it selects, from the plausible set of MDPs consistent with the confidence intervals, the one that maximises the value of the current state — a continuous relaxation of R-MAX's binary known/unknown distinction.

## Properties
### Why continuous confidence intervals improve on R-MAX
R-MAX's fixed visit-count threshold $m$ must be conservative enough to guarantee accuracy in the worst case, meaning it can continue treating a state-action pair as "unknown" (and hence artificially optimistic) for longer than strictly necessary once enough data has actually accumulated to estimate it reasonably well. MBIE's confidence intervals shrink continuously and *automatically* as visit counts grow (following the standard $\sqrt{\ln(\cdot)/n}$ shape familiar from [[UCB exploration|UCB]]), so the degree of optimism at each state-action pair adapts smoothly to how much has actually been learned about it, rather than switching abruptly at a fixed threshold.

### Relation to UCB
MBIE is, in essence, the model-based, full-MDP generalisation of the same "optimism via a confidence bound" principle that [[UCB exploration|UCB]] applies to the single-state [[Multi-armed bandits|bandit]] problem: both add an uncertainty-shrinking bonus to a point estimate and act optimistically with respect to the result, but MBIE must additionally propagate that optimism through the *planning* step (value iteration over the plausible MDP set), since actions have delayed, multi-step consequences in the full MDP setting that a single-state bandit does not have.

### Sample complexity
MBIE-EB (a simplified exploration-bonus variant) achieves PAC-MDP sample complexity comparable to or tighter than R-MAX's, with the interval-based construction generally giving better *empirical* performance even when the worst-case polynomial bounds are of similar order — see [[Sample Complexity of Exploration]].

## See also
[[Algorithms/R-MAX]], [[Algorithms/MoRmax]], [[UCB exploration]], [[Sample Complexity of Exploration]]
