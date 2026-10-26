---
title: "Bounds for Option Prices"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "PGT Lectures - Advanced Topics in Option Pricing"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, no-arbitrage, option-bounds]
---
## Definition
Before any pricing formula is derived, the [[No-arbitrage principle]] alone pins down model-free **bounds** on option prices. Notation: lowercase $c,p$ for [[European Options|European]] call/put prices, uppercase $C,P$ for [[American Options|American]] call/put prices. Since American options grant a strict superset of exercise rights, $C\ge c$ and $P\ge p$.

## Properties
### Upper bounds
For both European and American calls: $c\le S$, $C\le S$ (a call can never be worth more than the stock itself — if $C>S$, buy the stock and sell the call for a riskless profit). For puts: $p\le K$, $P\le K$ (the maximum payoff at maturity is $K$); for the European put specifically, discounting gives the tighter bound $p\le Ke^{-r(T-t)}$ (this refinement does **not** apply to American puts, due to early exercise).

### Lower bound for a European call (non-dividend stock)
$$
c \ge \max\{S-Ke^{-r(T-t)},\,0\}.
$$
**Proof.** Compare Portfolio A (one call $+$ cash $Ke^{-r(T-t)}$) and Portfolio B (one share). At $T$: Portfolio A is worth $\max\{S_T,K\}$; Portfolio B is worth $S_T$. Since $\max\{S_T,K\}\ge S_T$ always, Portfolio A must be worth at least as much as Portfolio B today: $c+Ke^{-r(T-t)}\ge S \Rightarrow c\ge S-Ke^{-r(T-t)}$. Since $c\ge0$ always, $c\ge\max\{S-Ke^{-r(T-t)},0\}$. $\blacksquare$

### Lower bound for a European put (non-dividend stock)
By a symmetric argument, $p \ge \max\{Ke^{-r(T-t)}-S,\,0\}$.

## Examples
$S=51,K=50,T-t=0.5,r=12\%$: lower bound $=51-50e^{-0.06}\approx\$3.91$, so the call must be priced at least \$3.91.

## See also
[[No-arbitrage principle]], [[Put-call parity]], [[American Options]], [[Call option]], [[Put option]]
