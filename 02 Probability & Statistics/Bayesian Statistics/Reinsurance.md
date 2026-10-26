---
title: "Reinsurance"
domain: "Probability & Statistics"
course: "Bayesian Statistics"
unit: "Chapter 7 - Reinsurance, Convolution and Central Limit Theory (CLT)"
level: MSc
status: drafted
confidence: 0
tags: [bayesian-statistics, actuarial, risk-theory]
---
## Definition
Reinsurance is insurance purchased by an insurer (the **cedant**/**ceding company**) from another insurer (the **reinsurer**), as risk management. For aggregate loss $X\ge0$ initially assumed by the insurer, the insurer cedes $f(X)$ to the reinsurer (the **ceded function**, $0\le f(x)\le x$) and retains $X-f(X)$.

Two main types:
1. **Proportional reinsurance**: the cedant transfers a (fixed or variable) proportion of the risk.
2. **Non-proportional reinsurance**: e.g. **stop-loss reinsurance**, where the insurer's retention is capped at a fixed level $d$:
$$
(X-d)_+ := \max\{X-d,0\} = \begin{cases}X-d & X>d\\ 0 & X\le d\end{cases}
$$
The insurer retains at most $d$ (its "retention"); the reinsurer pays everything above $d$.

## Properties
### Worked derivation: expected reinsurer payment under a layered scheme
Claims $X\sim\text{Exp}(\beta=1/50)$ (mean 50). The reinsurer pays
$$
h(X) = \begin{cases}0 & 0<X<40\\ 0.5X-20 & 40\le X<100\\ X-70 & X\ge100\end{cases}
$$
The expected payment is $E[h(X)] = \int_{40}^{100}(0.5x-20)(0.02e^{-0.02x})\,dx + \int_{100}^\infty(x-70)(0.02e^{-0.02x})\,dx$. Splitting each integral into a "linear-in-$x$" part (integrate by parts) and a "constant" part:
$$
\int_{40}^{100}0.01xe^{-0.02x}\,dx - \int_{40}^{100}0.4e^{-0.02x}\,dx + \int_{100}^\infty 0.02xe^{-0.02x}\,dx - \int_{100}^\infty 1.4e^{-0.02x}\,dx
$$
Evaluating each piece (using $\int xe^{-cx}dx = -\frac{x}{c}e^{-cx}+\frac{1}{c}\int e^{-cx}dx$) and summing gives
$$
E[h(X)] = 25e^{-2} + 25e^{-0.8} \approx 14.62
$$
This kind of piecewise-defined payment function (a "layer" of stop-loss cover between two thresholds, at a fractional coinsurance rate) is typical of real excess-of-loss treaties.

## See also
[[Risk Theory]], [[Convolution]], [[Moment Generating Function]]
