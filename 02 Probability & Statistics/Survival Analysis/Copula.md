---
title: "Copula"
domain: Probability & Statistics
course: Survival Analysis
unit: "Chapter 10 - Copulas & Measures of Association"
level: MSc
status: drafted
confidence: 0
tags: [survival-analysis, copulas, dependence-modelling]
---
## Definition
For two random variables $X,Y$, the [[Joint distribution|joint cdf]] $F_{X,Y}(x,y)=P(X\leq x,Y\leq y)$ has margins $F_X(x)=\lim_{y\to\infty}F_{X,Y}(x,y)$ and $F_Y(y)=\lim_{x\to\infty}F_{X,Y}(x,y)$. Specifying a joint pdf directly is hard outside special cases (e.g. the multivariate normal), and the relationship between the joint and the marginals is not transparent. A **copula** solves this by separating dependence structure from marginal behaviour.

**Definition (copula).** A copula $C(u,v)$ is a joint cdf of a random vector $(U,V)$ on $[0,1]^2$ with uniform marginals $C_U(u)=u$ and $C_V(v)=v$ on $[0,1]$. Formally, $C:[0,1]^2\to[0,1]$ satisfies:
1. $C(u,0)=C(0,u)=0$ and $C(u,1)=C(1,u)=u$ for all $u\in[0,1]$.
2. **2-increasing**: for $u_1\leq u_2$, $v_1\leq v_2$, $C(u_2,v_2)-C(u_2,v_1)-C(u_1,v_2)+C(u_1,v_1)\geq0$.

(A $d$-dimensional copula generalises this to a joint cdf of $(U_1,\dots,U_d)$ on $[0,1]^d$ with uniform marginals.)

Given univariate cdfs $F_1,F_2$ and a copula $C$, one builds a bivariate cdf via $F(x,y)=C(F_1(x),F_2(y))$: $C$ "couples" the marginals into a joint distribution, and contains the entire dependence structure between $X$ and $Y$.

## Properties
### Sklar's theorem (1959)
**Theorem.** Let $F(x,y)$ be a bivariate cdf with margins $F_1(x)$, $F_2(y)$. Then there exists a copula $C$ such that $F(x,y)=C(F_1(x),F_2(y))$ for all $x,y$.

Sklar's theorem separates $F$ into $C$ (the dependence structure) and $F_1,F_2$ (the marginal behaviours). If $F_1,F_2$ are continuous, $C$ is uniquely
$$
C(u,v) = F\left(F_1^{-1}(u), F_2^{-1}(v)\right), \qquad F_i^{-1}(u)=\inf\{x: F_i(x)\geq u\}
$$
This is called the **copula function** of $X,Y$.

### Example: Exponential margins with independence copula
Let $F(x,y) = (1-e^{-x})(1-e^{-y})$ for $x,y\geq0$. Margins: $F_1(x)=1-e^{-x}$, $F_2(y)=1-e^{-y}$, with inverses $F_1^{-1}(u)=-\ln(1-u)$, $F_2^{-1}(v)=-\ln(1-v)$. Then
$$
C(u,v) = F(F_1^{-1}(u),F_2^{-1}(v)) = [1-e^{\ln(1-u)}][1-e^{\ln(1-v)}] = [1-(1-u)][1-(1-v)] = uv
$$

### Fundamental copulas
Three fundamental copulas represent the basic possible dependence structures:
1. **Independence copula**: $\Pi(u,v)=uv$. If $F_X,F_Y$ are the margins, $F_{X,Y}(x,y)=\Pi(F_X(x),F_Y(y))=F_X(x)F_Y(y)$ — independence.
2. **Minimum (comonotonicity) copula**: $M(u,v)=\min(u,v)$, expressing **perfect positive dependence**. If $Y=cX+a$ with $c>0$ (take $c=1$): $P(X\leq x,Y\leq y)=P(X\leq\min(x,y-a))=\min(P(X\leq x),P(X\leq y-a))=\min(P(X\leq x),P(Y\leq y))$.
3. **Maximum (countermonotonicity) copula**: $W(u,v)=\max(u+v-1,0)$, expressing **perfect negative dependence**. If $Y=cX+a$ with $c<0$ (take $c=-1$): $P(X\leq x,Y\leq y)=P(X\leq x,X\geq a-y)=P(a-y\leq X\leq x)=P(X\leq x)-P(X\leq a-y)=P(X\leq x)+P(Y\leq y)-1$.

Note: all three generalise to $d>2$ dimensions except $W$, since it is not possible to have three or more variables each pairwise perfectly negatively related.

### Fréchet–Hoeffding bounds
**Theorem.** For every copula $C$ and every $(u,v)\in[0,1]^2$:
$$
W(u,v) \leq C(u,v) \leq M(u,v)
$$
**Corollary.** For a bivariate cdf $F$ with margins $F_1,F_2$: $\max(F_1(x)+F_2(y)-1,0) \leq F(x,y) \leq \min(F_1(x),F_2(y))$.

### Copula density
If $C(u,v)$ is differentiable, its **copula density** is $c(u,v) = \dfrac{\partial^2 C(u,v)}{\partial u\,\partial v}$. E.g. $\Pi(u,v)=uv$ has density $c(u,v)=1$ (the reference "no association" plane $z=1$); comparing $c(u,v)$ to this plane gives a localised view of association — values far from $1$ indicate strong local association, values close to $1$ indicate weak local association at that $(u,v)$.

## See also
[[Archimedean Copula]], [[Gaussian Copula]], [[Measures of Association]], [[Tail Dependence]], [[Joint distribution]]
