---
title: Sample Complexity of Exploration
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: seeding
confidence: 0
tags: [reinforcement-learning, theory]
---
## Definition
<!-- UNVERIFIED: check against a dedicated RL-theory reference (Kakade 2003; Strehl, Li & Littman 2009); not covered in the MA338 slide decks -->
The **sample complexity of exploration** of an online RL algorithm is the number of time steps, over an infinite run, on which the algorithm's current policy is *not* $\epsilon$-optimal from the current state, bounded with probability $\ge 1-\delta$. Formally, an algorithm has sample complexity $\zeta(\epsilon,\delta)$ if, except for at most $\zeta(\epsilon,\delta)$ steps (with probability $\ge 1-\delta$),
$$V^{A_t}(S_t) \ge V^*(S_t) - \epsilon,$$
where $V^{A_t}$ is the value function of the policy the algorithm would follow from step $t$ onward. This is the formal criterion underlying **PAC-MDP** (Probably Approximately Correct in Markov Decision Processes) algorithms.

## Properties
### The explore-or-exploit dichotomy (implicit lemma)
PAC-MDP proofs typically hinge on a dichotomy: at each step, either (a) the agent is already acting $\epsilon$-optimally ("exploit"), or (b) it visits an insufficiently-explored ("unknown") state-action pair, contributing toward completing the exploration of the MDP ("explore"). Since there are only finitely many state-action pairs and each can only be under-explored finitely many times before crossing a visitation threshold, case (b) can only occur a bounded number of times — this bound *is* the sample complexity.

### Representative bounds
- [[Algorithms/R-MAX|R-MAX]] (Brafman & Tennenholtz, 2002): $\tilde O\!\left(\dfrac{S^2A}{\epsilon^3(1-\gamma)^6}\right)$ (order-of-magnitude; exact exponents vary by proof/version).
- [[Algorithms/Model-based Interval Estimation (MBIE)|MBIE]] (Strehl & Littman, 2008) and [[Algorithms/MoRmax|MoRmax]] (Szita & Szepesvári, 2010) tighten this, with MoRmax achieving the (at-the-time) best-known polynomial dependence on $1/\epsilon$ for the discounted tabular setting.
- Episodic finite-horizon analogues: [[Algorithms/Upper-Confidence Fixed-Horizon (UCFH)|UCFH]] and [[Algorithms/Upper Bounding the Expected Next State Value (UBEV)|UBEV]] give PAC/regret guarantees for the $H$-step episodic setting without requiring the discount-factor machinery.

### Relation to Regret
A PAC-MDP sample-complexity bound $\zeta(\epsilon,\delta)$ can typically be converted into a regret bound of the same order (mistakes contribute $O(\epsilon)$-scale regret each, over $\zeta$ mistake-steps), but the two frameworks emphasise different failure modes: sample complexity bounds the number of *bad* decisions; regret bounds the *cumulative reward lost*, which can be dominated by a few very bad decisions even if most decisions are fine.

## See also
[[Sample Complexity]], [[Mean-square Sample Complexity]], [[Regret Analysis]], [[Algorithms/R-MAX]], [[Algorithms/Model-based Interval Estimation (MBIE)|MBIE]], [[Algorithms/MoRmax]]
