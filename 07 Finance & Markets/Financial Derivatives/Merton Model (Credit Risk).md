---
title: "Merton Model (Credit Risk)"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "Chapter 10 - Credit Risk"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, credit-risk, merton, structural-model]
---
## Definition
Merton's model (Merton, 1974) is the classical **structural** approach to [[Credit Risk]]. A firm's value decomposes as
$$
F(t) = B(t) + E(t),
$$
where $F$ is total firm value, $B$ the value of its debt (a single zero-coupon bond, face value $L$, maturity $T$; debtholders rank above shareholders), and $E$ the value of its equity. No dividends or coupons are assumed. The firm defaults if $F(T)<L$: bondholders then receive $F(T)$ (instead of the promised $L$) and shareholders receive nothing.

## Properties
### Equity as a call option
The equity payoff at maturity is
$$
E(T) = \max\{F(T)-L,\,0\}.
$$
This is exactly the payoff of a European call option on the firm's assets, with strike price equal to the debt $L$ and maturity $T$. So Merton's model treats shareholders as holding a call option on the firm's asset value, and the [[Black-Scholes formula]] applies directly:
$$
E_0 = F(0)N(d_1)-Le^{-rT}N(d_2), \qquad d_1=\frac{\ln(F(0)/L)+(r+\tfrac12\sigma^2)T}{\sigma\sqrt T},\quad d_2=d_1-\sigma\sqrt T,
$$
with $\sigma$ the volatility of the firm's asset value $F$.

### Risk-neutral default probability
The probability of bankruptcy at $T$ (under $Q$), conditional on the assets' value at $t$, is
$$
Q(F(T)<L\mid F(t)) = N(-d_2).
$$

### Credit spread
The excess yield on a risky (corporate) bond over the risk-free rate is the **credit spread**, closely related to the expected cost of default (and, in practice, also compensating for liquidity risk); the corporate bond price is lower than an otherwise-identical risk-free bond, equivalently its yield is higher.

### Distance to default (real-world measure)
Let $F(t)$ follow $dF(t)=\alpha F(t)\,dt+\sigma F(t)\,dW_t$ under the **real-world** measure $P$ ($\alpha$ the expected asset return). The real-world default probability is
$$
P(F(T)<L\mid F(t)) = N(-\tilde d_2), \qquad \tilde d_2 = \frac{\ln(F(t)/L)+(\alpha-\tfrac12\sigma^2)(T-t)}{\sigma\sqrt{T-t}}.
$$
Since $E^P[\ln F(T)] = \ln F(t)+(\alpha-\tfrac12\sigma^2)(T-t)$, define the **distance to default** as this expectation's distance from the bankruptcy threshold $\ln L$, in standard-deviation units:
$$
\text{Distance to default} = \frac{E^P[\ln F(T)]-\ln L}{\sigma\sqrt{T-t}} = \tilde d_2,
$$
so the real-world default probability is $N(-\text{distance to default})$.

## Examples
Firm value $F(t)=\$60$, debt $L=\$70$ (3-year ZCB), $\sigma=10\%$, $r=5\%$. Risk-neutral: $d_2=-0.1106\Rightarrow Q(\text{default})=N(0.1106)=54.40\%$; equity value $E_t=60N(0.0626)-70e^{-0.15}N(-0.1106)=\$4.03$. Real-world (with $\alpha=9\%$): $\tilde d_2=0.5823\Rightarrow P(\text{default})=N(-0.5823)=28.02\%$. The risk-neutral default probability (54.40%) exceeds the real-world one (28.02%) because assets grow more slowly under the risk-neutral measure ($r<\alpha$).

## See also
[[Credit Risk]], [[Black-Scholes formula]], [[Reduced-Form Credit Risk Model]], [[Terminal Share Price Distribution]]
