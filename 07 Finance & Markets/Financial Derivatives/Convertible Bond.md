---
title: "Convertible Bond"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "PGT Lectures - Warrants and Convertible Bonds"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, convertible-bonds, embedded-options]
---
## Definition
A **convertible bond** embeds a [[Warrant]] into a bond: the holder has the right to exchange the bond's maturity payment $M$ for shares instead. Notation: $n$ bonds each with maturity value $M$, each convertible into $p$ shares, $m$ original shares outstanding, $A_T$ the firm's asset value at maturity $T$.

## Properties
### Conversion decision
If all $n$ bonds convert, total shares become $m+np$. Conversion occurs at maturity iff the per-share value after conversion exceeds the per-bond maturity value expressed per share:
$$
\frac{A_T}{m+np} > \frac{M}{n} \quad\Longleftrightarrow\quad A_T > M\!\left(1+\frac{m}{np}\right).
$$
If the convertible bond is the firm's only debt, bankruptcy occurs if $A_T-nM<0$ (mirroring [[Merton Model (Credit Risk)|Merton's default condition]]).

### Payoff decomposition
The payoff of a single convertible bond at $T$ is
$$
\text{Payoff} = \max\!\left\{M-\frac{A_T}{n},0\right\} + p\cdot\max\!\left\{\frac{A_T}{m+np}-\frac Mn,0\right\}.
$$
This decomposes into: **a straight bond**, **minus a written European put** (on the firm's assets, capturing default risk — see [[Merton Model (Credit Risk)]]), **plus purchased warrants** (capturing the conversion option). Hence the value at $t=0$ is
$$
nMe^{-rT} - p_0(A,nM,\sigma,r,T) + np\cdot c_0\!\left(\frac An,\frac Mn,\sigma,r,T\right),
$$
with $p_0,c_0$ the [[Black-Scholes formula|Black-Scholes put/call prices]].

## Examples
Firm assets £10,000, six ZCBs of £1,000 face value each ($T=5$yr), $\sigma=30\%$, $r=6\%$, each bond convertible into 50 shares, 400 shares outstanding. Debt value $=6000e^{-0.3}-p_0(10000,6000,0.3,0.06,5)+6\times50\,c_0(25,20,0.3,0.06,5) = £5{,}276.35$; each bond is worth $£879.39$ (yield $2.57\%$); equity value $=\frac{10000-5276.35}{400}=£11.81$ per share.

## See also
[[Warrant]], [[Merton Model (Credit Risk)]], [[Black-Scholes formula]], [[Put option]]
