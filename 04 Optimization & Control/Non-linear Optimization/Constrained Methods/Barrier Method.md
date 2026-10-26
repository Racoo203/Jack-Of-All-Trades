---
title: "Barrier Method"
domain: "Optimization & Control"
course: "Non-linear Optimization"
unit: "Constrained Methods"
level: BSc
status: drafted
confidence: 0
tags: [nonlinear-optimization, numerical-methods, ma2008b]
---
## Definition
For inequality-constrained problems
$$\min_xf(x)\quad\text{s.t.}\quad c(x)\ge0,$$
the KKT conditions ([[Karush–Kuhn–Tucker conditions]]) contain inequalities ($\lambda\ge0$, $c\ge0$) and complementarity ($\lambda^Tc=0$), so they cannot be solved as a plain system of equations. **Barrier (interior-point) methods** replace the problem by a sequence of equality-constrained problems whose objective includes a **barrier term** that blows up at the boundary: it keeps iterates strictly feasible and barely changes $f$ in the interior.

**Log-barrier reformulation (slides).**
1. Add slacks: $\min_{x,s}f(x)$ s.t. $c(x)-s=0$, $s\ge0$.
2. Move the bounds into the objective:
$$\min_{x,s}\;f(x)-\mu\sum_i\log s_i\quad\text{s.t.}\quad c(x)-s=0,\qquad\mu>0.$$

## Properties
### Convergence as $\mu\to0$
If $x^*(\mu)$ solves the barrier problem, then (under standard assumptions) $\lim_{\mu\to0}x^*(\mu)=x^*$, the solution of the original problem. The trajectory $x^*(\mu)$ is the **central path**.

*Toy derivation (slides' picture).* $\min x^2$ s.t. $x\ge1$ ($x^*=1$). Barrier: $B(x)=x^2-\mu\log(x-1)$, defined for $x>1$.
$$B'(x)=2x-\frac{\mu}{x-1}=0\iff2x^2-2x-\mu=0\iff x^*(\mu)=\frac{1+\sqrt{1+2\mu}}{2}>1,$$
and $x^*(\mu)\to1$ as $\mu\to0^+$. Also $\frac{\mu}{x^*(\mu)-1}=2x^*(\mu)\to2=\lambda^*$: the barrier term's gradient estimates the KKT multiplier.

### Why the multiplier emerges
Stationarity of the barrier Lagrangian in $s$ gives $\lambda_i=\mu/s_i$, i.e. $\lambda_is_i=\mu$: a **perturbed complementarity** condition that becomes $\lambda_is_i=0$ as $\mu\to0$.

### Algorithm
1. Choose $\mu_1$ (e.g. $1$) and a strictly feasible start ($s_0>0$).
2. Starting from $x^*(\mu_{s-1})$, solve the barrier problem approximately (Newton on its KKT system, as in [[Penalty and Merit Functions]]).
3. Reduce $\mu_{s+1}=0.1\,\mu_s$ and return to 2, until $\mu$ is of the order of the desired accuracy (e.g. $10^{-5}$).

### Keeping iterates positive — fraction to the boundary
The objective is only defined for $s>0$ (and $x>0$ when the variables themselves are barrier-bounded), so the step must satisfy $x_k+\alpha p_k>0$:
$$\alpha<\bar\alpha=\min\left\{\frac{x_i}{-p_i}:p_i<0\right\},\qquad\alpha_k=\min\{1,\;0.99\,\bar\alpha\}\ \text{(or }0.995\bar\alpha).$$
Then check sufficient decrease of a merit function.

### Linear programming
$\min c^Tx$ s.t. $Ax=b$, $x\ge0$ becomes $\min c^Tx-\mu\sum\log x_i$ s.t. $Ax=b$; apply Newton, update $\mu$ — the primal barrier interior-point method for [[Linear Programming]] (Karmarkar-type), an alternative to simplex.

## Examples
**Portfolio (slides).** $\min_x x^TRx$ (variance) s.t. $m^Tx\ge3.5$ (expected return), $e^Tx=1$, $x\ge0$, with two assets. Standard form with slack: $m^Tx-s=3.5$, $e^Tx=1$, $x,s\ge0$; barrier problem
$$\min_{x,s}\;x^TRx-\mu\Big(\sum_i\log x_i+\log s\Big)\quad\text{s.t.}\quad m^Tx-s=3.5,\;e^Tx=1.$$
From $x_0=(0.5,0.5)$, $s_0=0.5$, $\mu_0=0.1$, $\lambda_0=0$, the Newton/KKT direction is $p_0=(0.675,-0.675,-2.877)$. A full step would make $x_2$ and $s$ negative (objective undefined), so
$$\bar\alpha=\min\left\{\frac{0.5}{0.675},\frac{0.5}{2.877}\right\}=0.174,\qquad\alpha_0=\min\{1,0.995\bar\alpha\}\approx0.173,$$
which passes the merit test ($m(x_0+\alpha p_0)=73.32<102.55$), giving $x_1\approx(0.617,0.383)$, $s_1\approx0.002$. <!-- The R and m data are partly garbled in the extracted slide text (R ≈ ((26, 55.6), (55.6, 248)), m ≈ (1.46, 4.6)); check the slide before reusing the numbers. -->

## See also
[[Penalty and Merit Functions]], [[Karush–Kuhn–Tucker conditions]], [[Newton's Method (Optimization)]], [[Linear Programming]], [[Markowitz model]]
