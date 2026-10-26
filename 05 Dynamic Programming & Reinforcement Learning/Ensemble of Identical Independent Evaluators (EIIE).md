---
title: "Ensemble of Identical Independent Evaluators (EIIE)"
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: seeding
confidence: 0
tags: [reinforcement-learning, finance, deep-rl, theory]
---
## Definition
<!-- UNVERIFIED: check against Jiang, Xu & Liang (2017), "A Deep Reinforcement Learning Framework for the Financial Portfolio Management Problem"; not covered in the MA338 slide decks — this belongs to Raúl's own RL-in-finance reading rather than the taught module -->
The Ensemble of Identical Independent Evaluators (EIIE) is a neural-network architecture for portfolio-management RL (Jiang, Xu & Liang, 2017): a **single** network (the "evaluator"), sharing weights, is applied **independently** to each asset's own price-history window to produce a per-asset score, and the scores across all assets are then combined (typically via softmax) into portfolio weights.

## Properties
### Why weight-sharing across assets
Applying an *identical* network independently to each asset (rather than one large network taking the full multi-asset state as input) means: (i) the number of parameters does not grow with the number of assets in the universe, so the architecture scales to large portfolios; (ii) it encodes the inductive bias that the same technical/price-action features should be evaluated the same way regardless of which specific asset they belong to, aiding generalisation to assets seen rarely (or not at all) during training; (iii) since the evaluators do not interact, evaluation is trivially **parallelisable** across assets.

### Role within the RL problem formulation
EIIE outputs a score per asset, converted (e.g. via softmax) into portfolio weights forming the **policy**'s output (a continuous action — the portfolio allocation vector). This is a [[Policy-based|policy-based]] (specifically, deterministic-policy or direct-mapping) architecture: the network maps a state (recent price histories) directly to an action (portfolio weights), trained by policy-gradient-style methods to maximise a return/risk-adjusted objective such as the [[Differential Sharpe ratio]] or cumulative portfolio return, using [[Algorithms/REINFORCE|REINFORCE]]-style or actor-critic training in the original paper.

### Relevance to `investment-automation`
This is the architecture referenced in Raúl's personal `investment-automation` project ("mean-CVaR optimizer + REINFORCE RL allocation agent"): EIIE-style per-asset evaluators are a standard building block for scaling deep-RL portfolio allocation beyond a handful of hand-picked assets.

## See also
[[Differential Sharpe ratio]], [[Algorithms/REINFORCE]], [[Policy-based]], [[Nonlinear Functional Approximation]]
