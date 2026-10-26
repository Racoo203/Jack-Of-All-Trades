---
title: "Implied Volatility"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "Chapter 6 - The Black-Scholes-Merton Model; Chapter 7 - The Greeks"
level: MSc
status: seeding
confidence: 0
tags: [financial-derivatives, volatility, black-scholes]
---
## Definition
Given the [[Black-Scholes formula]], every input except [[Volatility (Financial)|volatility]] $\sigma$ is directly observable ($S,K,r,T$) or quoted in the market — the **market price** of the option, $c_{\text{market}}$, is also observed. The **implied volatility** is the value of $\sigma$ that, substituted into the Black-Scholes formula, reproduces the observed market price:
$$
S_tN(d_1)-Ke^{-r\tau}N(d_2) = c_{\text{market}}(t).
$$

## Properties
### Why iteration is needed
The formula cannot be inverted algebraically for $\sigma$ (it appears inside $d_1,d_2$ in a way that has no closed form), so implied volatility is found **numerically**: start from a trial $\sigma$, compute the model price, and adjust. Since (by [[Greeks|vega]]) $\nu=\frac{\partial c}{\partial\sigma}=S\sqrt\tau\,\frac{e^{-d_1^2/2}}{\sqrt{2\pi}}>0$, call prices increase **monotonically** with $\sigma$, so the direction of adjustment is always well defined (bisection/interpolation converges).

**Example.** $S=21,K=20,r=0.1,\tau=0.25,c=1.875$. Try $\sigma=0.2\Rightarrow c=1.76$ (too low); $\sigma=0.3\Rightarrow c=2.10$ (too high); $\sigma=0.25\Rightarrow$ still too high; converges to $\sigma\approx0.235$.

**Example (linear interpolation).** A call costs £187.06 with $S=5000,K=5250,\tau=0.5,r=5\%$. Trying $\sigma=15\%\Rightarrow c=158.96$ and $\sigma=18\%\Rightarrow c=200.72$; linear interpolation gives $\sigma\approx17.02\%$.

### Weighted-average implied volatility
Different strikes on the same underlying/maturity typically produce *different* implied volatilities (the **volatility smile** — a shortcoming the [[Black-Scholes model]] cannot explain). A composite implied volatility can be formed as a weighted average, weighting each option by the sensitivity of its price to volatility.

<!-- UNVERIFIED: check against Chapter 6 slides, section on implied volatility -->
The slides' own worked example is internally inconsistent as transcribed: given two implied volatilities, 21% (at-the-money) and 26% (deep out-of-the-money), the text says "we could choose a weight of 0.9 for the deep-out-of-the-money option," but the stated calculation is $0.9\times0.21+0.1\times0.26=0.215$ — which actually applies the 0.9 weight to the *at-the-money* figure (0.21), not the OTM one (0.26) as the preceding sentence claims. Quoted here exactly as given; the intended weighting rule (heavier weight on the more liquid/sensitive at-the-money quote, consistent with the *numbers* used, vs. heavier weight on the OTM quote, consistent with the *wording*) should be confirmed against the original slide before relying on it.

## See also
[[Black-Scholes formula]], [[Volatility (Financial)]], [[Greeks]], [[Stochastic volatility]]
