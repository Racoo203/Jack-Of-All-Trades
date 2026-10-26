---
title: MatrixRL
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
unit: Algorithms
level: MSc
status: seeding
confidence: 0
tags: [reinforcement-learning, algorithms, theory, function-approximation]
---
## Definition
<!-- UNVERIFIED: check against Yang & Wang (2019), "Sample-Optimal Parametric Q-Learning Using Linearly Additive Features"; not covered in the MA338 slide decks -->
MatrixRL is a provably-efficient RL algorithm for MDPs whose Q-function is (approximately) **bilinear** in separate state and action feature maps — $Q(s,a)\approx\phi(s)^\top M\psi(a)$ for a learnable matrix $M$ — rather than the single joint feature map $\phi(s,a)$ used by [[Algorithms/Least-Squares Value Iteration (LSVI)|LSVI]]. This matrix-factorised structure is designed to more directly capture problems where state and action features interact in a specific low-rank way, and to allow regret/sample-complexity bounds stated in terms of the feature-map dimensions rather than $|\mathcal S|,|\mathcal A|$ directly.

## Properties
### Bilinear vs. joint-feature parametrisation
Writing $Q(s,a)=\phi(s)^\top M\psi(a)$ instead of $Q(s,a)=\theta^\top\phi(s,a)$ (as in [[Algorithms/Least-Squares Value Iteration (LSVI)|LSVI]]'s linear-MDP setup) is a form of **low-rank matrix regression**: rather than learning a single long weight vector over a (potentially very high-dimensional) joint feature map, MatrixRL learns a $\dim(\phi)\times\dim(\psi)$ matrix $M$, which can be substantially more sample-efficient when the true interaction between state and action features genuinely has low rank — directly analogous to how low-rank matrix completion outperforms unstructured regression when the underlying data-generating matrix genuinely has low rank.

### Confidence-ellipsoid optimism, matrix version
Like [[Algorithms/Least-Squares Value Iteration (LSVI)|LSVI-UCB]], MatrixRL adds an optimism bonus derived from a confidence region around its estimate of $M$ (a matrix-valued generalisation of the vector confidence ellipsoids used in linear bandits/LSVI-UCB), preserving the same "optimism in the face of uncertainty" principle common to every algorithm in this reference layer ([[UCB exploration|UCB]], [[Algorithms/Model-based Interval Estimation (MBIE)|MBIE]], [[Algorithms/Least-Squares Value Iteration (LSVI)|LSVI-UCB]]), now instantiated for a bilinear rather than linear Q-function class.

### Positioning relative to LSVI
MatrixRL and LSVI represent two different structural assumptions for provably-efficient linear-style function approximation: LSVI assumes linearity in a single *joint* state-action feature map; MatrixRL assumes a *separable, low-rank bilinear* structure across independent state and action feature maps — the right choice between them, in practice, depends on which structural assumption more plausibly matches the true (unknown) $Q$-function of the problem at hand.

## See also
[[Algorithms/Least-Squares Value Iteration (LSVI)|LSVI]], [[Linear MDPs & Linear Functional Approximation]], [[Regret Analysis]]
