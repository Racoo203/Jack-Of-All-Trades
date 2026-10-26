---
title: "Convex Function"
domain: "Optimization & Control"
course: "Non-linear Optimization"
unit: "NLP Foundations"
level: BSc
status: drafted
confidence: 0
tags: [nonlinear-optimization, convexity, ma2008b]
---
## Definition
Let $X\subseteq\mathbb R^n$ be a [[Convex Set]]. A function $f:X\to\mathbb R$ is **convex** if for all $x_1,x_2\in X$ and $\lambda\in[0,1]$
$$f\big(\lambda x_1+(1-\lambda)x_2\big)\le\lambda f(x_1)+(1-\lambda)f(x_2),$$
i.e. the chord between two points of the graph lies on or above the graph. It is **strictly convex** if the inequality is strict for $x_1\ne x_2$, $\lambda\in(0,1)$. $f$ is **concave** if $-f$ is convex.

## Properties
### Algebra of convex functions (slides)
- Any linear function $c^Tx$ is both convex and concave (equality holds).
- $f$ convex ⇔ $-f$ concave.
- A nonnegative combination of convex functions is convex (add the defining inequalities).
- If $h$ is convex and $g$ is convex **and nondecreasing**, then $g\circ h$ is convex: $g(h(\lambda x_1+(1-\lambda)x_2))\le g(\lambda h(x_1)+(1-\lambda)h(x_2))\le\lambda g(h(x_1))+(1-\lambda)g(h(x_2))$. Example (Tema 7): $e^{x^2+y^2}$ is convex because $x^2+y^2$ is convex and $e^u$ is convex nondecreasing.
- A quadratic form $x^TDx$ ($D$ symmetric) is convex on $\mathbb R^n$ iff $D$ is PSD, strictly convex if PD (see [[Definiteness of Quadratic Forms]]); concave iff NSD.

### First-order characterization
For $f\in C^1$ on an open convex region: $f$ is convex iff
$$f(x)\ge f(x^*)+\nabla f(x^*)^T(x-x^*)\quad\forall x,x^*,$$
i.e. the graph lies above every tangent plane (concave: below).
*Proof (⇒).* From convexity, $f(x^*+\lambda(x-x^*))\le f(x^*)+\lambda[f(x)-f(x^*)]$, so $\dfrac{f(x^*+\lambda(x-x^*))-f(x^*)}{\lambda}\le f(x)-f(x^*)$. Let $\lambda\to0^+$: the left side tends to the directional derivative $\nabla f(x^*)^T(x-x^*)$. ∎
*(⇐).* Let $z=\lambda x_1+(1-\lambda)x_2$. Apply the inequality at $z$ to $x_1$ and $x_2$, multiply by $\lambda$ and $1-\lambda$ and add: $\lambda f(x_1)+(1-\lambda)f(x_2)\ge f(z)+\nabla f(z)^T(\lambda x_1+(1-\lambda)x_2-z)=f(z)$. ∎

### Second-order characterization
For $f\in C^2$ on an open convex region $R$: $f$ is convex on $R$ **iff its [[Hessian Matrix|Hessian]] $H(x)$ is positive semidefinite for every $x\in R$** (PD everywhere ⇒ strictly convex, but not conversely: $x^4$ is strictly convex with $f''(0)=0$).
*Proof sketch.* Restrict to a line: $\varphi(t)=f(x+td)$ has $\varphi''(t)=d^TH(x+td)d$. A one-variable $C^2$ function is convex iff $\varphi''\ge0$ (by the mean value theorem, $\varphi'$ is then nondecreasing, which gives the chord inequality), and $f$ is convex iff all such restrictions are. ∎
Because $H$ is symmetric when the mixed partials are continuous ([[Schwarz's Theorem]]), the definiteness tests apply directly. The Hessian of a convex function may vanish at some points.

### Local minimum ⇒ global minimum
If $f$ is convex on a convex set $X$, every local minimum is global.
*Proof.* Let $x^*$ be a local min and suppose $f(y)<f(x^*)$ for some $y\in X$. For $\lambda\in(0,1]$, $z_\lambda=x^*+\lambda(y-x^*)\in X$ and $f(z_\lambda)\le(1-\lambda)f(x^*)+\lambda f(y)<f(x^*)$. As $\lambda\to0$, $z_\lambda$ enters every neighbourhood of $x^*$ — contradicting local minimality. ∎
Symmetrically, a local maximum of a concave function on a convex set is global. For a convex $f$ on a **compact** convex set, a global maximum is attained on the **boundary** (in fact at an extreme point).

### Stationary points are global minima
With the first-order inequality, $\nabla f(x^*)=0$ ⇒ $f(x)\ge f(x^*)$ for all $x$: for convex $C^1$ functions the first-order condition is also sufficient.

## Examples
**Tema 7.** $f(x,y)=x^2+2xy+3y^2$: $H=\begin{pmatrix}2&2\\2&6\end{pmatrix}$, $f_{xx}=2>0$, $\det H=12-4=8>0$ ⇒ PD ⇒ $f$ strictly convex.

**Quadratic with linear part.** $f(x)=c_0+c^Tx+x^TDx$ is convex iff $D$ is PSD — compare with its exact second-order Taylor expansion $f(x)=f(x_0)+\nabla f(x_0)^T(x-x_0)+(x-x_0)^TD(x-x_0)$.

## See also
[[Convex Set]], [[Definiteness of Quadratic Forms]], [[Optimality Conditions (Unconstrained)]], [[Karush–Kuhn–Tucker conditions]], [[Nonlinear Programming Problem]]
