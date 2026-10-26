---
title: "Hedging"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "Chapter 7 - The Greeks & Market Risk"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, hedging, risk-management]
---
## Definition
**Hedging** is the reduction of a portfolio's sensitivity to the movement of an underlying asset by taking opposite positions in different financial instruments — a form of insurance. The goal is to *manage* risk, not necessarily eliminate it: removing all risk from a position generally also removes expected return, so a risk manager seeks an acceptable trade-off, and this balance is inherently subjective (different investors have different risk tolerances).

## Properties
### Static hedge: put-call parity
A one-off transaction combining an asset, a call, and a put ([[Put-call parity]]: $S_t+p_t=c_t+Ke^{-r\tau}$) can lock in a riskless return with a single trade — reducing sensitivity to zero without ongoing management. This is the exception; most hedges require continuous attention.

### Dynamic hedge: delta hedging
The standard approach uses the [[Greeks]] on a **dynamic** basis: the hedge is only instantaneously risk-free and needs continuous re-balancing of the ratio between the asset and the derivative holdings. A market maker who receives a premium above fair value for a written option can maintain a **delta-neutral** position (trading the underlying, or a cheaper future on it) to lock in a riskless profit — but only if transaction costs are low enough to make frequent re-hedging worthwhile.

### Drawbacks of delta hedging
1. **Hedge slippage**: the delta-hedging rule forces buying the underlying when its price has risen and selling when it has fallen — "buying high, selling low" on every rebalance, a structural loss that hedging more frequently reduces but cannot eliminate.
2. **Transaction costs**: substantial, since positions are adjusted regularly; more frequent rebalancing reduces slippage but increases these costs — a direct trade-off.

### Gamma-neutral hedging
Making a portfolio **gamma-neutral** as well as delta-neutral (using a second traded option, see [[Greeks]]) is a first correction for the fact that the underlying position cannot be adjusted continuously — it reduces the need for frequent re-hedging, at the cost of finding another sufficiently liquid traded option on the same underlying.

## Examples
Suppose a delta-neutral portfolio has $\Gamma=-3000$; a traded call has $\Delta=0.62,\Gamma=1.5$. Adding $3000/1.5=2000$ units of the call makes the portfolio gamma-neutral, but shifts its delta to $2000\times0.62=1240$ — so $1240$ units of the underlying must now be sold to restore delta-neutrality.

## See also
[[Greeks]], [[Put-call parity]], [[Black-Scholes model]], [[Long and Short Positions]]
