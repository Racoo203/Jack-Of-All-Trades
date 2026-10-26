---
title: "Binomial option pricing model"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "Chapter 5 - Binomial Trees"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, binomial-trees, risk-neutral-pricing]
---
## Definition
The **binomial tree model** prices a [[Derivative contract]] by assuming the underlying asset price can only take a finite number of values, moving in discrete time steps. It uses [[No-arbitrage principle|no-arbitrage]] and [[Replicating Portfolio|replication]] to find a fair value, and introduces the **synthetic (risk-neutral) probability**: a "probability" that is not physical but conveniently prices the derivative as if the market were risk-neutral.

## Properties
### One-step binomial model
Let a non-dividend stock $S_0$ move, after time $\delta T$, either up to $S_1^0=uS_0$ (derivative payoff $f_1^0$) or down to $S_1^1=dS_0$ (payoff $f_1^1$). Construct a portfolio: long $\Delta$ shares, short one derivative. Its value at $T$ is $\Delta uS_0-f_1^0$ or $\Delta dS_0-f_1^1$. Making it **riskless** (both outcomes equal) gives
$$
\Delta = \frac{f_1^0-f_1^1}{(u-d)S_0}.
$$
Discounting the (now-certain) portfolio value at the risk-free rate $r$ and solving for $f_0$:
$$
f_0 = e^{-r\delta T}\left\{q f_1^0 + (1-q)f_1^1\right\}, \qquad q=\frac{e^{r\delta T}-d}{u-d}.
$$
$q$ does **not** involve the real-world (physical) probability of an up-move — it is the **risk-neutral probability**, and $q\in(0,1)$ requires $d<e^{r\delta T}<u$ (see [[Equivalent Probability Measures]]).

**Example.** $S_0=\$20$, up to \$22 or down to \$18 in 4 months, strike \$21, $r=12\%$. Then $\Delta=\frac{1-0}{22-18}=0.25$, and hedging gives $f_0=0.676$ — the fair call price is 67.6c.

### Replicating strategy
Equivalently, find $\phi$ (units of stock) and $\psi$ (units of a \$1 bond) with $V_0=\phi S_0+\psi$ such that $V_1$ matches the derivative's payoff in both states: $\phi S_1^0+\psi e^{r\delta T}=f_1^0$, $\phi S_1^1+\psi e^{r\delta T}=f_1^1$. Solving these two equations and setting $f_0=V_0=\phi S_0+\psi$ recovers the same price. See [[Replicating Portfolio]], [[Self-Financing Strategy]].

### Multi-step extension
Using $u,d$ fixed across steps, after $n$ steps,
$$
f_0 = e^{-rn\delta T}\sum_{k=0}^n \binom{n}{k}q^k(1-q)^{n-k}\,f\!\left(S_0u^kd^{n-k}\right).
$$
For a two-step tree this is $f_0=e^{-2r\delta T}\{q^2f_2^{00}+2q(1-q)f_2^{01}+(1-q)^2f_2^{11}\}$.

### American options on the tree
See [[American Options]]: at each node before expiry, take the greater of the risk-neutral continuation value and the immediate-exercise payoff, working backward from expiry.

### Cox-Ross-Rubinstein (CRR) parameterization
CRR (1979) calibrate $u,d$ to a target [[Volatility (Financial)|volatility]] $\sigma$ (defined so $\sigma^2\delta T$ is the variance of the stock return over $\delta T$). Matching the tree's mean and variance to the real-world lognormal model (with real-world up-probability $p$, $E$-value $S_0e^{\mu\delta T}$) and expanding to first order in $\delta T$ gives
$$
u = e^{\sigma\sqrt{\delta T}}, \qquad d = e^{-\sigma\sqrt{\delta T}} = \frac1u.
$$
Remarkably, checking the risk-neutral variance with the same $u,d$ (replacing $p$ by $q$, $\mu$ by $r$) reproduces the *same* $\sigma^2\delta T$ to first order: moving from the real-world to the risk-neutral measure changes the expected return but **not** the volatility — an instance of [[Girsanov theorem|Girsanov's theorem]].

## Examples
Two-year European put, $K=52$, $S_0=50$, $u=1.2,d=0.8$, $r=5\%$, $q=0.6282$: $f_0 = e^{-0.1}\{0.6282^2(0)+2(0.6282)(0.3718)(4)+0.3718^2(20)\}=4.1923$. As an **American** put on the same tree, testing early exercise at each node raises the value to $5.0894$.

## See also
[[Replicating Portfolio]], [[Self-Financing Strategy]], [[Complete and Incomplete Financial Markets]], [[Volatility (Financial)]], [[American Options]], [[Black-Scholes model]], [[Equivalent Probability Measures]]
