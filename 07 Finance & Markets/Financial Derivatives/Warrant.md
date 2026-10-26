---
title: "Warrant"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "PGT Lectures - Warrants and Convertible Bonds"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, warrants, embedded-options]
---
## Definition
A **warrant** is a long-term [[European Options|European call option]] issued by a company on its **own** shares. Unlike an exchange-traded call (a third-party contract), exercising a warrant *creates new shares* — increasing the shares outstanding and diluting existing shareholders. Notation: $n$ = shares outstanding, $m$ = warrants outstanding (strike $K$), $A$ = total asset value of the company.

## Properties
### Dilution adjustment to value
If a warrant is exercised, the holder pays $K$ and receives one new share; after exercise the firm is worth $A+mK$, so each share (of the now $n+m$ shares) is worth $\frac{A+mK}{n+m}$, and the payoff per warrant is
$$
\frac{A+mK}{n+m}-K = \frac{A-Kn}{n+m}.
$$
Writing $S=A/n$ (the per-share value *absent* warrants), this simplifies to $\frac{m}{n+m}\max\{S-K,0\}$: the warrant is worth exactly $\frac{m}{n+m}$ of an ordinary call, reflecting the dilution.

### Valuation formula
$$
\text{Warrant value} = \frac{m}{n+m}\,c_0(A,K,r,\sigma,T),
$$
where $c_0$ is the ordinary [[Black-Scholes formula|Black-Scholes call price]] (evaluated on the firm's asset value $A$).

## See also
[[Convertible Bond]], [[Call option]], [[Black-Scholes formula]]
