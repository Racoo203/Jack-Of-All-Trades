---
title: "Newton's Method (Optimization)"
domain: "Optimization & Control"
course: "Non-linear Optimization"
unit: "Unconstrained Methods"
level: BSc
status: drafted
confidence: 0
tags: [nonlinear-optimization, numerical-methods, ma2008b]
---
## Definition
**Newton's (Newton–Raphson) method** minimizes $f$ by repeatedly minimizing its second-order [[Taylor's Theorem|Taylor]] model. At $x_k$,
$$f(x)\approx q_k(x)=f(x_k)+\nabla f(x_k)^T(x-x_k)+\tfrac12(x-x_k)^TH(x_k)(x-x_k),$$
and setting $\nabla q_k=0$ gives the **Newton step** $p_k$ from
$$H(x_k)\,p_k=-\nabla f(x_k),\qquad x_{k+1}=x_k+p_k=x_k-H(x_k)^{-1}\nabla f(x_k).$$
In one variable: $x_{k+1}=x_k-\dfrac{f'(x_k)}{f''(x_k)}$ (Newton's root-finding method applied to $f'$). For a line search inside a multivariable method, the needed scalar derivatives are directional: $f'=\nabla f^Td$, $f''=d^THd$.

**Basic algorithm (slides).** Start at $x_0$; if $\|\nabla f(x_k)\|<\varepsilon$ stop; solve $\nabla^2f(x_k)p=-\nabla f(x_k)$; set $x_{k+1}=x_k+p_k$; repeat.

## Properties
### Exact for quadratics
If $f=c+b^Tx+\frac12x^TQx$ with $Q$ PD, then $q_k\equiv f$ and one Newton step from any point lands on $x^*=-Q^{-1}b$.
*Slides' example:* $f=-20+3x^2+y^2$, $\nabla f=(6x,2y)$, $H=\operatorname{diag}(6,2)$, $H^{-1}=\operatorname{diag}(\frac16,\frac12)$: from any $(x,y)$, $(x,y)-H^{-1}\nabla f=(x-x,\;y-y)=(0,0)$. Compare with the zig-zag of [[Steepest Descent]].

### Local quadratic convergence
If $f\in C^3$ (or $\nabla^2f$ Lipschitz), $\nabla f(x^*)=0$ and $H(x^*)$ is PD, then for $x_0$ close enough to $x^*$, $\|x_{k+1}-x^*\|\le C\|x_k-x^*\|^2$.
*Sketch.* $0=\nabla f(x^*)=\nabla f(x_k)+H(x_k)(x^*-x_k)+O(\|x_k-x^*\|^2)$. Multiply by $H(x_k)^{-1}$ (bounded near $x^*$) and use $x_{k+1}=x_k-H^{-1}\nabla f(x_k)$ to get $x_{k+1}-x^*=O(\|x_k-x^*\|^2)$.

### Difficulties (slides)
- **No convergence:** iterates run off to infinity, or $H(x_k)$ is singular so the system has no solution.
- **Convergence to maxima or saddle points:** the pure method only looks for $\nabla f=0$.
- $p_k$ is a descent direction only if $\nabla f^Tp_k=-\nabla f^TH^{-1}\nabla f<0$, which is guaranteed when $H(x_k)$ is PD — true near a strict minimum, not far from it.

### Modified Newton method
Solve $M_kp_k=-\nabla f(x_k)$ with $M_k$ **positive definite** and as close as possible to $\nabla^2f(x_k)$:
- **Add a multiple of the identity:** $M_k=\nabla^2f(x_k)+\gamma I$, $\gamma=-\min\big(0,\lambda_{\min}(\nabla^2f(x_k))-\delta\big)$ for a small $\delta>0$. All eigenvalues shift by $\gamma$.
- **Modify the eigenvalues:** $\nabla^2f=U\Lambda U^T$, $M_k=U\bar\Lambda U^T$ with $\bar\lambda_i=\max(\delta,\lambda_i)$ (or $|\lambda_i|$), keeping the eigenvectors.
- **Modified Cholesky** factorization, etc.
Because $M_k$ is PD, $p_k$ is a descent direction. To also rule out divergence and cycling, add a **[[Line Search|backtracking line search]]**: $x_{k+1}=x_k+\alpha_kp_k$ with $\alpha_k\in(0,1]$ satisfying $f(x_k+\alpha_kp_k)\le f(x_k)+\sigma\alpha_k\nabla f(x_k)^Tp_k$, $\sigma\in[10^{-4},0.1]$ — try $\alpha=1$, then halve. For **maximization**, require $M_k$ negative definite (use $H_k-\gamma I$).

### Global convergence (slides' proof outline)
Assume the level set $S_0=\{y:f(y)\le f(x_0)\}$ is compact; all iterates stay in $S_0$, so convergent subsequences exist. From the sufficient-decrease condition, summing over $k$ and using boundedness of $f$ below, $\alpha_k\nabla f(x_k)^Tp_k\to0$. From $M_kp_k=-\nabla f(x_k)$ with eigenvalues of $M_k$ bounded in $[\delta,\Delta]$,
$$\nabla f(x_k)^Tp_k=-\nabla f(x_k)^TM_k^{-1}\nabla f(x_k)\le-\tfrac1\Delta\|\nabla f(x_k)\|^2,$$
so $\alpha_k\|\nabla f(x_k)\|^2\to0$. A Taylor expansion of $\varphi(\alpha)=f(x_k+\alpha p_k)$ shows the accepted $\alpha_k$ cannot shrink to zero (it is bounded below by a multiple of $-(1-\sigma)\varphi'(0)/\varphi''$), hence $\|\nabla f(x_k)\|\to0$: every limit point is stationary. (Stationary, not necessarily a minimum.)

### Levenberg–Marquardt
$$x_{i+1}=x_i-\alpha\,(\lambda I+H_f)^{-1}\nabla f,$$
with $\lambda$ chosen so that $\lambda I+H_f$ is PD. As $\lambda\to\infty$ the step tends to a short steepest-descent step; as $\lambda\to0$, to Newton's step — an interpolation between robustness and speed.

### Practical descent strategy (slides)
Start with Newton; if there is no descent (Hessian not PD) after several attempts (e.g. 10), switch to steepest descent.

### Cholesky factorization as a PD test and solver
A symmetric matrix is PD iff it factors as $A=LL^T$ with $L$ lower triangular and positive diagonal. Row by row ($k=1..n$):
$$L_{ki}=\frac{A_{ki}-\sum_{j<i}L_{ij}L_{kj}}{L_{ii}}\;(i<k),\qquad L_{kk}=\sqrt{A_{kk}-\sum_{j<k}L_{kj}^2}.$$
If a radicand is $\le0$, $A$ is not PD — then modify it. Solving $Hp=-g$ reduces to two triangular solves.

### Quasi-Newton by finite differences (1-D)
When derivatives are not available:
$$f'(x)\approx\frac{f(x+\Delta x)-f(x-\Delta x)}{2\Delta x},\qquad f''(x)\approx\frac{f(x+\Delta x)-2f(x)+f(x-\Delta x)}{\Delta x^2}.$$
Multivariable quasi-Newton methods (DFP, BFGS) build $H^{-1}$ approximations from gradient differences instead — see [[Davidon-Fletcher-Powell Method]].

### Equality constraints
Newton applied to the Lagrange conditions gives the KKT system — see [[Penalty and Merit Functions]].

## Examples
**Slides' example.** $\min f(x)=\dfrac{x_1}{(1+x_1^2)(1+x_2^2)}$, $x_0=(-0.4,0.3)$, solution $x^*=(-1,0)$ ($f^*=-\frac12$).
Iteration 1: $\nabla f(x_0)=(0.573,0.174)^T$ (matches the slide). Near the solution, at $(-1.007,-0.454)$: $\nabla f=(-0.003,-0.312)$, $H_{11}=0.406$ ✓. The slide's later Hessian entries ($H_{22}=0.452$ and $0.802$) do not match a direct evaluation ($0.218$ at $(-1.007,-0.454)$; $0.708$ at $(-0.996,0.236)$), and a pure Newton step from $x_0$ with the exact Hessian goes to $(-1.061,-0.684)$, not the slide's $(-1.007,-0.454)$. <!-- UNVERIFIED: the slide's numeric iterates are not reproducible with the exact Hessian; use them for the method's flow, not the numbers. -->

**Modified Newton, indefinite Hessian (slides).** Same $f$ at $x_0=(0.5,-0.3)$: $\nabla^2f(x_0)\approx\begin{pmatrix}-1.29&0.24\\0.24&-0.45\end{pmatrix}$ is negative definite (eigenvalues $\approx-1.36,-0.39$), so the pure Newton step would head for a maximum. Shifting by $\gamma\approx1.37$ gives a PD $M_0$ and a descent direction; the backtracking search then accepts $\alpha=1$.

## See also
[[Steepest Descent]], [[Line Search]], [[Definiteness of Quadratic Forms]], [[Powell's Method]], [[Penalty and Merit Functions]], [[Davidon-Fletcher-Powell Method]]
