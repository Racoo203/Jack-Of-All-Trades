---
title: "Quadratic Interpolation Search"
domain: "Optimization & Control"
course: "Non-linear Optimization"
unit: "Unconstrained Methods"
level: BSc
status: drafted
confidence: 0
tags: [nonlinear-optimization, numerical-methods, ma2008b]
---
## Definition
**Curve-fitting line searches** approximate the one-dimensional function $\varphi$ (see [[Line Search]]) by a low-degree polynomial through a few points and take the polynomial's minimizer as the next estimate.

**Quadratic interpolation.** Given $x_0<x_1<x_2$ with values $f_0,f_1,f_2$ (ideally $f_1<f_0$, $f_1<f_2$, so the minimum is bracketed), the parabola through them has its vertex at
$$x_3=\frac{f_0(x_1^2-x_2^2)+f_1(x_2^2-x_0^2)+f_2(x_0^2-x_1^2)}{2\left[f_0(x_1-x_2)+f_1(x_2-x_0)+f_2(x_0-x_1)\right]}.$$

**DSC method (Davies, Swann and Campey)** combines a *bracketing* phase with steps that double, and a single quadratic fit.

## Properties
### Derivation of the vertex formula
Write $q(x)=a+bx+cx^2$ through the three points. The vertex is $x^*=-\frac{b}{2c}$. Using Lagrange interpolation,
$$q(x)=\sum_{i}f_i\prod_{j\ne i}\frac{x-x_j}{x_i-x_j},$$
the coefficients are $c=\sum_i\frac{f_i}{\prod_{j\ne i}(x_i-x_j)}$ and $b=-\sum_i\frac{f_i\sum_{j\ne i}x_j}{\prod_{j\ne i}(x_i-x_j)}$. Multiplying numerator and denominator by $-(x_0-x_1)(x_1-x_2)(x_2-x_0)$ and simplifying gives the formula above.

### Equally spaced points
If $x_0=a-\Delta$, $x_1=a$, $x_2=a+\Delta$:
$$x^*=a+\frac{\Delta\,(f_0-f_2)}{2\,(f_0-2f_1+f_2)}.$$
(Denominator $>0$ when $f_1$ is below the average of its neighbours, i.e. the parabola opens upward.)

### DSC procedure (slides)
1. Evaluate $f(x^{(0)})$. If $f(x^{(0)}+\Delta x)\le f(x^{(0)})$ go to step 2; otherwise set $\Delta x\leftarrow-\Delta x$ (search the other way) or halve it, and repeat.
2. Set $x^{(k+1)}=x^{(k)}+\Delta x$. If $f(x^{(k+1)})\le f(x^{(k)})$, **double** $\Delta x$ and repeat with $k+1$.
3. When $f(x^{(k+1)})>f(x^{(k)})$, the minimum has been overshot. Call the last point $x^{(m)}$ and the previous ones $x^{(m-1)},x^{(m-2)}$. Halve the last step and evaluate once more at $x^{(m+1)}=x^{(m)}-\tfrac12\Delta x_{\text{last}}$ — the midpoint of $[x^{(m-1)},x^{(m)}]$.
4. Now $x^{(m-2)},x^{(m-1)},x^{(m+1)},x^{(m)}$ are **equally spaced** (spacing $\tfrac12\Delta x_{\text{last}}$). Keep the point with the smallest $f$ and its two neighbours and apply the equally-spaced vertex formula.
5. Optionally repeat from the new estimate with a smaller initial step.

### Cubic fit (with derivatives)
Given $x_{k-1},x_k$ with $f$ and $f'$ at both, fit a cubic and take its local minimizer:
$$x_{k+1}=x_k-(x_k-x_{k-1})\,\frac{f'(x_k)+u_2-u_1}{f'(x_k)-f'(x_{k-1})+2u_2},$$
$$u_1=f'(x_{k-1})+f'(x_k)-3\,\frac{f(x_{k-1})-f(x_k)}{x_{k-1}-x_k},\qquad u_2=\sqrt{u_1^2-f'(x_{k-1})f'(x_k)}.$$
Near the minimum, polynomial fits converge superlinearly (order $\approx1.3$ for the quadratic fit, $2$ for the cubic fit), faster than the linear rate of [[Golden Section Search]], but they need a safeguard to keep points bracketed.

## Examples
$f(x)=(x-2)^2+1$ (an exact parabola): any three distinct points give $x_3=2$ in one step. With $x_0=0,x_1=1,x_2=3$: $f=5,2,2$;
numerator $5(1-9)+2(9-0)+2(0-1)=-40+18-2=-24$; denominator $2[5(1-3)+2(3-0)+2(0-1)]=2(-10+6-2)=-12$; $x_3=2$ ✓.

## See also
[[Line Search]], [[Golden Section Search]], [[Fibonacci Search]], [[Newton's Method (Optimization)]]
