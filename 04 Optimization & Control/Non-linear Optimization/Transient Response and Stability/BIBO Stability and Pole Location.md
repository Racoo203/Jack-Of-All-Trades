---
title: "BIBO Stability and Pole Location"
domain: "Optimization & Control"
course: "Non-linear Optimization"
unit: "Transient Response and Stability"
level: BSc
status: drafted
confidence: 0
tags: [control-theory, stability, ma2008b]
---
## Definition
Stability is the most basic requirement of a control system (it prevents loss of control and equipment damage). The slides distinguish three questions: **absolute stability** (yes/no, qualitative), **relative stability** (how stable — quantitative, e.g. [[Gain and Phase Margins]]), and **robustness** (how much the plant can be perturbed and remain stable).

For a [[Linear Time-Invariant System]] with impulse response ("weighting function") $w(t)$ and closed-loop transfer function
$$T(s)=\frac{N(s)}{D(s)},\qquad D(s)=a_ns^n+\dots+a_1s+a_0,$$
the following are **equivalent definitions of stability** (slides):
1. **BIBO:** every bounded input produces a bounded output.
2. $w$ is absolutely integrable: $\int_0^\infty|w(t)|\,dt<\infty$.
3. All poles of $T(s)$ lie in the open left half of the $s$-plane.
4. $w(t)\to0$ as $t\to\infty$.
5. (State space) all eigenvalues of $A$ have negative real part (see [[State-Space Representation]]).

**Classification by the roots of $D(s)$:** *asymptotically stable* if all roots are in the open LHP; *marginally stable* if none is in the RHP and the roots on the $j\omega$ axis are simple; *unstable* if some root has positive real part or a $j\omega$-axis root is repeated.

## Properties
### (2) ⇒ (1)
Output by convolution (see [[Convolution Theorem (Laplace)]]): $y(t)=\int_0^tw(\tau)u(t-\tau)\,d\tau$. If $|u|\le M$,
$$|y(t)|\le M\int_0^t|w(\tau)|\,d\tau\le M\int_0^\infty|w|<\infty.$$
Conversely (1) ⇒ (2): if $\int|w|=\infty$, the bounded input $u(t-\tau)=\operatorname{sgn}w(\tau)$ on $[0,t]$ gives $y(t)=\int_0^t|w|\to\infty$.

### (3) ⇔ (2)
Partial fractions write $w(t)=\sum_i\sum_r c_{ir}\,t^{r}e^{p_it}$ over poles $p_i$ with multiplicity. Each term $t^re^{p_it}$ is absolutely integrable iff $\operatorname{Re}p_i<0$ (for $\operatorname{Re}p_i<0$, $\int_0^\infty t^re^{\operatorname{Re}(p_i)t}dt=r!/|\operatorname{Re}p_i|^{r+1}$; otherwise the modulus does not decay). A simple pole on the $j\omega$ axis gives a non-decaying bounded term — bounded impulse response but **not** BIBO stable (a sinusoid at that frequency causes resonance), which is why such systems are called only *marginally* stable. A repeated $j\omega$ pole gives $t\sin\omega t$, which is unbounded.

### Necessary condition on coefficients ("initial screening")
If all roots are in the LHP, $D(s)=a_n\prod(s+\alpha_i)\prod\big((s+\sigma_k)^2+\omega_k^2\big)$ with $\alpha_i,\sigma_k>0$; expanding a product of polynomials with positive coefficients gives **all coefficients present and of the same sign**. Hence a missing or sign-changed coefficient ⇒ not stable. The condition is **necessary but not sufficient** (e.g. $s^3+s^2+2s+8=(s+2)(s^2-s+4)$ has all coefficients positive but RHP roots $0.5\pm j1.94$). The complete test is the [[Routh-Hurwitz Criterion]].

### Examples of $D(s)$ requested in class
- At least one RHP root: $(s-1)(s+2)=s^2+s-2$.
- Repeated roots on the $j\omega$ axis: $(s^2+1)^2=s^4+2s^2+1$ (unstable).
- All roots in the RHP: $(s-1)(s-2)=s^2-3s+2$.

## See also
[[Routh-Hurwitz Criterion]], [[Root Locus]], [[Nyquist Stability Criterion]], [[Transfer Function]], [[Initial and Final Value Theorems]]
