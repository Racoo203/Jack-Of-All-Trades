---
title: "Option Trading Strategies"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "PGT Lectures - Option Strategies (J. O'Hara)"
level: MSc
status: seeding
confidence: 0
tags: [financial-derivatives, options, trading-strategies]
---
## Definition
An **option trading strategy** combines positions in [[Call option|calls]], [[Put option|puts]], and the underlying (see [[Long and Short Positions]]) to express a directional and/or volatility view while shaping the risk/reward profile. All strategies below are European-style, with $S_T$ the terminal share price, $K$ (or $K_1<K_2$) the strike(s), and premiums netted into a **breakeven point**.

## Properties
### Single-leg directional strategies
- **Long call**: buy a call. Bullish. Risk limited to the premium $p$; reward potentially unlimited. Payoff $\max\{S_T-K,0\}-p$. Breakeven: $S_T=K+p$.
- **Long put**: buy a put. Bearish. Risk limited to premium; reward potentially unlimited (capped at $K-p$ since $S_T\ge0$). Payoff $\max\{K-S_T,0\}-p$. Breakeven: $S_T=K-p$.
- **Short call**: sell a call. Very bearish view required. Risk unlimited; reward capped at the premium received. Payoff $p-\max\{S_T-K,0\}$. Breakeven: $S_T=K+p$.
- **Short put**: sell a put. Very bullish view required. Risk limited to $K-p$ (stock can only fall to 0); reward capped at the premium. Payoff $p-\max\{K-S_T,0\}$. Breakeven: $S_T=K-p$.

### Synthetics
- **Long synthetic** (synthetic long stock): buy a call, sell a put, same $K,T$. Bullish; mimics a long position in the stock at lower upfront cost. Combined payoff $=(S_T-K)+(-(K-S_T))=S_T-K$ (matches a forward on the stock struck at $K$).
- **Short synthetic** (synthetic short stock): sell a call, buy a put, same $K,T$. Bearish; mimics a short stock position. Combined payoff $=K-S_T$.

### Spreads (limited risk, limited reward)
- **Bull (call) spread**: buy an ITM call ($K_1$, lower strike), sell an OTM call ($K_2>K_1$). Moderately bullish. Cheaper than a naked long call, but caps the reward at $K_2-K_1-$(net premium). Payoff: $0$ for $S_T\le K_1$; $S_T-K_1$ for $K_1<S_T<K_2$; $K_2-K_1$ for $S_T\ge K_2$ (minus net premium).
- **Bear (call) spread**: buy an OTM call ($K_2$, higher strike), sell an ITM call ($K_1<K_2$). Moderately bearish. Cheaper than a naked short call, reward capped at the net premium.

### Volatility strategies (direction-neutral)
- **Long straddle**: buy a call and a put, same $K,T$. Bets on a **large move in either direction** (high volatility). Risk limited to the combined premium; reward potentially unlimited. Breakeven: $S_T=K\pm(\text{net premium})$.
- **Short straddle**: sell a call and a put, same $K,T$. Bets on **low volatility** (price stays near $K$). Risk potentially unlimited; reward capped at the premium received.
- **Long strangle**: buy an OTM call (higher $K_2$) and an OTM put (lower $K_1$), same $T$. Similar to a long straddle but cheaper, with a wider "dead zone" before profit begins. Bullish on volatility, neutral on direction.
- **Short strangle**: sell an OTM call and an OTM put, same $T$. Bearish on volatility (profits if the price stays within the two strikes); wider profit region than a short straddle, at the cost of unlimited risk on either side.
- **Call backspread**: buy two OTM calls (strike $K_2$), sell one ITM call (strike $K_1<K_2$). Bullish on both direction and volatility; payoff "flattens" on the downside (limited loss/gain) but is large if the price rises substantially — profitable on both a fall (limited) and, more so, a large rise.

### Ladders and butterflies
<!-- UNVERIFIED: check against Option Strategies slides (O'Hara, 2019) — the OCR of the original scanned PDF was unreadable for these four strategies (items 14-17 of 17); drafted here from standard textbook conventions only. -->
- **Long call ladder**: buy one ITM call, sell one ATM call, sell one further OTM call (three different strikes, same underlying/maturity). Reduces the cost of a bull spread further but reintroduces unlimited risk on a large upward move (net short one call overall).
- **Short call ladder**: the mirror position (sell one ITM call, buy one ATM call, buy one OTM call) — used when a large move in either direction, but especially upward, is expected, at reduced net cost versus a straddle/strangle.
- **Long call butterfly**: buy one ITM call ($K_1$), sell two ATM calls ($K_2$), buy one OTM call ($K_3$), with $K_1<K_2<K_3$ equally spaced. Bets on **low volatility**, price finishing near $K_2$; risk limited to the net premium paid, reward limited and maximised at $S_T=K_2$.
- **Short call butterfly**: the mirror position (sell $K_1$, buy two $K_2$, sell $K_3$). Bets on a **large move away from $K_2$** in either direction; risk limited to the net premium paid (opposite sign convention to the long butterfly), reward limited.

## See also
[[Call option]], [[Put option]], [[Long and Short Positions]], [[Volatility (Financial)]], [[Implied Volatility]]
