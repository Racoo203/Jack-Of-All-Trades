---
title: "Garman-Kohlhagen Formula"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "Chapter 6 - The Black-Scholes-Merton Model; PGT Lectures - Extending Black-Scholes"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, black-scholes, dividends, fx-options]
---
## Definition
This course's name for the [[Black-Scholes model|Black-Scholes-Merton]] extension to an underlying paying a **constant continuous dividend yield** $q\%$ per annum (dividend $qS_t\,dt$ over $(t,t+dt]$). The modified PDE is
$$
\frac{\partial f}{\partial t}+(r-q)S_t\frac{\partial f}{\partial S}+\tfrac12\sigma^2S_t^2\frac{\partial^2f}{\partial S^2}=rf,
$$
with solution
$$
c(t,S_t) = S_te^{-q(T-t)}N(d_1)-Ke^{-r(T-t)}N(d_2), \qquad p(t,S_t)=Ke^{-r(T-t)}N(-d_2)-S_te^{-q(T-t)}N(-d_1),
$$
$$
d_1 = \frac{\ln(S_t/K)+\left(r-q+\tfrac12\sigma^2\right)(T-t)}{\sigma\sqrt{T-t}}, \qquad d_2 = d_1-\sigma\sqrt{T-t}.
$$

## Properties
### Derivation sketch
Construct the delta-hedged portfolio $\pi_t=S_t\frac{\partial f}{\partial S}-f$. Since the underlying now pays a dividend, the no-arbitrage/self-financing condition becomes $-df + \left(dS_t+qS_t\,dt\right)\frac{\partial f}{\partial S} = r\pi_t\,dt$ (the dividend income is part of the riskless return the hedger must earn); substituting $df$ via [[Ito's Lemma]] and simplifying yields the modified PDE above.

### Equivalent "reduce the spot price" trick
A dividend-paying stock with yield $q$ produces the *same* terminal distribution for $S_T$ as a non-dividend stock starting at $S_0e^{-qT}$. Hence: to price a European option on a stock with continuous dividend yield $q$, replace $S_0$ by $S_0e^{-qT}$ in the ordinary [[Black-Scholes formula]].

### Discrete dividends
If dividends are paid as known discrete amounts at known ex-dividend dates (rather than a continuous yield), replace $S_0$ by $S_0 - \text{PV(dividends)}$ (the present value of all dividends paid during the option's life, discounted from their ex-dividend dates) in the ordinary Black-Scholes formula, then proceed as usual.

**Example.** Call, ex-dividend dates in 2 and 5 months, 50c dividend each, $S_0=K=\$40$, $\sigma=30\%$, $r=9\%$, $T=6$ months. PV(dividends) $=0.5e^{-0.09\times\frac16}+0.5e^{-0.09\times\frac{5}{12}}=0.9741$, so use $S=40-0.9741=39.0259$ in the ordinary formula: $c=\$3.67$. (For the American analogue see [[American Options]] and **Black's approximation**.)

### Binomial trees with a dividend yield
The risk-neutral up-probability becomes $p^*=\frac{e^{(r-q)T}-d}{u-d}$ (the capital-gains component of return must be $r-q$ since the dividend supplies the remaining $q$).

### Applications: currency, index, and futures options
- **Currency options**: a foreign currency behaves like a stock paying a continuous "dividend yield" equal to the foreign risk-free rate $r_f$ — substitute $q\to r_f$. Gives $c=S_te^{-r_f(T-t)}N(d_1)-Ke^{-r(T-t)}N(d_2)$, the historical origin of the name **Garman-Kohlhagen formula** (Garman & Kohlhagen, 1983, FX options).
- **Index options**: substitute $q=$ the average annualised dividend yield on the index.
- **Futures options**: require a genuinely different derivation — see [[Black's Model (Options on Futures)]] (equivalent to setting $q=r$).

## Examples
S&P 500 call, 2 months to maturity, $S=310$, $K=300$, $r=8\%$, $\sigma=20\%$, average dividend yield $q=3\%$ p.a.: $d_1=0.5444$, $d_2=0.4628$, $c=310(0.7069)e^{-0.005}-300(0.6782)e^{-0.0133}=\$17.28$ per index unit.

## See also
[[Black-Scholes formula]], [[Black-Scholes model]], [[American Options]], [[Black's Model (Options on Futures)]], [[Implied Volatility]]
