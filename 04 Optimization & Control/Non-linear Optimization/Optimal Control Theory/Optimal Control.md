---
title: "Optimal Control"
domain: "Optimization & Control"
course: "Non-linear Optimization"
unit: "Optimal Control Theory"
level: BSc
status: drafted
confidence: 0
tags: [optimal-control, control-theory, ma2008b]
---
<!-- Module 6 has no lecture slides in Resources; the formulation follows the homework, labs and exam (Bolza form with F, f, φ notation) plus canonical texts (Kirk; Chiang, "Elements of Dynamic Optimization"). -->
## Definition
Classical design ([[Root Locus]], [[Frequency Response]]) produces systems that are "acceptable but not optimal." **Optimal control** instead chooses the control signal that optimizes a performance index subject to the system dynamics.

- **State variable** $x(t)\in\mathbb R^n$: describes the system (position, stock, capital…). Its evolution is given by the **state (equation of motion)** $\dot x=f(t,x,u)$.
- **Control variable** $u(t)\in U$: the decision we choose at each instant; it affects $x$ only through $f$.
- **Objective functional** (Bolza form):
$$J[u]=\phi\big(x(T)\big)+\int_0^TF\big(t,x(t),u(t)\big)\,dt\;\to\;\max\ (\text{or }\min),$$
with $F$ the running payoff/cost and $\phi$ a terminal (scrap) value.
- **Boundary conditions:** $x(0)=x_0$ given; the terminal state is either **fixed** ($x(T)=x_T$), **free**, or constrained; $T$ may be fixed or free.

A pair $(u^*,x^*)$ satisfying the dynamics and boundary conditions and optimizing $J$ is an **optimal control / optimal trajectory**.

## Properties
### Relation to the calculus of variations
If $f(t,x,u)=u$ (i.e. $\dot x=u$), the problem becomes $\max\int F(t,x,\dot x)\,dt$, the basic [[Calculus of Variations]] problem, whose necessary condition is the [[Euler-Lagrange Equation]]. Optimal control generalizes it by allowing arbitrary dynamics and control constraints (e.g. $u\in[a,b]$, giving bang-bang solutions).

### Necessary conditions
The main tool is [[Pontryagin's Maximum Principle]]: introduce a costate $\lambda(t)$ (a dynamic [[Lagrange Multipliers|Lagrange multiplier]]) and the Hamiltonian $H=F+\lambda f$; the optimal control maximizes $H$ pointwise.

### Other approaches
- [[Dynamic Programming]] / the [[Hamilton-Jacobi-Bellman Equation]] — gives sufficient conditions and feedback laws.
- The linear–quadratic case ($\dot x=Ax+Bu$, quadratic cost) yields the [[Linear-quadratic regulator (LQR)]], which connects back to [[State-Space Representation|state-space]] design.
- Direct numerical methods: discretize and solve a [[Nonlinear Programming Problem]].

### Why the state-space form is natural here
The course slides note that for optimal control problems the [[State-Space Representation]] is the most convenient model, since the dynamics enter as $\dot x=f(x,u)$ directly.

## Examples
A typical homework instance: maximize $J=\int_0^3(3x-5u^2)\,dt$ subject to $\dot x=4u-2$, $x(0)=1$, $x(3)$ free. Here $F=3x-5u^2$, $f=4u-2$, $\phi=0$. The payoff rewards a large state but penalizes control effort quadratically; the solution balances the two (see [[Pontryagin's Maximum Principle]] for the full solution).

## See also
[[Pontryagin's Maximum Principle]], [[State-Space Representation]], [[Linear-quadratic regulator (LQR)]], [[Dynamic Programming]], [[Nonlinear Programming Problem]]
