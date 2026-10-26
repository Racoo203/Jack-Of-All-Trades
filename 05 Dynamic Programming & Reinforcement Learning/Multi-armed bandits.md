---
title: Multi-armed bandits
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: drafted
confidence: 0
tags: [reinforcement-learning, bandits]
---
## Definition
The $k$-armed bandit problem is the single-state special case of reinforcement learning: repeatedly choose among $k$ actions ("arms"); after each choice, receive a numerical reward drawn from a stationary probability distribution depending only on the action selected. Let $A_t$ be the action selected at step $t$ and $R_t$ its reward. The **value** of action $a$ is
$$q_*(a) := \mathbb{E}[R_t \mid A_t = a].$$
The agent does not know the $q_*(a)$'s but maintains estimates $Q_t(a) \approx q_*(a)$. The objective is to maximise expected total reward over time, which forces a trade-off between exploring to improve the estimates and exploiting the current best estimate — see [[Exploration vs Exploitation]].

## Properties
### Sample-average estimation
The natural estimator averages the rewards actually observed for action $a$:
$$Q_t(a) := \frac{\sum_{i=1}^{t-1}R_i\, \mathbb 1[A_i=a]}{\sum_{i=1}^{t-1}\mathbb 1[A_i=a]}.$$
By the Law of Large Numbers, $Q_t(a) \to q_*(a)$ as the denominator $\to \infty$ — this is the **sample-average method**.

### Greedy action selection (and why it alone is insufficient)
The greedy rule $A_t = \arg\max_a Q_t(a)$ always exploits, never explores — an agent using it exclusively can permanently lock onto a suboptimal arm whose early samples happened to look good. [[Epsilon-greedy exploration]] fixes this with a small probability of pure exploration.

### Incremental update (derivation)
Let $R_i$ be the reward after the $i$-th selection of a fixed action, and $Q_n := \frac{R_1+\cdots+R_{n-1}}{n-1}$. Then
$$Q_{n+1} = Q_n + \frac{1}{n}[R_n - Q_n].$$
*Derivation.* $Q_{n+1} = \frac{1}{n}\sum_{i=1}^n R_i = \frac{1}{n}\left(R_n + \sum_{i=1}^{n-1}R_i\right) = \frac{1}{n}\left(R_n + (n-1)Q_n\right) = \frac{1}{n}\left(R_n + nQ_n - Q_n\right) = Q_n + \frac{1}{n}(R_n - Q_n)$. $\blacksquare$
This has the general form **NewEstimate ← OldEstimate + StepSize·[Target − OldEstimate]**, where the bracketed term is an *error* driving the update. With a constant step-size $\alpha$ instead of $1/n$, the method adapts to [[Stationary & Non-stationary Environments|non-stationary]] problems (exponential recency weighting — see that note for the convergence conditions on $\alpha$).

### Initial-value bias
Every incremental method above is biased by its initial estimate $Q_1(a)$. For sample-averaging, the bias vanishes once every action has been selected at least once; for constant-$\alpha$ methods, the bias is **permanent** (though decreasing geometrically — see [[Stationary & Non-stationary Environments]]).

## Examples
Listening to unfamiliar songs with generic names is a bandit problem: each play is an action, enjoyment is the (stochastic, stationary) reward.

## See also
[[Exploration vs Exploitation]], [[Epsilon-greedy exploration]], [[UCB exploration]], [[Boltzmann exploration]], [[Thompson sampling]], [[Stationary & Non-stationary Environments]], [[Asymptotic Convergence]]
