---
title: "Least-Squares Value Iteration (LSVI)"
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
unit: Algorithms
level: MSc
status: seeding
confidence: 0
tags: [reinforcement-learning, algorithms, theory, function-approximation]
---
## Definition
<!-- UNVERIFIED: check against Jin, Yang, Wang & Jordan (2020), "Provably Efficient Reinforcement Learning with Linear Function Approximation"; not covered in the MA338 slide decks -->
Least-Squares Value Iteration (LSVI) — and its exploration-augmented variant **LSVI-UCB** — is [[Value Iteration Equation|value iteration]] adapted to [[Linear MDPs & Linear Functional Approximation|linear function approximation]] with **provable** sample-efficiency guarantees, specifically for **linear MDPs**: MDPs whose transition and reward functions are themselves linear in a known feature map $\phi(s,a)$, i.e. $p(\cdot\mid s,a) = \phi(s,a)^\top\mu(\cdot)$ and $r(s,a) = \phi(s,a)^\top\theta$ for some (unknown) $\mu,\theta$. At each iteration, LSVI fits the Q-function by **regularised least-squares regression** (ridge regression) against Bellman-backup targets, rather than tabular Bellman updates.

## Properties
### Least-squares Bellman backup
Given a dataset of transitions $\{(s_i,a_i,r_i,s_i')\}$, LSVI computes $w_h$ (the weight vector for the Q-function at horizon step $h$) by solving
$$w_h = \arg\min_w \sum_i\left(\phi(s_i,a_i)^\top w - \left(r_i + \max_{a'}\phi(s_i',a')^\top w_{h+1}\right)\right)^2 + \lambda\|w\|^2,$$
a ridge-regression fit of the linear Q-function against the one-step Bellman-optimal target — structurally identical to the [[Linear MDPs & Linear Functional Approximation|Gradient Monte Carlo/semi-gradient TD]] updates covered in this module, but solved in **closed form** at each iteration (via the ridge-regression normal equations) rather than incrementally by SGD.

### LSVI-UCB: adding optimism for provable exploration
Plain LSVI, like plain [[Algorithms/Q-learning|Q-learning]] with function approximation, has no guaranteed exploration behaviour. LSVI-UCB adds an explicit **UCB-style bonus** to the fitted Q-value, derived from the ridge-regression's own uncertainty (a confidence ellipsoid around $w_h$, in the spirit of linear bandits) — directly generalising the tabular [[Algorithms/Model-based Interval Estimation (MBIE)|MBIE]]/[[UCB exploration|UCB]] optimism principle to the linear-function-approximation setting, and yields the first (at publication) polynomial regret guarantee for RL with general linear function approximation.

### Relation to the module's function-approximation content
LSVI is best understood as the theoretically-principled counterpart to the semi-gradient TD/MC methods in [[Linear MDPs & Linear Functional Approximation]]: where the module's semi-gradient methods use online SGD with no finite-sample guarantee, LSVI uses batch ridge regression specifically because it is the estimator for which finite-sample regret/PAC bounds can be proven under the linear-MDP assumption.

## See also
[[Linear MDPs & Linear Functional Approximation]], [[Algorithms/MatrixRL]], [[Algorithms/Model-based Interval Estimation (MBIE)|MBIE]], [[Regret Analysis]]
