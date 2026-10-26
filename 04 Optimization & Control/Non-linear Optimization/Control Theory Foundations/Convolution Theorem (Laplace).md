---
title: "Convolution Theorem (Laplace)"
domain: "Optimization & Control"
course: "Non-linear Optimization"
unit: "Control Theory Foundations"
level: BSc
status: drafted
confidence: 0
tags: [control-theory, differential-equations, ma2008b]
---
## Definition
For piecewise continuous $f,g$ on $[0,\infty)$, the **convolution** is
$$(f*g)(t)=\int_0^t f(\tau)\,g(t-\tau)\,d\tau.$$
It is commutative: substituting $u=t-\tau$ gives $\int_0^t f(t-u)g(u)\,du=(g*f)(t)$.

## Properties
### Convolution theorem
$$\mathcal L\{f*g\}=F(s)\,G(s).$$
*Proof.* Using the [[Laplace Transform]] definition,
$$F(s)G(s)=\int_0^\infty f(\tau)e^{-s\tau}d\tau\int_0^\infty g(u)e^{-su}du=\int_0^\infty\!\!\int_0^\infty f(\tau)g(u)e^{-s(\tau+u)}\,du\,d\tau.$$
Substitute $t=\tau+u$ (for fixed $\tau$, $u=t-\tau$, $du=dt$, $t$ from $\tau$ to $\infty$):
$$=\int_0^\infty\!\!\int_\tau^\infty f(\tau)g(t-\tau)e^{-st}\,dt\,d\tau.$$
The region is $0\le\tau\le t<\infty$; swapping the order ([[Fubini's Theorem]], justified by exponential order):
$$=\int_0^\infty e^{-st}\left(\int_0^t f(\tau)g(t-\tau)\,d\tau\right)dt=\mathcal L\{f*g\}.\qquad\blacksquare$$

### Main use: inverting products
$\mathcal L^{-1}\{F(s)G(s)\}=(f*g)(t)$. In control, the output of an LTI system is the convolution of the impulse response with the input: $y(t)=(g*u)(t)$ since $Y=G\,U$ (see [[Transfer Function]]).

### Special case $g\equiv1$
$G(s)=1/s$, so $\mathcal L^{-1}\{F(s)/s\}=\int_0^t f(\tau)d\tau$ — the integral rule.

## Examples
**Final value by convolution (Actividad 1).** $F(s)=\frac{10}{s(s+1)}=\frac{10}{s}\cdot\frac{1}{s+1}$, so
$$f(t)=\int_0^t 10\,e^{-(t-\tau)}\cdot1\,d\tau\;\text{(or }10*e^{-t})=10\,(1-e^{-t})\to10,$$
matching the [[Initial and Final Value Theorems|final value theorem]] $\lim_{s\to0}sF(s)=10$.

**Repeated factor (Actividad 1).** $F(s)=\frac{3}{(s^2+9)^2}=\frac13\cdot\frac{3}{s^2+9}\cdot\frac{3}{s^2+9}$, so $f=\frac13(\sin3t*\sin3t)$:
$$\int_0^t\sin3\tau\,\sin(3t-3\tau)\,d\tau=\frac12\int_0^t[\cos(6\tau-3t)-\cos3t]\,d\tau=\frac12\left[\frac{\sin 3t}{3}-t\cos3t\right],$$
using $\int_0^t\cos(6\tau-3t)d\tau=\frac{\sin3t-\sin(-3t)}{6}=\frac{\sin3t}{3}$. Hence
$$f(t)=\frac{1}{18}\sin3t-\frac{t}{6}\cos3t.$$

## See also
[[Laplace Transform]], [[Transfer Function]], [[Initial and Final Value Theorems]]
