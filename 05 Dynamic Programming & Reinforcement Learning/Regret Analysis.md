---
title: Regret Analysis
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: seeding
confidence: 0
tags: [reinforcement-learning, theory, bandits]
---
## Definition
<!-- UNVERIFIED: check against a dedicated RL-theory reference (e.g. Lattimore & Szepesvári, "Bandit Algorithms"), as this is not covered in the MA338 slide decks -->
**Regret** measures the cumulative cost of not always playing the optimal action. For a $k$-armed bandit with action values $q_*(a)$, let $a^* = \arg\max_a q_*(a)$. The (pseudo-)regret after $T$ rounds of an algorithm producing actions $A_1,\dots,A_T$ is
$$\mathrm{Regret}(T) := \sum_{t=1}^T \left[q_*(a^*) - q_*(A_t)\right] = T\,q_*(a^*) - \mathbb{E}\left[\sum_{t=1}^T R_t\right].$$
It generalises to episodic MDPs by comparing the cumulative reward of the learning policy against that of the optimal policy over $K$ episodes of length $H$.

## Properties
### Logarithmic regret is the benchmark for bandits
For the stochastic $k$-armed bandit, Lai & Robbins (1985) showed that **no** algorithm can achieve expected regret better than $\Omega(\log T)$ asymptotically (a fundamental lower bound driven by the statistical difficulty of distinguishing a near-optimal arm from the optimal one with a bounded number of samples). [[UCB exploration]]-style algorithms achieve matching $O(\log T)$ upper bounds under sub-Gaussian reward assumptions — the "optimism in the face of uncertainty" principle behind UCB is specifically designed to hit this bound. [[Thompson sampling]] achieves comparable $O(\log T)$ regret with a Bayesian argument (Agrawal & Goyal).

### Regret vs. [[Sample Complexity]]
Regret and sample complexity are two lenses on the same exploration problem: regret counts the *cumulative reward lost* while learning (natural in continual/online settings), whereas sample complexity (below) counts the *number of suboptimal/mistake steps* before near-optimal behaviour is reached (natural in episodic/PAC settings). Bounds on one can often be converted to bounds on the other, but the conversion is not always tight.

### Extension to episodic MDPs
For tabular episodic MDPs with $S$ states, $A$ actions, and horizon $H$, minimax-optimal regret is $\tilde O(\sqrt{HSAT})$ (Azar et al. 2017; Jin et al. 2018), where $T=KH$ is the total number of steps across $K$ episodes. Algorithms achieving bounds in this family in this domain include [[Algorithms/Upper-Confidence Fixed-Horizon (UCFH)|UCFH]] and [[Algorithms/Upper Bounding the Expected Next State Value (UBEV)|UBEV]].

## See also
[[Multi-armed bandits]], [[UCB exploration]], [[Thompson sampling]], [[Sample Complexity]], [[Algorithms/Upper-Confidence Fixed-Horizon (UCFH)|UCFH]], [[Algorithms/Upper Bounding the Expected Next State Value (UBEV)|UBEV]]
