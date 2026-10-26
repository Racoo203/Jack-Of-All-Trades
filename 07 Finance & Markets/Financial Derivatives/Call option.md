---
title: "Call option"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "Chapter 4 - Financial Markets"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, options]
---
## Definition
The holder of a **(European) call option** has the **right but not the obligation** to buy a share from the writer (seller) on a prescribed **exercise date** $T$ at a **strike price** $K$. Because this is a right, not an obligation, the holder pays a **premium** to the writer at inception. The writer, in contrast, has no choice: they must deliver the share if the holder exercises.

The **payoff** to the holder at time $T$ is
$$
f(S_T) = \max\{S_T-K,\,0\}.
$$
If $S_T<K$ the holder would be foolish to exercise (they can buy at the lower market price $S_T$ instead), so the option expires worthless and the holder loses only the premium. If $S_T>K$, the holder exercises, buying at $K$ and immediately selling at $S_T$ for a gain of $S_T-K$.

## Properties
### Moneyness
A call option is:
- **In-the-money (ITM)** if $S_t>K$;
- **Out-of-the-money (OTM)** if $S_t<K$;
- **At-the-money (ATM)** if $S_t=K$.

### Risk/reward asymmetry
The holder's maximum loss is the premium paid; the writer's downside is unlimited (share prices are theoretically unbounded above).

### Determinants of option value
Qualitatively (formalised later by the [[Greeks]] and the [[Black-Scholes formula]]): call value rises with the underlying price, falls as the strike rises, rises with time to expiry (for American options) and with volatility, and is ambiguously affected by the risk-free rate (though typically call values rise as $r$ increases); dividends reduce call value (the underlying's price drops on the ex-dividend date).

## Examples
Profit diagram (long call, strike $K$, premium $p$): profit $=\max\{S_T-K,0\}-p$, with a **breakeven point** at $S_T=K+p$. See also [[Option Trading Strategies]].

## See also
[[Put option]], [[European Options]], [[American Options]], [[Put-call parity]], [[Black-Scholes formula]], [[Greeks]]
