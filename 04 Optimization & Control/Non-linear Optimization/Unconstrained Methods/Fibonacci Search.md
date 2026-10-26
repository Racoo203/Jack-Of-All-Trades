---
title: "Fibonacci Search"
domain: "Optimization & Control"
course: "Non-linear Optimization"
unit: "Unconstrained Methods"
level: BSc
status: drafted
confidence: 0
tags: [nonlinear-optimization, numerical-methods, ma2008b]
---
## Definition
**Fibonacci search** finds (approximately) the minimum of a **[[Unimodal Function|unimodal]]** function $f$ on a closed interval $[c_1,c_2]$ using a fixed number $N$ of function evaluations, chosen so that the final **interval of uncertainty** is as small as possible. No derivatives are used; each new evaluation point is chosen from the values already observed.

With observations $c_1\le x_1<\dots<x_N\le c_2$ and $x_k$ the best of them, unimodality implies the minimizer lies in $[x_{k-1},x_{k+1}]$ — the region of uncertainty.

Fibonacci numbers (course convention): $F_0=F_1=1$, $F_k=F_{k-1}+F_{k-2}$ (so $1,1,2,3,5,8,13,\dots$).

## Properties
### Interval reduction
Let $d_1=c_2-c_1$ and $d_k$ the width after $k$ observations. The optimal strategy gives
$$d_k=\frac{F_{N-k+1}}{F_N}\,d_1,\qquad\text{in particular}\qquad d_N=\frac{d_1}{F_N}.$$

### Procedure
1. Choose $N$ and compute $F_0,\dots,F_N$.
2. Place the first two observations symmetrically, at distance $d_2=\dfrac{F_{N-1}}{F_N}d_1$ from each end:
$$x_1=c_2-\frac{F_{N-1}}{F_N}d_1,\qquad x_2=c_1+\frac{F_{N-1}}{F_N}d_1.$$
3. Compare $f(x_1)$ and $f(x_2)$ and discard the part beyond the worse point; the new interval has width $d_2$ and already contains one observation.
4. Place the next observation **symmetrically** to the one inside, so the width becomes $d_3=\frac{F_{N-2}}{F_N}d_1$, and so on. Each step reuses one previous evaluation.

### Why the widths follow Fibonacci numbers
Symmetric placement means the retained interval contains a point that becomes an interior point of the next step. So $d_k=d_{k+1}+d_{k+2}$ (the current interval is the union of the next interval and the discarded piece, which has the width of the one after). Running this recursion backward from the last step, where the two final points nearly coincide ($d_{N-1}=2d_N$), gives $d_{N-j}=F_{j+1}d_N$, hence $d_1=F_Nd_N$. ∎ (Strictly, the last two points are separated by a small $\epsilon$ to be distinguishable.)

### Relation to golden section
As $N\to\infty$, $F_{N-1}/F_N\to\frac{\sqrt5-1}{2}=0.618\ldots$, so Fibonacci search tends to [[Golden Section Search]]. Fibonacci is optimal for a known $N$; golden section does not require $N$ in advance and loses very little.

## Examples
$N=5$ on $[0,8]$: $F=1,1,2,3,5,8$ so $F_5=8$. First points at distance $\frac{F_4}{F_5}\cdot8=5$ from each end: $x_1=3$, $x_2=5$. Final uncertainty $d_5=8/8=1$ after 5 evaluations (vs $8\cdot0.618^4\approx1.17$ for golden section with 5 evaluations).

## See also
[[Golden Section Search]], [[Line Search]], [[Quadratic Interpolation Search]], [[Unimodal Function]]
