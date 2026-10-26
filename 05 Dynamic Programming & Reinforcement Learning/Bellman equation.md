---
title: Bellman equation
domain: Dynamic Programming & Reinforcement Learning
course: Dynamic Programming & Reinforcement Learning
level: MSc
status: drafted
confidence: 0
tags: [reinforcement-learning, mdp, value-functions]
---
## Definition
The Bellman equation expresses the recursive consistency that every value function must satisfy: the value of a state equals the expected immediate reward plus the discounted value of the successor state. For the [[State value function|state-value function]]:
$$v_\pi(s) = \mathbb E_\pi[R_{t+1}+\gamma v_\pi(S_{t+1})\mid S_t=s] = \sum_{a}\pi(a\mid s)\sum_{s',r}p(s',r\mid s,a)\left[r+\gamma v_\pi(s')\right].$$
For the [[Action value function|action-value function]]:
$$q_\pi(s,a) = \mathbb E_\pi[R_{t+1}+\gamma v_\pi(S_{t+1})\mid S_t=s,A_t=a] = \sum_{s',r}p(s',r\mid s,a)\left[r+\gamma v_\pi(s')\right].$$
And the two are linked by $v_\pi(s)=\sum_a\pi(a\mid s)q_\pi(s,a)$, $q_\pi(s,a)=\sum_{s',r}p(s',r\mid s,a)\left[r+\gamma\sum_{a'}\pi(a'\mid s')q_\pi(s',a')\right]$.

## Properties
### Derivation (state-value case)
Starting from the definition $v_\pi(s)=\mathbb E_\pi[G_t\mid S_t=s]$ and the recursive identity $G_t = R_{t+1}+\gamma G_{t+1}$ (see [[Discount factor]]):
$$v_\pi(s) = \mathbb E_\pi[R_{t+1}+\gamma G_{t+1}\mid S_t=s] = \mathbb E_\pi[R_{t+1}+\gamma v_\pi(S_{t+1})\mid S_t=s],$$
since $\mathbb E_\pi[G_{t+1}\mid S_{t+1}=s'] = v_\pi(s')$ by definition, and the Markov property allows conditioning on $S_{t+1}$ alone. Expanding the expectation over $\pi$ (which action is taken) and $p$ (which reward/next-state results) gives the sum form above. $\blacksquare$

### Bellman *optimality* equations
$$v_*(s) = \max_a \sum_{s',r}p(s',r\mid s,a)\left[r+\gamma v_*(s')\right], \qquad q_*(s,a) = \sum_{s',r}p(s',r\mid s,a)\left[r+\gamma\max_{a'}q_*(s',a')\right].$$
These follow from the observation $v_*(s)=\max_{a}q_{\pi^*}(s,a)$: the optimal policy is greedy with respect to $q_*$, so the "$\sum_a\pi(a\mid s)(\cdots)$" of the ordinary Bellman equation collapses to a $\max_a(\cdots)$. Given $q_*$, the optimal policy is read off immediately: $\pi^*(a\mid s)=1$ if $a\in\arg\max_{a'}q_*(s,a')$, else $0$. If $q_*$ is known, no model of the environment is needed at all to act optimally.

### Existence and uniqueness
The Bellman equation for $v_\pi$ has a unique solution provided $\gamma<1$, or the task is episodic with $T<\infty$ (see [[Infinite & Finite Time Horizon]]). Under full knowledge of $p,\pi$, it is a linear system of $|\mathcal S|$ equations in $|\mathcal S|$ unknowns — solvable directly, but in practice tackled iteratively (see [[Dynamic programming]]), since the same iterative machinery generalises to the methods used later when $p$ is unknown.

### No closed form for the optimality equations
Unlike the (linear) policy-evaluation Bellman equation, the Bellman *optimality* equations are **non-linear** (because of the $\max$), with no general closed-form solution. This is the central obstacle that [[Dynamic programming]] (iterative policy/value iteration), and later [[Monte Carlo Learning]] and [[Temporal-Difference Learning]], are built to circumvent.

### Why exact solutions are rarely attainable in practice
Even though $v_*,q_*$ are well-defined, finding them exactly is almost always infeasible because: (i) the dynamics $p$ are often unknown; (ii) the state/action space is too large computationally; or (iii) the observed states lack the Markov property (partial observability). These three failure modes motivate, respectively: [[Monte Carlo Learning|model-free learning]], [[Nonlinear Functional Approximation|function approximation]], and (beyond this module's scope) POMDP methods.

## Examples
See the worked Gridworld examples throughout [[Markov Decision Process]] and [[Dynamic programming]] for hand-computed instances of both the evaluation and optimality forms.

## See also
[[State value function]], [[Action value function]], [[Markov Decision Process]], [[Dynamic programming]], [[Value Iteration Equation]]
