---
title: "Greeks"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "Chapter 7 - The Greeks & Market Risk"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, greeks, risk-management]
---
## Definition
The **Greeks** are measures of the sensitivity of a derivative's (or portfolio's) value to the primary factors driving it: the underlying asset price, time, volatility, and the interest rate. They are used on a micro-level to manage market risk. Effects on option prices are qualitatively motivated before the Greeks are formalised: call values rise with $S$ and fall with $K$; both calls and puts rise in value with volatility $\sigma$; longer time-to-expiry raises American option value; dividends reduce call value and raise put value.

## Properties
### Delta ($\Delta$)
The first-order sensitivity of a derivative price to the underlying:
$$
\Delta = \frac{\partial c}{\partial S}.
$$
For a European call on a non-dividend stock, $\Delta_c=N(d_1)>0$; for the corresponding put (via [[Put-call parity]]), $\Delta_p=N(d_1)-1=-N(-d_1)<0$. For a portfolio $\Pi$, $\Delta_\Pi=\partial\Pi/\partial S$.

**Proof (of $\Delta_c=N(d_1)$).** Differentiate $c=SN(d_1)-Ke^{-rT}N(d_2)$ w.r.t. $S$:
$$
\Delta = N(d_1) + SN'(d_1)\frac{\partial d_1}{\partial S} - Ke^{-rT}N'(d_2)\frac{\partial d_2}{\partial S}.
$$
Since $\partial d_1/\partial S=\partial d_2/\partial S=\frac{1}{S\sigma\sqrt T}$, this becomes $\Delta=N(d_1)+\frac{1}{S\sigma\sqrt T}\left\{SN'(d_1)-Ke^{-rT}N'(d_2)\right\}$. The key lemma $SN'(d_1)=Ke^{-rT}N'(d_2)$ follows from $\frac{N'(d_1)}{N'(d_2)}=e^{-\frac12(d_1^2-d_2^2)}=e^{-\frac12(d_1+d_2)(d_1-d_2)}=e^{-r T}\frac{K}{S}$ (using $d_1-d_2=\sigma\sqrt T$ and $d_1+d_2=\frac{2\ln(S/K)+2rT}{\sigma\sqrt T}$). This makes the bracketed term vanish, leaving $\Delta=N(d_1)$. $\blacksquare$ (With a continuous dividend yield $q$: $\Delta_c=e^{-qT}N(d_1)$.)

### Delta hedging
"Delta-neutral" means $\Delta_\Pi=0$: a portfolio momentarily insensitive to small moves in $S$. Example: if a call's price moves \$0.50 for every \$1 move in the stock ("two for one"), hedge 100 short calls with 50 shares. This dynamic strategy requires continuous re-balancing as $\Delta$ itself changes (**hedge slippage**, and significant transaction costs, are its main drawbacks — see [[Hedging]]).

### Gamma ($\Gamma$)
The curvature of the derivative's value — the rate of change of $\Delta$ with respect to $S$:
$$
\Gamma = \frac{\partial^2c}{\partial S^2} = \frac{\partial\Delta}{\partial S} = \frac{N'(d_1)}{S\sigma\sqrt T}, \qquad N'(d_1)=\frac{e^{-d_1^2/2}}{\sqrt{2\pi}}.
$$
$\Gamma$ is identical for a call and the corresponding put. High $\Gamma$ means $\Delta$ is very sensitive to $S$, requiring frequent re-hedging to stay delta-neutral. A **gamma-neutral** portfolio is built by adding $\lambda=-\Gamma/\Gamma'$ units of a second traded option (gamma $\Gamma'$) — this changes the portfolio's $\Delta$, requiring a further adjustment in the underlying to restore delta-neutrality; gamma-neutrality is itself only instantaneous.

### Theta ($\Theta$)
Sensitivity to the passage of time:
$$
\Theta_\Pi = \frac{\partial\Pi}{\partial t} = -\frac{\partial\Pi}{\partial\tau}, \qquad \tau=T-t,
$$
$$
\Theta_{\text{call}} = -\frac{S_0N'(d_1)\sigma}{2\sqrt T}-rKe^{-rT}N(d_2), \qquad \Theta_{\text{put}} = -\frac{S_0N'(d_1)\sigma}{2\sqrt T}+rKe^{-rT}N(-d_2).
$$

### Vega ($\nu$) and Rho ($\rho$)
$$
\nu_\Pi=\frac{\partial\Pi}{\partial\sigma}, \qquad \rho_\Pi=\frac{\partial\Pi}{\partial r}.
$$
For a call, $\nu_c = S\sqrt T\,N'(d_1) > 0$: call prices increase monotonically with volatility (see [[Implied Volatility]]).

### Unifying identity
Rewriting the [[Black-Scholes model|Black-Scholes PDE]] $\frac{\partial c}{\partial t}+\tfrac12\sigma^2S^2\frac{\partial^2c}{\partial S^2}+rS\frac{\partial c}{\partial S}=rc$ in terms of the Greeks gives
$$
\Theta + \tfrac12\sigma^2S^2\Gamma + rS\Delta = rc.
$$
This ties the Greeks directly back to the no-arbitrage replicating-portfolio argument of [[Black-Scholes model]].

## Examples
$S_0=100,K=100,r=5\%,\sigma=40\%,\tau=4/12$: $d_1=0.1876$, so $\Delta_c=N(d_1)=0.5728$ (a \$1 move in $S$ changes the call price by about \$0.5728).

Delta-hedging table (selling calls on 1,000 shares of XYZ, $S=50,K=40,r=5\%,\sigma=30\%,\tau=1$): $d_1\approx1.060\Rightarrow\Delta\approx0.8554\Rightarrow$ buy 855 shares initially; as $S$ and $\tau$ change week to week, $\Delta$ (and the required share holding) must be re-computed and the position rebalanced.

## See also
[[Black-Scholes formula]], [[Black-Scholes model]], [[Hedging]], [[Implied Volatility]], [[Volatility (Financial)]]
