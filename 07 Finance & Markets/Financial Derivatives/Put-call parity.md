---
title: "Put-call parity"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "Chapter 4 - Financial Markets"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, options, no-arbitrage]
---
## Definition
For [[European Options|European]] [[Call option|call]] and [[Put option|put]] options on a non-dividend-paying stock, with the same strike $K$ and maturity $T$, **put-call parity (PCP)** states
$$
c_t + Ke^{-r(T-t)} = p_t + S_t.
$$

## Properties
### Proof (portfolio replication)
Compare two portfolios at maturity $T$:
- **Portfolio A**: one call option $+$ cash $Ke^{-r(T-t)}$.
- **Portfolio B**: one put option $+$ one share.

| | $S_T>K$ | $S_T<K$ |
|---|---|---|
| Portfolio A | $(S_T-K)+K=S_T$ | $0+K=K$ |
| Portfolio B | $0+S_T=S_T$ | $(K-S_T)+S_T=K$ |

Both portfolios are worth $\max\{S_T,K\}$ regardless of the outcome. By the [[No-arbitrage principle]], two portfolios with identical payoffs at $T$ must have the same value at every earlier time $t$, giving $c_t+Ke^{-r(T-t)} = p_t+S_t$. $\blacksquare$

### American options
Put-call parity holds only for European options. For American options on a non-dividend-paying stock, it becomes an inequality:
$$
S_t - K < C_t - P_t < S_t - Ke^{-r(T-t)}.
$$

### Discrete-dividend adjustment
If the stock pays a single discrete dividend $D$ at time $T_1<T$, compare:
- **Portfolio A**: long call $-$ short put (same $K,T$);
- **Portfolio B**: long stock, financed by borrowing $Ke^{-r(T-t)}+De^{-r(T_1-t)}$.

Both portfolios pay $S_T-K$ at maturity (Portfolio B receives the dividend $D$ at $T_1$, using it to help repay the loan), so
$$
c_t - p_t = S_t - Ke^{-r(T-t)} - De^{-r(T_1-t)}.
$$
The dividend reduces the effective forward value of the stock relative to the no-dividend case.

## Examples
GM stock, Dec 15 1995: two 35-strike March options (3 months), $r=5.5\%$, $c=4.25,\,p=1.00$. Then $c+Ke^{-r\tau}=38.78$ vs. $p+S=38.88$ — an approximate (not exact) parity check, the small discrepancy attributable to stock and option quotes being sampled at slightly different times.

**Discrete-dividend example.** Stock at £100, $K=£105$, $T=6$ months, dividend £2 at $T_1=3$ months, $r=5\%$, $c=£7$. Then
$$
p_t = c_t - S_t + Ke^{-r(T-t)} + De^{-r(T_1-t)} = 7-100+105e^{-0.025}+2e^{-0.0125} = £11.38.
$$

## See also
[[Call option]], [[Put option]], [[No-arbitrage principle]], [[Bounds for Option Prices]], [[American Options]]
