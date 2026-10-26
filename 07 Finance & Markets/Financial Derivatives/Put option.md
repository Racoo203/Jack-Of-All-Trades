---
title: "Put option"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "Chapter 4 - Financial Markets"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, options]
---
## Definition
The holder of a **(European) put option** has the **right but not the obligation** to sell one share at time $T$ (the exercise date) to the issuer at the strike price $K$. As with the [[Call option]], the holder pays a premium for this choice, while the writer has no choice. The option should be exercised if $S_T<K$, giving a **payoff**
$$
f(S_T) = \max\{K-S_T,\,0\}.
$$

## Properties
### Moneyness
A put option is:
- **In-the-money (ITM)** if $S_t<K$;
- **Out-of-the-money (OTM)** if $S_t>K$;
- **At-the-money (ATM)** if $S_t=K$.

### Risk/reward
The holder's maximum loss is the premium paid; the maximum gain is capped at $K$ (achieved if the share price falls to zero) — unlike a call, whose gain is theoretically unbounded.

## See also
[[Call option]], [[European Options]], [[American Options]], [[Put-call parity]], [[Black-Scholes formula]]
