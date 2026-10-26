---
title: "Transfer Function"
domain: "Optimization & Control"
course: "Non-linear Optimization"
unit: "Control Theory Foundations"
level: BSc
status: drafted
confidence: 0
tags: [control-theory, ma2008b]
---
## Definition
Consider a [[Linear Time-Invariant System]] described by the linear constant-coefficient ODE (Ogata §2-2, the reading for the course's transfer-function quiz)
$$a_0y^{(n)}+a_1y^{(n-1)}+\dots+a_{n-1}\dot y+a_ny=b_0x^{(m)}+b_1x^{(m-1)}+\dots+b_{m-1}\dot x+b_mx,\qquad n\ge m,$$
with output $y$ and input $x$. The **transfer function** is the ratio of the [[Laplace Transform]] of the output to that of the input, **with all initial conditions equal to zero**:
$$G(s)=\frac{\mathcal L[\text{output}]}{\mathcal L[\text{input}]}\bigg|_{\text{zero ICs}}=\frac{Y(s)}{X(s)}=\frac{b_0s^m+b_1s^{m-1}+\dots+b_m}{a_0s^n+a_1s^{n-1}+\dots+a_n}.$$
If the highest power of $s$ in the denominator is $n$, the system is called an **$n$-th order system**. Roots of the numerator are **zeros**, roots of the denominator are **poles**.

## Properties
### Derivation
Apply the derivative rule $\mathcal L\{y^{(k)}\}=s^kY(s)-\sum_{j}s^{k-1-j}y^{(j)}(0)$ to every term. With all $y^{(j)}(0)=x^{(j)}(0)=0$ the initial-condition terms vanish and each derivative becomes multiplication by $s^k$:
$$(a_0s^n+\dots+a_n)\,Y(s)=(b_0s^m+\dots+b_m)\,X(s),$$
and dividing gives $G(s)$. The zero-IC assumption is essential: with nonzero ICs, $Y(s)=G(s)X(s)+(\text{IC terms})/D(s)$, which is not proportional to $X(s)$.

### Comments (Ogata, reproduced in the course slides)
1. Applicable only to systems described by linear time-invariant ODEs.
2. It is a property of the system, **independent of the magnitude and nature of the input**.
3. It carries the units relating input and output but **no information about physical structure** — physically different systems can share the same $G(s)$ (compare [[Mechanical and Electrical System Models|a mass–spring–damper and an RLC circuit]]).
4. Knowing $G(s)$, the response to any input can be studied; not knowing it, $G(s)$ can be identified experimentally by applying known inputs.

### Impulse response and the convolution integral
Since $Y(s)=G(s)X(s)$, the [[Convolution Theorem (Laplace)|convolution theorem]] gives
$$y(t)=\int_0^t x(\tau)\,g(t-\tau)\,d\tau,\qquad g(t)=\mathcal L^{-1}\{G(s)\}.$$
For a unit impulse input, $X(s)=\mathcal L\{\delta(t)\}=1$ (see [[Unit Step and Dirac Delta Functions]]), so $Y(s)=G(s)$ and the output is $g(t)$ — the **impulse response** (or *weighting function*). Hence the transfer function and the impulse response **contain the same information** about the dynamics (the quiz statement claiming they do not is **false**).

### Poles, response and stability
Partial fractions of $Y(s)$ show that each pole $p$ contributes a term $e^{pt}$ (times polynomials in $t$ for repeated poles). So the pole locations determine the natural response and [[BIBO Stability and Pole Location|stability]].

### Closed loop and state space
- For a feedback loop with forward path $G$ and feedback $H$: $T(s)=\dfrac{G}{1+GH}$ (see [[Control System Fundamentals]], [[Block Diagram Reduction]]).
- From a [[State-Space Representation]]: $G(s)=C(sI-A)^{-1}B+D$.

## Examples
- $y''+3y'+2y=m(t)$ → $G(s)=\dfrac{1}{(s+1)(s+2)}$; poles $-1,-2$.
- Series RC with charge output: $Rq'+q/C=E(t)$ → $G(s)=\dfrac{Q(s)}{E(s)}=\dfrac{1}{Rs+1/C}$, single pole $s=-1/(RC)$.
- Satellite attitude (rotational, no friction): $J\ddot\theta=T$ → $G(s)=\dfrac{\Theta(s)}{T(s)}=\dfrac{1}{Js^2}$ (double pole at the origin — not asymptotically stable).

## See also
[[Laplace Transform]], [[State-Space Representation]], [[Block Diagram Reduction]], [[Mechanical and Electrical System Models]], [[First-Order System Response]], [[Frequency Response]]
