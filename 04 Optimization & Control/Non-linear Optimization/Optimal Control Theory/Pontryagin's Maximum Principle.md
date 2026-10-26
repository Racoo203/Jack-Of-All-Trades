---
title: "Pontryagin's Maximum Principle"
domain: "Optimization & Control"
course: "Non-linear Optimization"
unit: "Optimal Control Theory"
level: BSc
status: drafted
confidence: 0
tags: [optimal-control, ma2008b, exam]
---
## Definition
For the [[Optimal Control]] problem
$$\max_{u}\;J=\phi(x(T))+\int_0^TF(t,x,u)\,dt\quad\text{s.t.}\quad\dot x=f(t,x,u),\;x(0)=x_0,$$
define the **Hamiltonian**
$$H(t,x,u,\lambda)=F(t,x,u)+\lambda(t)\,f(t,x,u),$$
where $\lambda(t)$ is the **costate** (adjoint variable). **Pontryagin's Maximum Principle** states that if $(u^*,x^*)$ is optimal, there is a continuous $\lambda(t)$ such that
1. **Maximum condition:** $H(t,x^*,u^*,\lambda)\ge H(t,x^*,u,\lambda)$ for all admissible $u$. For an interior optimum with $u$ unconstrained: $\dfrac{\partial H}{\partial u}=0$ and $\dfrac{\partial^2H}{\partial u^2}\le0$.
2. **State equation:** $\dot x=\dfrac{\partial H}{\partial\lambda}=f(t,x,u)$.
3. **Costate equation:** $\dot\lambda=-\dfrac{\partial H}{\partial x}$.
4. **Transversality (boundary) condition:** if $x(T)$ is free, $\lambda(T)=\dfrac{\partial\phi}{\partial x}\Big|_{t=T}$ (so $\lambda(T)=0$ when $\phi=0$); if $x(T)=x_T$ is fixed, $\lambda(T)$ is free and $x(T)=x_T$ is used instead.

For a **minimization** problem, $H$ must be **minimized** in $u$ (equivalently, maximize $-J$).

### The course's 5-step recipe (labs and exam)
① Write $H=F+\lambda f$. ② Solve $\lambda'=-\partial H/\partial x$. ③ Apply $\lambda(t_f)=\partial\phi(t_f)/\partial x$ (or keep the constant for a fixed endpoint). ④ Set $\partial H/\partial u=0$ and solve for $u$ in terms of $\lambda$. ⑤ Substitute into $x'=f$, integrate, and use $x(0)$ (and $x(T)$ if fixed).

## Properties
### Heuristic derivation (variational argument)
Adjoin the dynamics with a multiplier function:
$$\bar J=\phi(x(T))+\int_0^T\big[F+\lambda(f-\dot x)\big]dt=\phi(x(T))+\int_0^T\big[H-\lambda\dot x\big]dt.$$
Integrate $-\int\lambda\dot x$ by parts: $-\int_0^T\lambda\dot x\,dt=-\lambda(T)x(T)+\lambda(0)x(0)+\int_0^T\dot\lambda x\,dt$. So
$$\bar J=\phi(x(T))-\lambda(T)x(T)+\lambda(0)x_0+\int_0^T\big[H+\dot\lambda x\big]dt.$$
Perturb $u\to u^*+\varepsilon\,\delta u$, which induces $x\to x^*+\varepsilon\,\delta x$ with $\delta x(0)=0$. The first variation is
$$\delta\bar J=\big[\phi_x-\lambda(T)\big]\delta x(T)+\int_0^T\Big[(H_x+\dot\lambda)\,\delta x+H_u\,\delta u\Big]dt.$$
Choosing $\lambda$ to kill the coefficient of $\delta x$ gives the **costate equation** $\dot\lambda=-H_x$ and the **transversality condition** $\lambda(T)=\phi_x$ (when $\delta x(T)$ is free; if $x(T)$ is fixed, $\delta x(T)=0$ and no condition on $\lambda(T)$ arises). Then $\delta\bar J=\int H_u\delta u\,dt$ must vanish for every $\delta u$, so $H_u=0$ at an interior optimum. The full theorem (with $H$ maximized even when $u$ is bounded and $H$ not differentiable) needs needle variations; the above is the smooth special case.

### Second-order check — do not skip it
$H_u=0$ only gives a *stationary* point of $H$. For a maximization with unconstrained $u$ one needs $H_{uu}\le0$ (typically $F$ concave in $u$). If $H$ is **convex** in $u$ in a maximization problem (or concave in a minimization), the stationary point is the *worst* choice and, with unbounded $u$, the problem has no optimal solution (the objective is unbounded).

### Sufficiency (Mangasarian)
If $H$ is jointly concave in $(x,u)$ for the $\lambda(t)$ found (for a maximization), the conditions are also sufficient.

### Interpretation of $\lambda$
$\lambda(t)$ is the **shadow value** of the state: the marginal change of the optimal value per unit of extra $x$ at time $t$. $\lambda(T)=0$ says a free terminal state has no value beyond $T$.

