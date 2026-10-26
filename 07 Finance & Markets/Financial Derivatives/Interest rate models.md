---
title: "Interest rate models"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "Chapter 9 - Interest Rate Models"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, interest-rate-models, term-structure]
---
## Definition
A **term structure model** describes how interest rates evolve over time and relate to maturities. Key notation:
- $B(t,T)$ — price at $t$ of a zero-coupon bond (ZCB) maturing at $T$, paying \$1;
- $r(t)$ — instantaneous risk-free (short) rate at $t$;
- $C(t)=e^{\int_0^t r(u)\,du}$ — the cash/money-market account (accumulated value at $t$ of \$1 invested at $0$), satisfying $dC(t)=r(t)C(t)\,dt$;
- $F(t,T,S)$ — forward rate at $t$ for delivery between $T$ and $S$; $f(t,T)=\lim_{S\to T}F(t,T,S)$ — the **instantaneous forward rate**;
- $R(t,T)$ — the **spot rate** associated with the ZCB $B(t,T)$.

A **one-factor model** assumes the short rate is driven by a single source of randomness: $dr_t=a(t,r_t)\,dt+b(t,r_t)\,dW_t$.

## Properties
### Spot/forward-rate relationships
$$
R(t,T) = -\frac{1}{T-t}\ln B(t,T) \quad\Longleftrightarrow\quad B(t,T)=e^{-R(t,T)(T-t)},
$$
$$
f(t,T) = -\frac{\partial}{\partial T}\ln B(t,T), \qquad B(t,T)=\exp\left\{-\int_t^Tf(t,u)\,du\right\}.
$$
So the spot rate is (in a precise sense) an average of the forward rates: $R(t,T)=\frac{1}{T-t}\int_t^Tf(t,u)\,du$.

### Desirable characteristics of a model
A term-structure model should: be arbitrage-free; keep interest rates positive; have the short rate display mean-reverting behaviour; be easy to calculate with; be reasonably realistic; fit historical data well; be easy to calibrate; and be flexible.

### Risk-neutral bond pricing
By an argument analogous to [[Black-Scholes model|Black-Scholes]]:
$$
B(t,T) = E^Q\!\left[e^{-\int_t^Tr(u)\,du}\ \middle|\ \mathcal F_t\right],
$$
and a derivative with payoff $X$ contingent on the bond has value $V_t=E^Q\!\left[e^{-\int_t^ur(v)\,dv}X\mid\mathcal F_t\right]$.

### Market price of risk
Under the real-world measure $P$, a ZCB of maturity $T_1$ follows $dB(t,T_1)=B(t,T_1)\{m(t,T_1)\,dt+S(t,T_1)\,dW_t\}$. The **market price of risk** is
$$
\gamma(t,T_1) = \frac{m(t,T_1)-r(t)}{S(t,T_1)},
$$
and the **risk premium** on the bond is $\gamma(t,T_1)S(t,T_1)=m(t,T_1)-r(t)$. In a one-factor model, $\gamma(t,T_1)=\gamma(t)$ is the same for every maturity $T_1$ — a single market price of risk prices every bond. [[Girsanov theorem|Girsanov's theorem]] then changes $dW_t\to dW_t^*=dW_t+\gamma(t)dt$ to move from $P$ to the risk-neutral measure $Q$, transforming the short-rate SDE $dr_t=a\,dt+b\,dW_t$ (under $P$) into $dr_t=(a-\gamma b)\,dt+b\,dW_t^*$ (under $Q$).

### The pricing kernel approach
An alternative: specify a strictly positive diffusion (pricing kernel/deflator) $A_t$ with $dA_t=A_t\{\mu_A(t)\,dt+\sigma_A(t)\,dW_t\}$ under $P$; then $B(t,T)=A_t^{-1}E^P\!\left[A_T\mid\mathcal F_t\right]$. Example: if $A_t$ is deterministic with $\mu_A(t)=-\delta$, $\sigma_A(t)=0$, then $A_t=ke^{-\delta t}$ and $B(t,T)=e^{-\delta(T-t)}$ — a constant short rate $\delta$. (The pricing-kernel and risk-neutral approaches look very different but are equivalent; the connection is via the Radon-Nikodym derivative.)

### Comparison of short-rate models

| Model | Dynamics | $r_t>0\ \forall t$ | Distribution of $r_t$ |
|---|---|---|---|
| [[Vasicek Model]] | $dr_t=\alpha(\mu-r_t)dt+\sigma\,dW_t$ | No | Normal |
| [[Cox-Ingersoll-Ross (CIR) Process]] | $dr_t=\alpha(\mu-r_t)dt+\sigma\sqrt{r_t}\,dW_t$ | Yes | Non-central $\chi^2$ |
| [[Hull-White Model]] | $dr_t=\alpha(\mu(t)-r_t)dt+\sigma\,dW_t$ | No | Normal |
| Hull-White + CIR | $dr_t=\alpha(\mu(t)-r_t)dt+\sigma\sqrt{r_t}\,dW_t$ | Yes | Non-central $\chi^2$ |

### Shortcomings of one-factor models
All maturities are driven by the *same* single source of randomness, so bonds of different maturities move perfectly (locally) correlated — unrealistic, and unsuitable for pricing swaptions and similar products that depend on the *relationship* between rates of different maturities. There is little consistency between different models' valuations, and one-factor models are difficult to calibrate. Historically, both interest rates and volatility exhibit clustering (a low-volatility period tends to be followed by a low-volatility period) that a single source of randomness cannot capture. These limitations motivate **multi-factor models** (outside the scope of this module).

## See also
[[Vasicek Model]], [[Cox-Ingersoll-Ross (CIR) Process]], [[Hull-White Model]], [[Girsanov theorem]], [[Swap contract]]
