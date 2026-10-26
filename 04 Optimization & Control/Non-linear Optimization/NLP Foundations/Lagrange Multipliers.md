---
title: "Lagrange Multipliers"
domain: "Optimization & Control"
course: "Non-linear Optimization"
unit: "NLP Foundations"
level: BSc
status: drafted
confidence: 0
tags: [nonlinear-optimization, ma2008b]
---
## Definition
For the equality-constrained problem
$$\min f(x)\quad\text{s.t.}\quad h_j(x)=0,\;j=1,\dots,m\;(m<n),$$
the **Lagrangian** is
$$L(x,\mu)=f(x)+\sum_{j=1}^m\mu_j\,h_j(x),$$
with **Lagrange multipliers** $\mu_j$ (the sign convention varies; Ogata-style slides in Sesión 2–3 write $f-\lambda^Tc$). The method is used when the constraints cannot simply be solved for some variables and substituted into $f$ (the "differential calculus with substitution" approach in the slides' taxonomy).

## Properties
### First-order necessary condition
If $x^*$ is a local minimum and $x^*$ is **regular** (the gradients $\nabla h_j(x^*)$ are linearly independent), there exist $\mu^*$ such that
$$\nabla_xL(x^*,\mu^*)=\nabla f(x^*)+\sum_j\mu_j^*\nabla h_j(x^*)=0,\qquad h(x^*)=0.$$
That is, $(x^*,\mu^*)$ is a stationary point of $L$ in all $n+m$ variables.

*Geometric derivation (Tema 7).* At a feasible $x$, a direction $d$ keeps feasibility to first order iff $\nabla h(x)^Td=0$, and decreases $f$ iff $\nabla f(x)^Td<0$. If $\nabla f$ had a component orthogonal to $\nabla h$, we could choose $d$ as minus that component and obtain both. So no feasible descent direction exists exactly when $\nabla f(x^*)$ is **parallel** to $\nabla h(x^*)$: $\nabla f(x^*)=-\mu\nabla h(x^*)$, which is $\nabla_xL=0$.

*Implicit-function derivation ($n=2$, $m=1$).* Regularity lets us write $x_2=\psi(x_1)$ near $x^*$ with $\psi'=-h_{x_1}/h_{x_2}$. Then $x_1\mapsto f(x_1,\psi(x_1))$ has a stationary point: $f_{x_1}+f_{x_2}\psi'=0$, i.e. $f_{x_1}/h_{x_1}=f_{x_2}/h_{x_2}=:-\mu$, giving $f_{x_i}+\mu h_{x_i}=0$.

### Stationarity is not sufficient
Stationary points of $L$ may be minima, maxima or neither. The multiplier matters: the **second-order** test uses $\nabla^2_{xx}L(x^*,\mu^*)$ restricted to the tangent space $\{d:\nabla h(x^*)^Td=0\}$ — positive definite there ⇒ strict local min, negative definite ⇒ strict local max.

### Interpretation: shadow price
For $h(x)=b-g(x)$, $\mu^*=\dfrac{\partial f^*}{\partial b}$ up to sign: the rate of change of the optimal value per unit relaxation of the constraint.

### Newton's method on the Lagrange system
Solving $\nabla_xL=0,\;h=0$ numerically leads to the KKT linear system of [[Penalty and Merit Functions]].

## Examples
**Tema 7.** $\min x_1+x_2$ s.t. $h=x_1^2+x_2^2-2=0$.
$L=x_1+x_2+\mu(x_1^2+x_2^2-2)$, so $\nabla_xL=(1+2\mu x_1,\;1+2\mu x_2)=0$ ⇒ $x_1=x_2=-\frac1{2\mu}$. Substituting in $h$: $2x_1^2=2\Rightarrow x_1=\pm1$.
- $(-1,-1)$, $\mu=\frac12$: $\nabla^2_{xx}L=2\mu I=I$ PD ⇒ **minimum**, $f=-2$. Check: $\nabla f=(1,1)$, $\nabla h(-1,-1)=(-2,-2)$, parallel ✓.
- $(1,1)$, $\mu=-\frac12$: $\nabla^2_{xx}L=-I$ ⇒ maximum, $f=2$.
The slide writes $\nabla L=(1-2\lambda x_1,\,1-2\lambda x_2)$, which corresponds to $L=f-\lambda h$; with that convention the multiplier signs flip, but the points are the same.

## See also
[[Karush–Kuhn–Tucker conditions]], [[Optimality Conditions (Unconstrained)]], [[Pontryagin's Maximum Principle]], [[Penalty and Merit Functions]], [[Convex Function]]
