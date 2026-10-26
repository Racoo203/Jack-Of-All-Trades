---
title: "Minimax estimator"
domain: "Probability & Statistics"
course: "Bayesian Statistics"
unit: "Chapter 4 - Bayesian Decision Theory"
level: MSc
status: drafted
confidence: 0
tags: [bayesian-statistics, decision-theory]
---
## Definition
The minimax risk for a [[Loss function]] $L$ is
$$
\bar R = \inf_{\delta^*\in D^*}\ \sup_\theta R(\theta,\delta^*)
$$
where $D^*$ is the space of (possibly randomized) decision rules, and $R(\theta,\delta)$ is the frequentist risk (see [[Bayes risk]]). A **minimax estimator** $\delta_0$ achieves this bound: $\sup_\theta R(\theta,\delta_0) = \bar R$. Minimax rules provide insurance against the worst case — the natural criterion when an adversary could effectively choose $\theta$ after seeing the decision rule.

## Properties
### Randomized estimators
A randomized estimator $\delta^*$ takes values in the space $D^*$ of probability distributions over $D$: rather than a deterministic function of the data, the decision itself is drawn randomly (e.g. from a distribution depending on $x$). Frequentist risk of $\delta^*$ is the average loss over both the data and this extra randomization. Randomization is needed in frequentist theory for exact-coverage procedures and in adversarial (game-theoretic) settings — but for **Bayesian** analysis, randomization never helps:
$$
\inf_{\delta\in D} r(\pi,\delta) = \inf_{\delta^*\in D^*} r(\pi,\delta^*)
$$
i.e. there is always a deterministic Bayes rule at least as good as any randomized one — because the pointwise-minimization argument in [[Bayes risk]] already picks the single best action at each $x$.

### Worked example: 3-state minimax decision (loss matrix)
A physician chooses among actions $a_1,a_2,a_3$ against states $\theta_1,\theta_2,\theta_3$ with loss matrix
$$
\begin{array}{c|ccc} & a_1 & a_2 & a_3 \\\hline \theta_1 & 7 & 1 & 3 \\ \theta_2 & 0 & 1 & 6 \\ \theta_3 & 1 & 2 & 0 \end{array}
$$
A randomized action is $\delta = p_1\langle a_1\rangle + p_2\langle a_2\rangle + p_3\langle a_3\rangle$ ($\sum p_i=1$), with risk
$$
R(\theta_1,\delta)=7p_1+p_2+3p_3,\quad R(\theta_2,\delta)=p_2+6p_3,\quad R(\theta_3,\delta)=p_1+2p_2
$$
To find $\delta^*=\arg\min_\delta \sup_\theta R(\theta,\delta)$, check each region where one $R(\theta_i,\delta)$ dominates the others and minimize there. E.g. on the region where $\theta_1$ is worst ($7p_1+p_2+3p_3 \ge$ the other two), using $p_2=1-p_1-p_3$:
$$
\sup_\theta R = 7p_1+p_2+3p_3 = 6p_1+1+2p_3
$$
minimized at the smallest feasible $p_1$ and $p_3$ within that region, giving $p_1=3/49,\ p_3=1/7,\ p_2=39/49$. Repeating the same computation on the regions where $\theta_2$ or $\theta_3$ is worst yields the **same** solution — confirming $\delta^* = \tfrac{3}{49}\langle a_1\rangle + \tfrac{39}{49}\langle a_2\rangle + \tfrac17\langle a_3\rangle$ is minimax, with risk equal across all three states of nature (a hallmark of a minimax solution: at the optimum, the risk is "equalized" across the states that are candidates for being worst-case).

## See also
[[Bayes risk]], [[Loss function]], [[Bayes estimate]]
