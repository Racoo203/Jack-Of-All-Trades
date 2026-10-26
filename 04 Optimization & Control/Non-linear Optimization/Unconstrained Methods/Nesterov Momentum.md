---
title: "Nesterov Momentum"
domain: "Optimization & Control"
course: "Non-linear Optimization"
unit: "Unconstrained Methods"
level: BSc
status: seeding
confidence: 0
tags: [nonlinear-optimization, numerical-methods, ma2008b]
---
## Definition
**Nesterov's accelerated gradient (NAG)** adds a velocity term to gradient descent and evaluates the gradient at a **look-ahead point** rather than at the current iterate.

**Form used in the course labs (Laboratorio Multimodal, June 2025):** with learning rate $\lambda$, momentum $\beta\in[0,1)$, $v_0=0$,
$$\tilde x_k=x_k+\beta v_k,\qquad v_{k+1}=\beta v_k-\lambda(1-\beta)\,\nabla f(\tilde x_k),\qquad x_{k+1}=x_k+v_{k+1}.$$
<!-- UNVERIFIED: the (1-β) damping factor is the labs' convention (EMA-style momentum); no Nesterov slide is in Resources. The textbook form (Sutskever et al., 2013) is v_{k+1} = β v_k − λ ∇f(x_k + β v_k). Check against the professor's material. -->

**Textbook form:** $v_{k+1}=\beta v_k-\lambda\nabla f(x_k+\beta v_k)$, $x_{k+1}=x_k+v_{k+1}$. The two are equivalent up to rescaling the learning rate ($\lambda_{\text{text}}=\lambda(1-\beta)$).

## Properties
### Intuition
Plain momentum ("heavy ball", $v_{k+1}=\beta v_k-\lambda\nabla f(x_k)$) accumulates past gradients, damping the zig-zag of [[Steepest Descent]] across narrow valleys and speeding motion along them. Nesterov's correction first moves by the momentum and then measures the gradient there, so it "sees" an overshoot one step earlier and brakes sooner.

### Convergence rate
For convex $f$ with $L$-Lipschitz gradient, a suitable schedule of $\beta_k$ gives $f(x_k)-f^*=O(1/k^2)$, versus $O(1/k)$ for gradient descent — optimal among first-order methods (Nesterov, 1983). For $\mu$-strongly convex $f$, a constant $\beta=\frac{\sqrt\kappa-1}{\sqrt\kappa+1}$ gives a linear rate $\approx(1-1/\sqrt\kappa)$ instead of $(1-1/\kappa)$, where $\kappa=L/\mu$.

### Quadratic analysis
For $f=\frac12x^TQx$, each eigen-component with eigenvalue $q$ follows a linear second-order recursion; the iteration is stable when its characteristic roots lie inside the unit circle. With the course form, the effective step is $\lambda(1-\beta)$, so the step-size limit of gradient descent is relaxed by the factor $1-\beta$ (a larger nominal $\lambda$ is tolerated).

## Examples
**Lab ejercicio 7.** Minimize $f=x^2+3y^2$ with $\lambda=0.1$, $\beta=0.9$, $x_0=(4,2)$, $v_0=0$; $\nabla f=(2x,6y)$.
- $k=0$: $\tilde x_0=(4,2)$, $\nabla f=(8,12)$, $v_1=-0.1(0.1)(8,12)=(-0.08,-0.12)$, $x_1=(3.92,1.88)$.
- $k=1$: $\tilde x_1=(3.92,1.88)+0.9(-0.08,-0.12)=(3.848,1.772)$, $\nabla f=(7.696,10.632)$, $v_2=0.9(-0.08,-0.12)-0.01(7.696,10.632)=(-0.149,-0.214)$, $x_2=(3.771,1.666)$.
- $k=2$: $x_3=(3.564,1.384)$; $k=3$: $x_4=(3.311,1.063)$ … converging to the minimum $(0,0)$ with accelerating steps.

**June 2025 exam, problem 2.** $f=(x-2)^2+(y-4)^2$, $x_0=v_0=0$: $\nabla f(\tilde x_0)=(-4,-8)$, $v_1=-(0.5)(0.5)(-4,-8)=(1,2)$, $x_1=(1,2)$; $\tilde x_1=(1,2)+0.9(1,2)=(1.9,3.8)$, $\nabla f=(-0.2,-0.4)$, $v_2=0.9(1,2)+0.25(0.2,0.4)=(0.95,1.9)$, $x_2=(1.95,3.9)$.
Note the sheet mixes parameters: the look-ahead uses $0.9$ while the gradient factor is $0.5\times0.5$ (i.e. $\lambda=0.5$ with $1-\beta=0.5$, which would imply $\beta=0.5$). <!-- UNVERIFIED: confirm the intended β for this exam problem. -->

## See also
[[Steepest Descent]], [[Line Search]], [[Newton's Method (Optimization)]], [[Stochastic Gradient Descent]]