## Examples
**Exam, Problem 1.** $\max\int_0^2(e^{3t}x-u^2)dt$, $\dot x=u$, $x(0)=3$, $x(2)$ free.
① $H=e^{3t}x-u^2+\lambda u$. ② $\dot\lambda=-e^{3t}\Rightarrow\lambda=-\tfrac13e^{3t}+C_1$. ③ $\lambda(2)=0\Rightarrow C_1=\tfrac13e^6$, $\lambda=\tfrac13(e^6-e^{3t})$. ④ $H_u=-2u+\lambda=0\Rightarrow u=\tfrac\lambda2=\tfrac16(e^6-e^{3t})$; $H_{uu}=-2<0$ ✓. ⑤ $\dot x=u\Rightarrow x=\tfrac16e^6t-\tfrac1{18}e^{3t}+C_2$, $x(0)=3\Rightarrow C_2=3+\tfrac1{18}=\tfrac{55}{18}$:
$$x^*(t)=-\tfrac1{18}e^{3t}+\tfrac16e^6t+\tfrac{55}{18}.$$

**Exam, Problem 2 (fixed endpoint).** $\max\int_0^3(x-u^2)dt$, $\dot x=u-x$, $x(0)=2$, $x(3)=e^2$.
$H=x-u^2+\lambda(u-x)$; $\dot\lambda=-(1-\lambda)\Rightarrow\lambda=1+C_1e^t$; $H_u=0\Rightarrow u=\tfrac12+\tfrac{C_1}{2}e^t$ ($H_{uu}=-2$ ✓). Then $\dot x+x=\tfrac12+\tfrac{C_1}2e^t\Rightarrow x=\tfrac12+C_3e^t+C_2e^{-t}$ with $C_3=C_1/4$. Boundary conditions: $C_3+C_2=\tfrac32$ and $\tfrac12e^3+C_3e^6+C_2=e^5$, so
$$C_3=\frac{2e^5-e^3-3}{2(e^6-1)}\approx0.340,\qquad C_2=\frac{3e^6-2e^5+e^3}{2(e^6-1)}\approx1.160,$$
$$x^*(t)=\tfrac12+0.340\,e^t+1.160\,e^{-t}.$$

**Exam, Problem 3 (fixed endpoint).** $\max\int_0^2(7t^2x-4u^2)dt$, $\dot x=u$, $x(0)=0$, $x(2)=2$.
$\dot\lambda=-7t^2\Rightarrow\lambda=-\tfrac73t^3+C_1$; $H_u=-8u+\lambda=0\Rightarrow u=-\tfrac7{24}t^3+\tfrac{C_1}8$; $x=-\tfrac7{96}t^4+C_3t+C_2$. $x(0)=0\Rightarrow C_2=0$; $x(2)=2\Rightarrow-\tfrac76+2C_3=2\Rightarrow C_3=\tfrac{19}{12}$:
$$x^*(t)=-\tfrac{7}{96}t^4+\tfrac{19}{12}t.$$

**Ejercicios 1 (Apr 2025).** $\max\int_0^2(3y-2u^2)dt$, $\dot y=3u-1$, $y(0)=1$: $\lambda=-3t+6$, $u=\tfrac34\lambda=-\tfrac94(t-2)$, $y^*=-\tfrac{27}8t^2+\tfrac{25}2t+1$.

**Tarea, Problem 1.** $\max\int_0^3(3x-5u^2)dt$, $\dot x=4u-2$, $x(0)=1$: $\dot\lambda=-3$, $\lambda(3)=0\Rightarrow\lambda=9-3t$; $H_u=-10u+4\lambda=0\Rightarrow u^*=3.6-1.2t$ ($H_{uu}=-10<0$ ✓); $\dot x=12.4-4.8t\Rightarrow x^*=1+12.4t-2.4t^2$.

**Tarea, Problems 2 and 3 — ill-posed as stated.**
- Problem 3 ($\max\int_0^1(x+2u^2)dt$, $\dot x=u$, $x(0)=0$): $H=x+2u^2+\lambda u$ has $H_{uu}=+4>0$. The recipe gives $\lambda=1-t$, $u=-\lambda/4=\tfrac t4-\tfrac14$, $x=\tfrac18t^2-\tfrac14t$ (the lab's answer), but this $u$ **minimizes** $H$. Indeed $J$ is unbounded above: $u\equiv c$ gives $J=\tfrac c2+2c^2\to\infty$. No maximum exists.
- Problem 2 ($\min\int_0^1(5x-4u-u^2)dt$, $\dot x=x+u$, $x(0)=1$): $H_{uu}=-2<0$, so $H_u=0$ ($u=\tfrac{\lambda-4}{2}$ with $\lambda=5e^{1-t}-5$) **maximizes** $H$, whereas a minimization needs $H$ minimized; $J$ is unbounded below ($u\equiv c$, $c\to\infty$).
Either the problems intend the opposite sense of optimization, or bounded controls. Flag for the professor.

## See also
[[Optimal Control]], [[Lagrange Multipliers]], [[Calculus of Variations]], [[Hamilton-Jacobi-Bellman Equation]], [[Linear-quadratic regulator (LQR)]]
