---
title: "Penalty and Merit Functions"
domain: "Optimization & Control"
course: "Non-linear Optimization"
unit: "Constrained Methods"
level: BSc
status: drafted
confidence: 0
tags: [nonlinear-optimization, numerical-methods, ma2008b]
---
## Definition
For the equality-constrained problem
$$\min_xf(x)\quad\text{s.t.}\quad c(x)=0\qquad(c:\mathbb R^n\to\mathbb R^m),$$
the necessary conditions ([[Lagrange Multipliers]], sign convention of Sesión 2–3) are
$$c(x)=0,\qquad\nabla f(x)-\nabla c(x)^T\lambda=0,$$
a nonlinear system in $(x,\lambda)$. A **merit function** is a scalar measure that combines progress in $f$ with progress in feasibility $\|c\|$, and whose minimizer is the solution of the constrained problem; it is used to choose step lengths. A **penalty function** adds a term that punishes constraint violation to $f$.

## Properties
### Newton's method on the KKT conditions
Linearize both conditions at $(x_k,\lambda_k)$ with step $(p_k,\nu_k)$ (writing $\lambda_{k+1}=\lambda_k+\nu_k$):
$$c(x_k)+\nabla c(x_k)p_k=0,\qquad \nabla f(x_k)+\nabla^2_{xx}L(x_k,\lambda_k)p_k-\nabla c(x_k)^T\lambda_k-\nabla c(x_k)^T\nu_k=0,$$
where $L=f-\lambda^Tc$. In matrix form (the **KKT system**), with $H_k=\nabla^2_{xx}L$, $A_k=\nabla c(x_k)$, $g_k=\nabla f(x_k)$, $c_k=c(x_k)$:
$$\begin{pmatrix}H_k&-A_k^T\\A_k&0\end{pmatrix}\begin{pmatrix}p_k\\\nu_k\end{pmatrix}=-\begin{pmatrix}g_k-A_k^T\lambda_k\\c_k\end{pmatrix}.$$
It is exactly the optimality system of the **quadratic subproblem** $\min_p\,g_k^Tp+\frac12p^TH_kp$ s.t. $A_kp+c_k=0$ — the basis of sequential quadratic programming (SQP).
**Basic algorithm:** start at $(x_0,\lambda_0)$; stop if $\|c(x_k)\|+\|\nabla f(x_k)-A_k^T\lambda_k\|<\varepsilon$; solve the KKT system; update $x_{k+1}=x_k+p_k$, $\lambda_{k+1}=\lambda_k+\nu_k$.

### Null-space decomposition
Split $p_k=Z_kp_Z+A_k^Tp_Y$ with $A_kZ_k=0$. Then $A_kA_k^Tp_Y=-c_k$ (the **normal** component restores feasibility) and
$$Z_k^TH_kZ_k\,p_Z=-Z_k^Tg_k-Z_k^TH_kA_k^Tp_Y$$
(the **tangential** component improves $f$ without disturbing the linearized constraints). For descent, the **reduced Hessian** $Z_k^TH_kZ_k$ should be PD; if not, replace it by a PD modification $M_k$, as in the [[Newton's Method (Optimization)|modified Newton method]].

### Feasibility always improves along the normal step
With $\phi(x)=\|c(x)\|^2$, $\nabla\phi=2A^Tc$ and $\nabla\phi^Tp=2c^TAp=-2\|c\|^2<0$ whenever $Ap=-c$: $p$ is always a descent direction for infeasibility. It is not always possible to improve $f$ and feasibility simultaneously; the priority is **first satisfy the constraints, then improve $f$**.

### Merit functions
- **Exact (nonsmooth) penalty:** $m_E(x)=f(x)+\rho\|c(x)\|$. *Theorem:* there is $\bar\rho$ (namely $\bar\rho=\|\lambda^*\|_*$, the dual norm of the optimal multiplier) such that for every $\rho>\bar\rho$, local minimizers of the problem are local minimizers of $m_E$. Drawback: $m_E$ is **not differentiable** where $c=0$.
- **Augmented Lagrangian (smooth):** $m_A(x,\lambda)=f(x)-\lambda^Tc(x)+\tfrac12\rho\|c(x)\|^2$. The Lagrangian alone has zero gradient at the solution but may fail the second-order condition; the quadratic term fixes that: for $\rho$ large enough, minimizers of $m_A(\cdot,\lambda^*)$ and of the problem coincide.
- **Quadratic penalty (not exact):** $f+\frac\rho2\|c\|^2$ recovers the solution only as $\rho\to\infty$, which makes the subproblems ill-conditioned.

*Toy check.* $\min x^2$ s.t. $x-1=0$ ($x^*=1$, $\lambda^*=2$). Quadratic penalty: $\frac{d}{dx}\big[x^2+\frac\rho2(x-1)^2\big]=0\Rightarrow x_\rho=\frac{\rho}{2+\rho}<1$ for every finite $\rho$. Exact penalty $x^2+\rho|x-1|$: for $x<1$ its derivative is $2x-\rho<0$ when $\rho>2$, and for $x>1$ it is $2x+\rho>0$, so the minimum is exactly $x=1$ once $\rho>2=|\lambda^*|$.

### Using the merit function in the line search
Choose $\alpha_k$ so that the merit function decreases sufficiently, e.g.
$$m_E(x_k+\alpha_kp_k)\le m_E(x_k)+\sigma\alpha_k\,\nabla m_E(x_k)^Tp_k,$$
then set $x_{k+1}=x_k+\alpha_kp_k$, $\lambda_{k+1}=\lambda_k+\alpha_k\nu_k$.

## Examples
**Slides.** $\min f(x)=\dfrac{x_1}{(1+x_1^2)(1+x_2^2)}$ s.t. $x_1^2+x_2^2=0.8$, from $x_0=(-0.6,-0.3)$, $\lambda_0=0$: $c(x_0)=0.45-0.8=-0.35$; after solving the KKT system, the exact-penalty merit function ($\rho=10$, $\sigma=0.1$) rejects $\alpha=1$ and accepts $\alpha=0.5$, giving $x_1=(-0.836,-0.120)$, $\lambda_1=0.069$ with $c(x_1)=-0.087$; the next full step is accepted, $x_2=(-0.911,-0.038)$ — feasibility and objective improve together toward $(-\sqrt{0.8},0)$.

## See also
[[Barrier Method]], [[Lagrange Multipliers]], [[Karush–Kuhn–Tucker conditions]], [[Newton's Method (Optimization)]], [[Line Search]], [[Quadratic Programming]]
