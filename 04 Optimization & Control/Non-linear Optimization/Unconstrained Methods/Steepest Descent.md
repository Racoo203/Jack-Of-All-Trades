---
title: "Steepest Descent"
domain: "Optimization & Control"
course: "Non-linear Optimization"
unit: "Unconstrained Methods"
level: BSc
status: drafted
confidence: 0
tags: [nonlinear-optimization, numerical-methods, ma2008b]
---
## Definition
The **steepest descent** (gradient) method — one of the oldest multidimensional minimization techniques — moves against the gradient, the direction of fastest local decrease (see [[Optimality Conditions (Unconstrained)]]):
$$x_{k+1}=x_k-\alpha_k\nabla f(x_k),\qquad\alpha_k>0,$$
where $\alpha_k$ comes from a [[Line Search]] or is a fixed **step size / learning rate**. Stop when $\|\nabla f(x_k)\|<\varepsilon$ (in the slides, when $\nabla f(x_{k+1})\approx0$).
**Gradient ascent** (for maximization, as in the Laboratorio Multimodal) uses $x_{k+1}=x_k+\lambda\nabla f(x_k)$.

One-variable version: $x_{k+1}=x_k-\alpha f'(x_k)$ with $\alpha\in(0,1]$ chosen by the user ("modified gradient method"); ideally $\alpha$ decreases as the search progresses, which introduces two tuning parameters — the motivation for [[Newton's Method (Optimization)|Newton's method]], which computes the step itself.

## Properties
### Why $-\nabla f$ is the steepest direction
For a unit vector $\beta$, $D_\beta f=\nabla f^T\beta=\|\nabla f\|\cos\theta$, minimized at $\theta=\pi$, i.e. $\beta=-\nabla f/\|\nabla f\|$.

### Exact line search on a quadratic
For $f=\frac12x^TQx-b^Tx$ ($Q$ PD) and $g_k=\nabla f(x_k)$, the exact step along $-g_k$ is
$$\alpha_k=\frac{g_k^Tg_k}{g_k^TQg_k}$$
(set $\frac{d}{d\alpha}f(x_k-\alpha g_k)=-g_k^T(g_k-\alpha Qg_k)=0$). Consecutive gradients are orthogonal ($g_{k+1}^Tg_k=0$), which causes the characteristic **zig-zag** path when the level sets are elongated ellipses. The error satisfies (Kantorovich)
$$f(x_{k+1})-f^*\le\left(\frac{\kappa-1}{\kappa+1}\right)^2\big(f(x_k)-f^*\big),\qquad\kappa=\frac{\lambda_{\max}(Q)}{\lambda_{\min}(Q)},$$
i.e. only **linear** convergence, slow for ill-conditioned problems.

### Fixed step size: stability limit
For the quadratic above, $x_{k+1}-x^*=(I-\alpha Q)(x_k-x^*)$. In eigen-coordinates each component is multiplied by $1-\alpha\lambda_i$, so the iteration converges iff $|1-\alpha\lambda_i|<1$ for all $i$:
$$0<\alpha<\frac{2}{\lambda_{\max}(Q)}.$$
Too large a step makes the iterates oscillate with growing amplitude ("the gradient explodes"); the best fixed step is $\alpha=\frac{2}{\lambda_{\min}+\lambda_{\max}}$.

## Examples
**Slides.** $f(x,y)=-20+3x^2+y^2$, $\nabla f=(6x,2y)$, minimum at $(0,0)$, start $(-1.7,1.7)$. The Hessian is $\operatorname{diag}(6,2)$ ($\kappa=3$), so a fixed step needs $\alpha<\frac26=\frac13$: with $\alpha=0.25$ the $x$-error is multiplied by $1-1.5=-0.5$ (oscillating but converging) and the $y$-error by $0.5$; with $\alpha=0.9$ the $x$-error is multiplied by $1-5.4=-4.4$ and the raw-gradient iteration diverges. <!-- UNVERIFIED: check whether the slide's α=0.9 plot uses the raw or a normalized gradient. --> With exact line search the path zig-zags; the rate bound is $\left(\frac{3-1}{3+1}\right)^2=0.25$ per step.

**Gradient ascent, Lab ejercicio 6.** Maximize $f=4x_1+7x_2+x_1x_2-x_1^2-2x_2^2$, $x_0=(2,2)$, $\lambda=0.1$. $\nabla f=(4+x_2-2x_1,\;7+x_1-4x_2)$.
- $\nabla f(2,2)=(2,1)$ → $x_1=(2.2,2.1)$
- $\nabla f(x_1)=(1.7,0.8)$ → $x_2=(2.37,2.18)$
- $\nabla f(x_2)=(1.44,0.65)$ → $x_3=(2.514,2.245)$ … $x_7=(2.898,2.410)$, $f=15.43$.
Exact maximizer: $\nabla f=0\Rightarrow x^*=(\frac{23}{7},\frac{18}{7})\approx(3.286,2.571)$, $f^*=15.571$ ($H=\begin{pmatrix}-2&1\\1&-4\end{pmatrix}$ ND ⇒ global max).

**Gradient ascent, Lab ejercicios 4–5.** $f=6x_1+3x_2+x_1x_2-x_1^2-x_2^2$ → $x^*=(5,4)$, $f^*=21$. $f=5x_1+2x_2+2x_1x_2-2x_1^2-x_2^2$ → $x^*=(3.5,4.5)$, $f^*=13.25$.

**Exploding gradient (June 2025 exam).** Maximize $f=-2x_1^2-8x_2^2+8x_1+32x_2$ from $(0,0)$ with $\lambda=0.25$: $\nabla f=(8-4x_1,\,32-16x_2)$.
$x_1=(2,8)$, $\nabla f=(0,-96)$; $x_2=(2,-16)$, $\nabla f=(0,288)$; $x_3=(2,56)$, … The $x_1$-coordinate is exact after one step ($1-0.25\cdot4=0$), but the $x_2$-error is multiplied by $1-0.25\cdot16=-3$ each step. Here $\lambda_{\max}=16$, so ascent needs $\lambda<\frac{2}{16}=0.125$ — "$\lambda=0.25$ makes the gradient explode" (the exam's conclusion) is exactly this stability limit.

## See also
[[Line Search]], [[Newton's Method (Optimization)]], [[Nesterov Momentum]], [[Powell's Method]], [[Optimality Conditions (Unconstrained)]]
