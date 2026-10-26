---
title: "American Options"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "Chapter 4 - Financial Markets; Chapter 5 - Binomial Trees"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, options, early-exercise]
---
## Definition
An **American option** differs from a [[European Options|European option]] only in that it may be exercised **at any time up to (and including) the expiry date**, not just at expiry. At expiry, its value equals the corresponding European option's value; before expiry it must be tested at each point in time (or, in a [[Binomial option pricing model|binomial tree]], at each node) for whether **early exercise** is optimal. Unlike European options, American options require margin payments from the writer.

Notation: lowercase $c,p$ for European call/put prices; uppercase $C,P$ for American call/put prices. Since American options grant a strict superset of exercise opportunities, $C\ge c$ and $P\ge p$.

## Properties
### Pricing on a binomial tree
At each node before expiry, the value of the American option is the **greater of**:
1. the value implied by risk-neutral continuation (as for the European option, equation $f_0=e^{-r\delta T}\{qf_1^0+(1-q)f_1^1\}$ — see [[Binomial option pricing model]]), and
2. the payoff from immediate exercise.

### Theorem — early exercise of an American call on a non-dividend-paying stock is never optimal
Hence $C=c$ for a non-dividend-paying underlying.

**Proof (portfolio argument).** Compare:
- **Portfolio A**: one American call plus cash $Ke^{-r(T-t)}$;
- **Portfolio B**: one share of the stock.

If the call is exercised early at $\tau<T$, Portfolio A is worth $S_\tau - K + Ke^{-r(T-\tau)} < S_\tau$ (since $Ke^{-r(T-\tau)}<K$) — worse than simply holding the stock (Portfolio B). If instead the call is held to maturity, Portfolio A is worth $\max\{S_T,K\}\ge S_T=$ Portfolio B's value. Since holding to maturity dominates exercising early in every comparison, early exercise destroys value, and an American call on a non-dividend-paying stock should never be exercised before $T$. $\blacksquare$

For American **puts**, early exercise *can* be optimal (receiving the strike early can be valuable), so in general $P>p$.

### Dividends can make early exercise of a call optimal
If the underlying pays discrete dividends $D_1,\dots,D_n$ at ex-dividend dates $t_1<\dots<t_n<T$, it is optimal to exercise **only** (if at all) immediately before an ex-dividend date. Exercise just before $t_k$ is not optimal if
$$
D_k \le K\left\{1-e^{-r(t_{k+1}-t_k)}\right\} \approx Kr(t_{k+1}-t_k) \quad \text{(for small } t_{k+1}-t_k\text{)}.
$$
So in practice only the **final** ex-dividend date $t_n$ needs checking. **Black's approximation** (Black, 1975) prices the American call as the greater of two European call values: one maturing at $T$, one maturing just before $t_n$ (using the dividend-adjusted stock price at each).

**Example.** Ex-dividend dates in 2 and 5 months, dividend 50c each, $S_0=K=\$40$, $\sigma=30\%$, $r=9\%$, $T=6$ months. Checking $K\{1-e^{-r(t_2-t_1)}\}=0.89>0.5=D_2$: not optimal to exercise at $t_1$; checking $K\{1-e^{-r(T-t_2)}\}=0.30<0.5=D_2$: exercising at $t_2$ can be optimal. Black's approximation takes $\max(\$3.52,\$3.67)=\$3.67$.

## See also
[[European Options]], [[Call option]], [[Put option]], [[Binomial option pricing model]], [[Bounds for Option Prices]], [[Garman-Kohlhagen Formula]]
