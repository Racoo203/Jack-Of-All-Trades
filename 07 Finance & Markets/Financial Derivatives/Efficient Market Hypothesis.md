---
title: "Efficient Market Hypothesis"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "Chapter 2 - Brownian Motion"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, market-efficiency]
---
## Definition
The **Efficient Market Hypothesis (EMH)** states that past history is fully reflected in the present price of an asset: past performance is not indicative of future returns, and markets respond immediately to any new information about an asset.

## Properties
### EMH $\Leftrightarrow$ Markov process
The course motivates modelling share prices with [[Brownian motion]] precisely because a [[Markov Property|Markov process]] — one where only the present value is relevant for predicting the future, so that knowledge of the past history is irrelevant for determining future outcomes — is the mathematical expression of the EMH. Since a (standard) Brownian motion $\{B_t\}$ has independent, stationary increments, it is a Markov process, and is offered as informal justification for using it (and its exponential transform, [[Geometric Brownian Motion]]) to model share prices.

> [!note] Markov $\ne$ martingale
> A Brownian motion is also a [[Martingale]] (its increments have zero mean), but the two properties are logically independent in general: Markov processes need not be martingales, and vice versa. The EMH argument above only invokes the Markov property.

## Examples
If the EMH held exactly and prices were driven by ordinary Brownian motion, an investor could not use technical analysis (patterns in past prices) to earn abnormal returns, since the conditional distribution of $B_t$ given the entire history up to $s<t$ depends only on $B_s$.

## See also
[[Brownian motion]], [[Martingale]], [[Bachelier's Model]], [[Geometric Brownian Motion]]
