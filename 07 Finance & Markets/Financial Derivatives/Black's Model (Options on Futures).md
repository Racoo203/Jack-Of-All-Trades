---
title: "Black's Model (Options on Futures)"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "PGT Lectures - Extending Black-Scholes"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, futures-options, black-76]
---
## Definition
**Black's model** (also known as **Black-76**) prices a European option on a **futures contract**, where the futures price $F$ (rather than a spot price $S$) follows [[Geometric Brownian Motion]]:
$$
dF = \mu F\,dt+\sigma F\,dW_t.
$$
Options on futures are settled either by delivery of a futures position or in cash, and are popular because they avoid physical delivery of the underlying commodity/asset and are typically cheaper to fund than the underlying itself.

## Properties
### Derivation
Since $f$ (the option value) is a function of $F,t$, by [[Ito's Lemma]],
$$
df = \left(\frac{\partial f}{\partial t}+\tfrac12\sigma^2F^2\frac{\partial^2f}{\partial F^2}\right)dt + \sigma F\frac{\partial f}{\partial F}\,dW_t
$$
(no $\mu F\,\partial f/\partial F\,dt$ drift term survives once combined with the hedge below). Construct a portfolio of $-1$ derivative and $\partial f/\partial F$ futures contracts; since entering a futures contract costs nothing, the portfolio value is $\Pi=-f$. Over $\delta t$, the portfolio's wealth change is $\delta Q = \frac{\partial f}{\partial F}\delta F - \delta f$, which — after substituting the SDEs for $\delta F,\delta f$ — has its random ($\delta W_t$) terms cancel exactly, leaving $\delta Q$ riskless:
$$
\delta Q = -\left(\frac{\partial f}{\partial t}+\tfrac12\sigma^2F^2\frac{\partial^2f}{\partial F^2}\right)\delta t.
$$
By no-arbitrage, $\delta Q=r\Pi\,\delta t=-rf\,\delta t$, giving
$$
rf = \frac{\partial f}{\partial t}+\tfrac12\sigma^2F^2\frac{\partial^2f}{\partial F^2}.
$$
This has the **same form** as the [[Garman-Kohlhagen Formula|continuous-dividend Black-Scholes PDE]] with $q=r$ (a futures price behaves like a stock paying a continuous dividend yield equal to $r$, since holding a futures position costs nothing to establish).

### Pricing formula
$$
c = e^{-r(T-t)}\left\{FN(d_1)-KN(d_2)\right\}, \qquad p = e^{-r(T-t)}\left\{KN(-d_2)-FN(-d_1)\right\},
$$
$$
d_1 = \frac{\ln(F/K)+\tfrac12\sigma^2(T-t)}{\sigma\sqrt{T-t}}, \qquad d_2 = d_1-\sigma\sqrt{T-t}.
$$

## Examples
European put on crude oil futures, $T-t=4$ months, $F=K=\$20$, $r=9\%$, $\sigma=25\%$: $d_1=0.07216$, $d_2=-0.07216$, $p=e^{-0.03}(20\times0.5288-20\times0.4712)=\$1.12$.

## See also
[[Garman-Kohlhagen Formula]], [[Black-Scholes formula]], [[Future contract]], [[Ito's Lemma]]
