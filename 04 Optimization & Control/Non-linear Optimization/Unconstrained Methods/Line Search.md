---
title: "Line Search"
domain: "Optimization & Control"
course: "Non-linear Optimization"
unit: "Unconstrained Methods"
level: BSc
status: drafted
confidence: 0
tags: [nonlinear-optimization, numerical-methods, ma2008b]
---
## Definition
**Basic descent methods** for $\min_{x\in\mathbb R^n}f(x)$ share one structure:
1. start at $x_0$;
2. choose a **descent direction** $d_k$ by a fixed rule (this is what distinguishes [[Steepest Descent]], [[Newton's Method (Optimization)|Newton]], [[Powell's Method|Powell]], …), i.e. $\nabla f(x_k)^Td_k<0$;
3. find a step length $\alpha_k$ along $d_k$ — the **line search**;
4. update $x_{k+1}=x_k+\alpha_kd_k$.

The line search solves the one-dimensional subproblem
$$\min_{\alpha\ge0}\;\varphi(\alpha)=f(x_k+\alpha d_k).$$
It is much simpler than the original problem (one variable), but it is responsible for a large share of the function evaluations, so its choice matters.

## Properties
### Why a descent direction guarantees progress
$\varphi'(0)=\nabla f(x_k)^Td_k<0$, so by Taylor $\varphi(\alpha)=\varphi(0)+\alpha\varphi'(0)+o(\alpha)<\varphi(0)$ for small $\alpha>0$.

### Exact line search
Choose $\alpha_k=\arg\min_\alpha\varphi(\alpha)$, i.e. $\varphi'(\alpha_k)=\nabla f(x_{k+1})^Td_k=0$: **the new gradient is orthogonal to the previous direction**. For a quadratic $f=\frac12x^TQx-b^Tx$ with $g_k=\nabla f(x_k)$ this has the closed form
$$\alpha_k=-\frac{g_k^Td_k}{d_k^TQd_k}$$
(from $\varphi'(\alpha)=(Q(x_k+\alpha d_k)-b)^Td_k=g_k^Td_k+\alpha d_k^TQd_k=0$). In hand calculations (Powell labs) one writes $\varphi(\lambda)$ explicitly and solves $\varphi'(\lambda)=0$.

### Families of line-search methods (slides)
- **Direct / derivative-based:** gradient, Newton, quasi-Newton, secant.
- **Polynomial interpolation:** quadratic, cubic, DSC (Davies–Swann–Campey) — see [[Quadratic Interpolation Search]].
- **Interval (bracketing):** bisection, [[Fibonacci Search]], [[Golden Section Search]] — require a unimodal $\varphi$ on a known interval.
- **Inexact:** Armijo, Goldstein.

### Inexact line search
Exact minimization along $d_k$ is wasteful: the minimum along a line is not the minimum of $f$. Precision is sacrificed for total computing time by stopping early, according to a criterion:
- **Percentage test:** accept $\alpha$ with $|\alpha-\alpha^*|\le c\,\alpha^*$ ($0<c<1$, typically $c=0.1$).
- **Armijo rule:** with $0<\varepsilon<1$ and $\eta>1$, $\alpha$ is *not too large* if
$$\varphi(\alpha)\le\varphi(0)+\varepsilon\,\alpha\,\varphi'(0)$$
(the value lies below the dashed line of slope $\varepsilon\varphi'(0)$), and *not too small* if $\varphi(\eta\alpha)>\varphi(0)+\varepsilon\,\eta\alpha\,\varphi'(0)$. Typical values: $\eta=2$, $\varepsilon=0.2$ (slides) or $\varepsilon\in[10^{-4},0.1]$ (Newton slides).
  *Simplified Armijo procedure:* start from an arbitrary $\alpha$; if it satisfies the inequality, multiply by $\eta$ until it fails and keep the last one that passed; if it fails, divide by $\eta$ until it passes.
- **Backtracking** (used with Newton): try $\alpha=1$; if the sufficient-decrease condition fails, halve $\alpha$ and repeat.

### The sufficient-decrease line is always reachable
Since $\varphi(\alpha)=\varphi(0)+\alpha\varphi'(0)+o(\alpha)$ and $\varepsilon\varphi'(0)>\varphi'(0)$ (because $\varphi'(0)<0$, $\varepsilon<1$), we get $\varphi(\alpha)<\varphi(0)+\varepsilon\alpha\varphi'(0)$ for all small enough $\alpha$. So backtracking terminates.

## Examples
**Backtracking (slides).** $f(x)=\dfrac{x_1}{(1+x_1^2)(1+x_2^2)}$, $x_0=(-0.5,-0.3)^T$, $p_0=(-2,1)^T$, $\varepsilon=0.1$.
$f(x_0)=-0.367$, $\nabla f(x_0)=(0.440,-0.202)^T$, $\nabla f(x_0)^Tp_0=-1.083<0$ (descent).
- $\alpha=1$: $f(x_0+p_0)=f(-2.5,0.7)=-0.231>-0.367+0.1(-1.083)=-0.475$ → reject.
- $\alpha=0.5$: $f(-1.5,0.2)=-0.444\le-0.367+0.05(-1.083)=-0.421$ → accept.
So $x_1=x_0+0.5p_0=(-1.5,0.2)^T$.

## See also
[[Steepest Descent]], [[Newton's Method (Optimization)]], [[Golden Section Search]], [[Fibonacci Search]], [[Quadratic Interpolation Search]], [[Powell's Method]]
