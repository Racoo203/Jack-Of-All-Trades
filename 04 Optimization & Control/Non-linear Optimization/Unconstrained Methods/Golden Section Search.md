---
title: "Golden Section Search"
domain: "Optimization & Control"
course: "Non-linear Optimization"
unit: "Unconstrained Methods"
level: BSc
status: drafted
confidence: 0
tags: [nonlinear-optimization, numerical-methods, ma2008b]
---
## Definition
**Golden section search** locates the extremum of a [[Unimodal Function|unimodal]] function on $[x_l,x_u]$ by shrinking the interval by a constant factor $R=\frac{\sqrt5-1}{2}\approx0.618$ per iteration, reusing one interior evaluation each time.

With $d=R\,(x_u-x_l)$, the two interior points are
$$x_1=x_l+d,\qquad x_2=x_u-d\qquad(x_2<x_1).$$
For **minimization**:
- if $f(x_1)<f(x_2)$: the minimum is in $[x_2,x_u]$ → $x_l\leftarrow x_2$, $x_2\leftarrow x_1$, compute a new $x_1$;
- if $f(x_2)<f(x_1)$: the minimum is in $[x_l,x_1]$ → $x_u\leftarrow x_1$, $x_1\leftarrow x_2$, compute a new $x_2$.
(For maximization reverse the comparisons.)

## Properties
### Deriving the golden ratio
Two conditions (slides): the two sub-lengths add up to the whole, $\ell_0=\ell_1+\ell_2$, and successive ratios are equal, $\dfrac{\ell_1}{\ell_0}=\dfrac{\ell_2}{\ell_1}$ (so the retained interior point sits in the same relative position in the next interval, and can be reused). Let $R=\ell_2/\ell_1$. Dividing the first condition by $\ell_1$: $\frac{\ell_0}{\ell_1}=1+R$, and the second gives $\frac{\ell_0}{\ell_1}=\frac1R$. Hence
$$\frac1R=1+R\;\Longrightarrow\;R^2+R-1=0\;\Longrightarrow\;R=\frac{-1+\sqrt{1+4}}{2}=\frac{\sqrt5-1}{2}=0.61803\ldots$$

### Why an evaluation is reused
Take the first case: the new interval is $[x_2,x_u]$ with length $\ell'=x_u-x_2=R\ell_0$. Its left interior point must be $x_2'=x_u-R\ell'=x_u-R^2\ell_0$. Using $R^2=1-R$,
$$x_2'=x_u-(1-R)\ell_0=x_l+\ell_0-(1-R)\ell_0=x_l+R\ell_0=x_1.$$
So the old $x_1$ is exactly the new $x_2$ (the update "$x_2\leftarrow x_1$"), and its function value is already known: only **one new evaluation per iteration** is needed. The second case is symmetric.

### Convergence
After $k$ iterations the interval length is $R^k\ell_0$ — linear convergence with rate $0.618$. To reach tolerance $\varepsilon$: $k\ge\dfrac{\ln(\varepsilon/\ell_0)}{\ln R}$. For $\ell_0=10$ and $\varepsilon=10^{-4}$, $k\ge24$.

## Examples
**Course script (`busquedadorada_completo.py`).** Minimizes a user-given $f$ on $[-5,5]$ for 25 iterations with $r=0.618$:
```python
x3 = x2 - r*(x2 - x1)   # left interior point
x4 = x1 + r*(x2 - x1)   # right interior point
if f(x3) < f(x4): keep [x1, x4]   # minimum is left of x4
else:             keep [x3, x2]
```
Run on $f(x)=(x-2)^2$ (`output.txt`): first iteration $x_3=-1.18$, $x_4=1.18$, $f(x_3)=10.11>f(x_4)=0.672$ → keep $[-1.18,5]$; …; after 25 iterations the interval is $[1.999977,\,2.000036]$ and the estimate $x^*\approx2.000007$, $f\approx0$. Width check: $10\times0.618^{25}\approx6\times10^{-5}$ ✓.
*Improvement:* the script recomputes both interior points each iteration (2 evaluations) instead of reusing one, which is exactly the saving the golden ratio was designed for; with $r=0.618$ rounded, the reused point would also drift slightly.

## See also
[[Fibonacci Search]], [[Line Search]], [[Quadratic Interpolation Search]], [[Unimodal Function]]
