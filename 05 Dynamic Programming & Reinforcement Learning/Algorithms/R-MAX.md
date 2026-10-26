---
title: R-MAX
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
unit: Algorithms
level: MSc
status: seeding
confidence: 0
tags: [reinforcement-learning, algorithms, theory, pac-mdp, model-based]
---
## Definition
<!-- UNVERIFIED: check against Brafman & Tennenholtz (2002), "R-MAX — A General Polynomial Time Algorithm for Near-Optimal Reinforcement Learning"; not covered in the MA338 slide decks -->
R-MAX is a [[Model-free & Model-based|model-based]] tabular RL algorithm with a provable [[Sample Complexity of Exploration|PAC-MDP sample complexity]] bound, built on the principle of **optimism in the face of uncertainty**: every state-action pair that has not yet been visited "enough" times is optimistically assumed to yield the maximum possible reward $R_{\max}$ and to transition straight back to itself, ensuring the current model always *overestimates* the true value of insufficiently-explored regions and so is greedily preferred by planning — driving exploration automatically, with no separate exploration bonus or schedule required.

## Properties
### Mechanism
Maintain an empirical model $\hat p(s'\mid s,a)$ and $\hat r(s,a)$ for every state-action pair visited at least $m$ times (a threshold chosen from the desired accuracy $\epsilon$); for any pair visited fewer than $m$ times, treat it as "unknown" and set its modelled reward to $R_{\max}$ and its transition to a fictitious self-absorbing high-value state. Plan (via [[Dynamic programming|value iteration]]) on this optimistic model at every step (or periodically). Because unknown state-action pairs always look maximally attractive under the optimistic model, the planner's greedy policy is automatically driven to visit them — converting exploration into ordinary greedy planning under an optimistic model.

### The implicit explore-or-exploit lemma
This is the canonical instance of the "explore-or-exploit" dichotomy discussed in [[Sample Complexity of Exploration]]: at each step, the agent is either (a) already acting near-optimally with respect to the *true* MDP (because the known part of the model is accurate and dominates the optimistic unknown part), or (b) it visits an unknown state-action pair, making progress toward completing the model. Since there are only $|\mathcal S||\mathcal A|$ pairs and each needs only $m$ visits to become "known", case (b) can occur only finitely often — giving R-MAX its polynomial sample-complexity guarantee.

### Sample complexity
R-MAX's number of "mistake" steps (non-$\epsilon$-optimal decisions) is polynomial in $|\mathcal S|$, $|\mathcal A|$, $1/\epsilon$, and $1/(1-\gamma)$ — see [[Sample Complexity of Exploration]] for the general framework and comparison to tighter successors.

### Relation to successors
[[Algorithms/Model-based Interval Estimation (MBIE)|MBIE]] tightens R-MAX's confidence-region construction (using explicit confidence intervals on $\hat p,\hat r$ rather than a simple visit-count threshold); [[Algorithms/MoRmax|MoRmax]] further improves the polynomial dependence on $1/\epsilon$.

## See also
[[Sample Complexity of Exploration]], [[Algorithms/Model-based Interval Estimation (MBIE)|MBIE]], [[Algorithms/MoRmax]], [[Model-free & Model-based]], [[Dynamic programming]]
