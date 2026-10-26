---
title: Deep Q-Network
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
unit: Algorithms
level: MSc
status: drafted
confidence: 0
tags: [reinforcement-learning, deep-rl, algorithms, off-policy]
---
## Definition
A Deep Q-Network (DQN) is [[Algorithms/Q-learning|Q-learning]] with $Q(s,a)$ replaced by a neural-network approximator $Q(s,a,w)$, engineered specifically to remain stable despite exhibiting all three components of the [[Nonlinear Functional Approximation|Deadly Triad]] (bootstrapping, function approximation, off-policy). Naively minimising the semi-gradient loss $l = \left[r+\gamma\max_{a'}Q(s',a',w)-Q(s,a,w)\right]^2$ works for tabular methods but leads to divergence with neural networks, because of (i) correlation between consecutive samples and (ii) non-stationary bootstrapped targets ($r+\gamma\max_aQ(s',a,w)$ changes every time $w$ is updated, since the same $w$ generates both the prediction and its own target).

## Properties
### DQN procedure
1. Take action $a \leftarrow \pi_\epsilon(Q(s,\cdot,w))$ ($\epsilon$-greedy on the current network).
2. Store the observed transition $(s,a,r,s')$ in a memory buffer $\mathcal D$ (**experience replay**).
3. Sample a mini-batch $\mathcal D_b\subset\mathcal D$ of size $b>1$.
4. Compute the bootstrapped Q-target using a **delayed** parameter vector $w^-$: $r+\gamma\max_aQ(s',a,w^-)$.
5. Minimise, by SGD, $L(w) = \mathbb E_{\mathcal D_b}\left[\left(r+\gamma\max_aQ(s',a,w^-)-Q(s,a,w)\right)^2\right]$.
6. Periodically synchronise $w^-\leftarrow w$ ("update the target network from time to time").

### Why each ingredient fixes a specific failure mode
- **Experience replay** breaks the correlation between consecutive samples (which violates the i.i.d. assumption underlying stable SGD) by building a shuffled dataset from the agent's *own* past experience and sampling mini-batches from it, rather than training on the live, highly-correlated trajectory as it is generated.
- **Target network** ($w^-$, held fixed between periodic syncs) removes the non-stationarity of the bootstrap target: since $w^-$ does not change during the inner optimisation of $w$, the regression target stops moving under the optimiser's feet, converting the otherwise ever-shifting objective into something closer to ordinary supervised regression for a batch of updates.

## Examples
TD-Gammon (the historical precursor, using TD(λ) rather than DQN's exact loss) used a neural network with $\sim$40–80 hidden units over 198 input features (backgammon board encoding) to approximate $V(S_t,w)$, predicting win probability directly from board state — an early demonstration that a nonlinear approximator could learn strong play purely from self-play TD updates, without the replay-buffer/target-network machinery DQN later formalised for the harder off-policy Q-learning case.

## See also
[[Algorithms/Q-learning]], [[Nonlinear Functional Approximation]], [[Deep Reinforcement Learning]], [[Algorithms/Double Deep Q-Network]]
