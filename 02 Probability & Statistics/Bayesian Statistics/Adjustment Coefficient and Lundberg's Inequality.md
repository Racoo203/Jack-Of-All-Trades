---
title: "Adjustment Coefficient and Lundberg's Inequality"
domain: "Probability & Statistics"
course: "Bayesian Statistics"
unit: "Chapter 8 - Risk Theory"
level: MSc
status: drafted
confidence: 0
tags: [bayesian-statistics, actuarial, risk-theory]
---
## Definition
For a [[Ruin Theory|ruin process]] with claims $X\ge0$, $E[X]=\mu_1>0$, the **adjustment coefficient** $R$ is the positive root of
$$
\lambda + cR = \lambda\, m_X(R)
$$
equivalently (writing $S$ for total claims in a unit interval, compound Poisson with mgf $m_S(R)=\exp\{\lambda(m_X(R)-1)\}$): $e^{Rc}=E[e^{RS}] \iff Rc=\log m_S(R) \iff \lambda+cR=\lambda m_X(R)$.

**Theorem (Lundberg's inequality).** For a compound Poisson risk process with initial capital $u$, premium rate $c$, claim mgf $m_X$, and adjustment coefficient $R$,
$$
\psi(u) \le e^{-Ru}
$$

## Properties
### Existence of a positive root
Let $g(r)=\lambda m_X(r)-\lambda-cr$. Then $g(0)=0$ (since $m_X(0)=1$); $g'(0)=\lambda\mu_1-c<0$ (using the loading condition $c>\lambda\mu_1$); and $g''(r)=\lambda E[X^2e^{rX}]>0$, so $g$ is convex with $g'(0)<0$. Since $m_X(r)\to\infty$ as $r$ approaches the boundary $\gamma$ of its domain of existence, $g(r)\to\infty$ for some $r<\gamma$, so by continuity and convexity there is exactly one root $R>0$ (besides the trivial root at $0$).

### Proof of Lundberg's inequality (induction on claim number)
Let $\psi_k(u)$ be the probability of ruin at or before the $k$-th claim; $\psi_k(u)\uparrow\psi(u)$. Base case $k=0$: $\psi_0(u)=\mathbb 1[u<0] \le e^{-Ru}$ trivially (holds for $u\ge0$; for $u<0$ ruin is immediate and the bound is a convention). Conditioning on the time $t$ and size $x$ of the first claim:
$$
\psi_k(u) = \int_0^\infty\int_0^\infty \psi_{k-1}(u+ct-x)\,dP(x)\,\lambda e^{-\lambda t}\,dt
$$
Assuming the inductive hypothesis $\psi_{k-1}(u)\le e^{-Ru}$ for all $u$:
$$
\psi_k(u) \le \int_0^\infty\int_0^\infty e^{-R(u+ct-x)}\,dP(x)\,\lambda e^{-\lambda t}\,dt
= e^{-Ru}\int_0^\infty \lambda e^{-t(\lambda+Rc)}\,dt \int_0^\infty e^{Rx}\,dP(x)
= e^{-Ru}\cdot\frac{\lambda}{\lambda+cR}\,m_X(R) = e^{-Ru}
$$
using the defining equation $\lambda+cR=\lambda m_X(R)$ in the last step. By induction, $\psi_k(u)\le e^{-Ru}$ for all $k$, hence $\psi(u)=\lim_k\psi_k(u)\le e^{-Ru}$. $\blacksquare$

## Examples
### Worked derivation: exponential claims
$X\sim\text{Exp}(\alpha)$: $\mu_1=1/\alpha$, $m_X(t)=\frac{\alpha}{\alpha-t}$. Substituting into $\lambda+cR=\lambda m_X(R)$:
$$
\lambda\alpha = (\lambda+cR)(\alpha-R) = \lambda\alpha + (c\alpha-\lambda)R - cR^2 \implies (c\alpha-\lambda)R - cR^2 = 0
$$
so $R=0$ or $R=\alpha-\lambda/c$. Since $c>\lambda\mu_1=\lambda/\alpha$, the second root is positive, so $R=\alpha-\lambda/c$, and using $c=(1+\theta)\lambda/\alpha$:
$$
\psi(u) \le e^{-(\alpha-\lambda/c)u} = e^{-\frac{\theta\alpha}{1+\theta}u}
$$
— the ruin-probability bound decays exponentially in both the initial capital $u$ and the premium loading $\theta$.

## See also
[[Ruin Theory]], [[Collective Risk Model]], [[Moment Generating Function]]
