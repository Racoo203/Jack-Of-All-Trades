---
title: Neural Fitted Q-learning
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
unit: Algorithms
level: MSc
status: seeding
confidence: 0
tags: [reinforcement-learning, deep-rl, algorithms, off-policy]
---
## Definition
<!-- UNVERIFIED: check against Riedmiller (2005), "Neural Fitted Q Iteration"; not covered in the MA338 slide decks -->
Neural Fitted Q-learning (NFQ) is a **batch-mode** (offline, within each iteration) Q-learning algorithm, historically the most direct precursor to [[Algorithms/Deep Q-Network|DQN]]: rather than updating a neural-network $Q(s,a,w)$ online with a single semi-gradient step per transition (as in naive online deep Q-learning), NFQ collects a batch of transitions $\{(s_i,a_i,r_i,s_i')\}$, computes Q-learning targets $y_i = r_i+\gamma\max_{a'}Q(s_i',a',w)$ for the *entire batch* using the current network, and then trains the network on this fixed target set to (approximate) convergence via ordinary supervised regression, before repeating with a new set of targets computed from the updated network.

## Properties
### Why batch/fitted updates help stability
Freezing the targets $y_i$ across an entire supervised-regression phase is structurally very similar to [[Algorithms/Deep Q-Network|DQN]]'s **target network** ($w^-$, held fixed between periodic syncs) — both techniques prevent the regression target from shifting *during* the optimisation that is supposed to be converging toward it, which is exactly what causes instability under the [[Nonlinear Functional Approximation|Deadly Triad]]. NFQ can be seen as the batch-mode ancestor of the idea DQN later adapted into an online, replay-buffer-based algorithm suitable for problems too large for full-batch fitting.

### Relation to DQN
DQN (Mnih et al., 2015) is often summarised as NFQ made online and scalable: instead of full-batch fitted iterations, DQN uses **mini-batches** sampled from a large **replay buffer** (rather than a small fixed batch recomputed every iteration) and updates the network incrementally via SGD rather than retraining to convergence at each iteration — trading NFQ's per-iteration stability for the ability to handle much larger, higher-dimensional (e.g. pixel-based) state spaces and much longer training runs.

## See also
[[Algorithms/Deep Q-Network]], [[Algorithms/Q-learning]], [[Nonlinear Functional Approximation]]
