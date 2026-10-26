---
title: Thompson sampling
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: drafted
confidence: 0
tags: [reinforcement-learning, bandits, exploration]
---
## Definition
Thompson sampling is a Bayesian approach to the [[Exploration vs Exploitation]] trade-off: maintain a posterior distribution over each action's true value $q_*(a)$, given the rewards observed so far; on each round, **sample** a value $\tilde q(a)$ from each action's posterior, and select $A_t = \arg\max_a \tilde q(a)$. After observing $R_t$, update the posterior for $A_t$ via Bayes' rule and repeat.

## Properties
### Why sampling (rather than the posterior mean) explores correctly
An action whose posterior is wide (little data, high uncertainty) will occasionally produce a very high sampled value purely by chance, making it likely to be selected — this is exploration, driven entirely by posterior uncertainty rather than an explicit bonus term (contrast with [[UCB exploration]], which adds an explicit deterministic bonus). As data accumulates for an action, its posterior narrows and its sampled values cluster around the true mean, so exploration of that action naturally tapers off — the algorithm requires no explicitly tuned exploration parameter (unlike $\epsilon$ in [[Epsilon-greedy exploration]] or $c$ in UCB).

### Canonical conjugate example: Bernoulli/Beta bandit
For Bernoulli rewards (e.g. click/no-click), a Beta($\alpha_a,\beta_a$) posterior is conjugate: initialise Beta(1,1) (uniform) for each arm; after observing reward $r\in\{0,1\}$ for arm $a$, update $\alpha_a \leftarrow \alpha_a + r$, $\beta_a \leftarrow \beta_a + (1-r)$. Sampling $\tilde q(a)\sim\text{Beta}(\alpha_a,\beta_a)$ and picking the argmax is a complete Thompson-sampling bandit algorithm.

### Empirical/theoretical standing
Thompson sampling is not covered in the MA338 slide decks but is one of the best-performing bandit algorithms in practice and enjoys [[Regret Analysis|regret]] bounds competitive with UCB-style methods (Agrawal & Goyal, 2012/2013) despite predating formal regret analysis by decades (Thompson, 1933).

## See also
[[Multi-armed bandits]], [[UCB exploration]], [[Epsilon-greedy exploration]], [[Regret Analysis]]
