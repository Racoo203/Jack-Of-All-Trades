---
title: "Forward contract"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "Chapter 4 - Financial Markets"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, forwards]
---
## Definition
A **forward contract** is an agreement to buy or sell an asset at a certain time in the future (the **maturity/expiry date** $T$) for a certain price (the **forward price**, or **delivery price** $K$). Both the issuer and the holder are *obligated* to complete the trade. The forward price is set so the contract's initial value is zero (no money changes hands at inception); as time passes and market conditions change, the contract acquires value.

Let $K$ be the delivery price, $T$ the maturity date, and $S_t$ ($0\le t\le T$) the value of the underlying at time $t$. The **payoff to the holder** at maturity is
$$
f(S_T) = S_T - K.
$$
So if $S_T>K$ the holder gains $S_T-K$ (and the issuer loses the same amount); if $S_T<K$ the holder loses $K-S_T$.

## Properties
### Value of a forward contract (no-arbitrage pricing)
Let $t$ be the current time, $T$ maturity, $S_t$ the spot price of an asset paying no income, and $r$ the continuously-compounded risk-free rate. Let $F_t$ denote the forward price at time $t$. Then, by [[No-arbitrage principle|no-arbitrage]]:
$$
F_t = S_t\,e^{r(T-t)}.
$$
**Proof (arbitrage argument).** If $F_t > S_te^{r(T-t)}$: borrow $S_t$ at rate $r$ for $T-t$ years, buy the asset, and take a short position in the forward. At $T$, deliver the asset for $F_t$ and use $S_te^{r(T-t)}$ of the proceeds to repay the loan, pocketing the riskless profit $F_t - S_te^{r(T-t)}>0$ — an arbitrage. A symmetric argument rules out $F_t < S_te^{r(T-t)}$. $\blacksquare$

### Notation table
| Symbol | Meaning |
|---|---|
| $T$ | maturity (years) |
| $t$ | current time (years) |
| $S_t,S_T$ | spot price of underlying at $t,T$ |
| $K$ | delivery price |
| $f$ | value of a long forward at time $t$ |
| $F$ | forward price at time $t$ |
| $r$ | continuously-compounded risk-free rate |

## Examples
Forwards are typically traded over-the-counter (OTC), unlike [[Future contract|futures]], and carry no margin requirement — the entire gain/loss is realised only at maturity $T$.

## See also
[[Future contract]], [[No-arbitrage principle]], [[Derivative contract]], [[Long and Short Positions]]
