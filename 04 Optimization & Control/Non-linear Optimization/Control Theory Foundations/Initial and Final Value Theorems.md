---
title: "Initial and Final Value Theorems"
domain: "Optimization & Control"
course: "Non-linear Optimization"
unit: "Control Theory Foundations"
level: BSc
status: drafted
confidence: 0
tags: [control-theory, ma2008b]
---
## Definition
Let $F(s)=\mathcal L\{f(t)\}$ (see [[Laplace Transform]]) with $f,f'$ transformable.

**Initial value theorem.** $\displaystyle f(0^+)=\lim_{t\to0^+}f(t)=\lim_{s\to\infty}sF(s)$.

**Final value theorem.** If $\lim_{t\to\infty}f(t)$ exists — equivalently, all poles of $sF(s)$ lie in the open left half-plane — then
$$f(\infty)=\lim_{t\to\infty}f(t)=\lim_{s\to0}sF(s).$$

## Properties
### Proof sketch (both theorems)
Start from the derivative rule: $\int_0^\infty f'(t)e^{-st}dt=sF(s)-f(0)$.

- **Final value:** let $s\to0$. The left side becomes $\int_0^\infty f'(t)dt=f(\infty)-f(0)$ (interchange of limit and integral justified when $f(\infty)$ exists). So $\lim_{s\to0}sF(s)-f(0)=f(\infty)-f(0)$.
- **Initial value:** let $s\to\infty$. Since $e^{-st}\to0$ for every $t>0$ and $f'$ is of exponential order, the left side tends to $0$ (dominated convergence), so $\lim_{s\to\infty}sF(s)=f(0^+)$.

### The hypothesis matters
If $F(s)=\frac{\omega}{s^2+\omega^2}$ ($f=\sin\omega t$), then $\lim_{s\to0}sF(s)=0$, yet $f$ has no limit — the poles $\pm j\omega$ violate the condition. Likewise $F=\frac1{s-1}$ gives $0$ while $e^t\to\infty$. Always check pole locations ([[BIBO Stability and Pole Location]]) before applying the theorem.

### Use in control
For a stable closed loop with transfer function $T(s)$ and unit-step input, the steady-state output is $y(\infty)=\lim_{s\to0}s\,T(s)\frac1s=T(0)$ (the DC gain). This underlies steady-state error analysis ([[Steady-State Error]]).

## Examples
- $F(s)=\frac{10}{s(s+1)}$: $f(\infty)=\lim_{s\to0}\frac{10}{s+1}=10$; poles of $sF$ are $\{-1\}$, so the theorem applies (Actividad 1).
- RC circuit with constant source $E_0$, $q(0)=0$: $Q(s)=\frac{E_0}{s(Rs+1/C)}$, so $q(\infty)=\lim_{s\to0}\frac{E_0}{Rs+1/C}=E_0C$ — the capacitor charges fully, read off without inverting.
- Initial value of the same: $\lim_{s\to\infty}\frac{E_0}{Rs+1/C}=0=q(0)$ ✓.

## See also
[[Laplace Transform]], [[Convolution Theorem (Laplace)]], [[First-Order System Response]], [[Transfer Function]]
