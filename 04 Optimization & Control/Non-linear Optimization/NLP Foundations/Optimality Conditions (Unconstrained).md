---
title: "Optimality Conditions (Unconstrained)"
domain: "Optimization & Control"
course: "Non-linear Optimization"
unit: "NLP Foundations"
level: BSc
status: drafted
confidence: 0
tags: [nonlinear-optimization, calculus, ma2008b]
---
## Definition
For $f:\mathbb R^n\to\mathbb R$, $x^*$ is a **local (relative) minimum** if $f(x^*)\le f(x)$ for all $x$ in some open neighbourhood of $x^*$, and a **global (absolute) minimum** on a set $S$ if $f(x^*)\le f(x)$ for all $x\in S$ (maxima analogously). A **critical point** is a point where $\nabla f=0$ or where $\nabla f$ does not exist; a **stationary point** is one with $\nabla f=0$.

Tools (reviewed in Sesión 2–3): the **gradient** $\nabla f=\left(\frac{\partial f}{\partial x_1},\dots,\frac{\partial f}{\partial x_n}\right)^T$, the **[[Hessian Matrix|Hessian]]** $H=\left[\frac{\partial^2f}{\partial x_i\partial x_j}\right]$, and the multivariable **[[Taylor's Theorem|Taylor formula]]**
$$f(x)=f(x_0)+\nabla f(x_0)^T(x-x_0)+\tfrac12(x-x_0)^TH(\xi)(x-x_0),$$
with $\xi$ on the segment $[x_0,x]$.

## Properties
### Existence — Weierstrass
A continuous function on a **compact** (closed and bounded) set attains a global minimum and maximum (extension of the one-variable [[Extreme Value Theorem]]). On a closed interval $[a,b]$ the procedure is: evaluate $f$ at critical points and at $a,b$; the largest/smallest value is the absolute max/min.

### The gradient is the direction of steepest ascent
The directional derivative along a unit vector $\beta$ is $D_\beta f(p)=\nabla f(p)^T\beta=\|\nabla f(p)\|\cos\theta$, which is maximal when $\theta=0$, i.e. $\beta=\nabla f/\|\nabla f\|$. So $\nabla f(p)$ points where $f$ increases fastest, and it is orthogonal to the level curves of $f$. This motivates [[Steepest Descent]].

### First-order necessary condition
If $f$ is differentiable and $x^*$ is an interior local extremum, then $\nabla f(x^*)=0$.
*Proof.* For each direction $d$, $\varphi(t)=f(x^*+td)$ has a local extremum at $t=0$, so $\varphi'(0)=\nabla f(x^*)^Td=0$ (one-variable result, via the sign of the difference quotient on both sides). Taking $d=\nabla f(x^*)$ gives $\|\nabla f(x^*)\|^2=0$. ∎
The condition is **necessary, not sufficient**: $f(x)=(x-1)^3$ has $f'(1)=0$ but no extremum (an inflection / saddle behaviour). An extremum can also occur where $f'$ does not exist ($|x-1|$ at $1$).

### Second-order conditions
Let $f\in C^2$ and $\nabla f(x^*)=0$. Taylor gives $f(x^*+h)-f(x^*)=\tfrac12h^TH(\xi)h$.
- **Sufficient:** $H(x^*)$ positive definite ⇒ strict local minimum. (By continuity $H(\xi)$ stays PD for small $h$, so the difference is $>0$.) Negative definite ⇒ strict local max.
- **Necessary:** local min ⇒ $H(x^*)$ PSD.
- $H(x^*)$ indefinite ⇒ **saddle point**.
- $H(x^*)$ only semidefinite ⇒ inconclusive (look at higher-order terms).
One-variable version: $f'(c)=0$ and $f''(c)<0$ ⇒ relative max; $f''(c)>0$ ⇒ relative min; $f''(c)=0$ ⇒ no conclusion. First-derivative test: $f'$ changes $+\to-$ at $c$ ⇒ max; $-\to+$ ⇒ min.

### Unique local extremum ⇒ global (one variable)
If $f$ is continuous on an interval $I$ and $c$ is its **only** relative extremum there, then $f(c)$ is the absolute extremum of that type on $I$ (otherwise, by the intermediate/extreme value theorems, another relative extremum would have to exist).

### Supporting theorems (slides)
[[Rolle's Theorem]] (continuous on $[a,b]$, differentiable on $(a,b)$, $f(a)=f(b)=0$ ⇒ $\exists c:f'(c)=0$); [[Mean Value Theorem]] ($f'(c)=\frac{f(b)-f(a)}{b-a}$, Taylor with $n=0$); monotonicity from the sign of $f'$; differentiability ⇒ continuity (not conversely, e.g. $|x|$); continuous partials ⇒ differentiability.

## Examples
**Slides.** $f(x,y)=-20+3x^2+y^2$: $\nabla f=(6x,2y)=0\Rightarrow(0,0)$; $H=\operatorname{diag}(6,2)$ PD ⇒ global minimum $f=-20$ (the function is convex, so local = global).

**Saddle.** $f=x^2-y^2$: $\nabla f=0$ at the origin, $H=\operatorname{diag}(2,-2)$ indefinite ⇒ saddle.

## See also
[[Definiteness of Quadratic Forms]], [[Convex Function]], [[Lagrange Multipliers]], [[Karush–Kuhn–Tucker conditions]], [[Steepest Descent]], [[Newton's Method (Optimization)]]
