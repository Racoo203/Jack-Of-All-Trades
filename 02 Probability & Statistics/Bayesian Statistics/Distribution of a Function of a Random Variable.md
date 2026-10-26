---
title: "Distribution of a Function of a Random Variable"
domain: "Probability & Statistics"
course: "Bayesian Statistics"
unit: "Chapter 1 - Preliminary"
level: MSc
status: drafted
confidence: 0
tags: [bayesian-statistics, foundations]
---
## Definition
Given $X \sim f_X(x)$ (or [[Cumulative Distribution Function (CDF) | CDF]] $F_X(x)$) and a real-valued function $g$, $Y=g(X)$ is itself a [[Random Variable]]; the problem is to find its distribution $f_Y(y)$ from $f_X(x)$ and $g$.

## Properties
### Change-of-variable formula (single monotone branch)
**Theorem.** Let $X$ have pdf $f_X(x)$ with support $B=\{x:f_X(x)>0\}$, and let $g$ be strictly monotone on $B$ with differentiable inverse $g^{-1}$. Then $Y=g(X)$ has density
$$
f_Y(y) = f_X(g^{-1}(y))\left|\frac{d}{dy}g^{-1}(y)\right|, \qquad y=g(x),\ x\in B
$$
**Proof.** The cdf of $Y$ is $F_Y(y)=P(Y\le y)=P(g(X)\le y)=P(X\le g^{-1}(y))=F_X(g^{-1}(y))$ (for $g$ increasing). Differentiating with the chain rule,
$$
f_Y(y) = \frac{dF_Y(y)}{dy} = \frac{dF_X(g^{-1}(y))}{d\,g^{-1}(y)}\cdot\frac{d}{dy}g^{-1}(y) = f_X(g^{-1}(y))\left|\frac{d}{dy}g^{-1}(y)\right|
$$

### General case (piecewise monotone)
If the support $B=\cup_k I_k$ where $g$ is strictly monotone on each interval $I_k$, with inverses $g_k^{-1}$ differentiable, then
$$
f_Y(y) = \begin{cases}\sum_k f_X(g_k^{-1}(y))\left|\dfrac{d}{dy}g_k^{-1}(y)\right| & y=g(x),\ x\in B \\ 0 & \text{otherwise}\end{cases}
$$

## Examples
### $Y=X^n$, $X\sim U[0,1]$
$F_Y(y)=P(X^n\le y)=P(X\le y^{1/n})=F_X(y^{1/n})=y^{1/n}$ for $y\in[0,1]$, so $f_Y(y)=\frac{1}{n}y^{1/n-1}$.

### $Y=X^2$ (piecewise monotone example)
$g(x)=x^2$ is strictly decreasing on $I_1=(-\infty,0]$ and strictly increasing on $I_2=(0,\infty)$, with inverses $g_1^{-1}(y)=-\sqrt y$, $g_2^{-1}(y)=\sqrt y$. Applying the general formula:
$$
f_Y(y) = \frac{1}{2\sqrt y}\left[f_X(-\sqrt y) + f_X(\sqrt y)\right], \qquad y>0
$$
and $f_Y(y)=0$ for $y<0$ since $Y=X^2$ cannot be negative. (Directly: $F_Y(y)=P(-\sqrt y\le X\le\sqrt y)=F_X(\sqrt y)-F_X(-\sqrt y)$ for $y>0$, differentiate to confirm.)

### Sum of two i.i.d. standard exponentials
For $X_1,X_2$ i.i.d. $\text{Exp}(1)$, $Y=X_1+X_2$ has $F_Y(y)=1-e^{-y}-ye^{-y}$ (via conditioning on $X_2$ and integrating), so $f_Y(y)=ye^{-y}$ — a $\text{Gamma}(2,1)$ distribution. This is a special case of [[Convolution]] (Chapter 7).

## See also
[[Random Variable]], [[Cumulative Distribution Function (CDF) | CDF]], [[Convolution]]
