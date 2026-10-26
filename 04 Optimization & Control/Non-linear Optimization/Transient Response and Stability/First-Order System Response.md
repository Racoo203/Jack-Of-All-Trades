---
title: "First-Order System Response"
domain: "Optimization & Control"
course: "Non-linear Optimization"
unit: "Transient Response and Stability"
level: BSc
status: drafted
confidence: 0
tags: [control-theory, transient-response, ma2008b]
---
## Definition
A **first-order system** obeys
$$\tau\frac{dy}{dt}+y=K\,u(t)\qquad\Longleftrightarrow\qquad G(s)=\frac{Y(s)}{U(s)}=\frac{K}{\tau s+1},$$
where $K$ is the **static (DC) gain** and $\tau>0$ the **time constant**. Equivalently $\dot y+ay=ku$ with $\tau=1/a$, $K=k/a$. The single pole is $s=-1/\tau$. Physical examples in the slides: RC circuit ($RC\,\dot v_C+v_C=v_s$, $\tau=RC$, $K=1$), a draining tank ($\dot h=u-kh$), a falling body with linear drag ($m\dot v=mg-kv$), a cooling body.

## Properties
### Unit-step response
With $U(s)=1/s$ (see [[Transfer Function]], [[Laplace Transform]]):
$$Y(s)=\frac{K}{s(\tau s+1)}=\frac{K}{s}-\frac{K\tau}{\tau s+1}=\frac Ks-\frac{K}{s+1/\tau}\;\Longrightarrow\;y(t)=K\left(1-e^{-t/\tau}\right),\;t\ge0.$$
- **Final value:** $y(\infty)=K$ (also from the [[Initial and Final Value Theorems|final value theorem]]: $\lim_{s\to0}\frac{K}{\tau s+1}=K$).
- **At $t=\tau$:** $y(\tau)=K(1-e^{-1})=0.632K$ — the time constant is the time to reach **63.2 %** of the final value.
- $y(2\tau)=0.865K$, $y(3\tau)=0.950K$, $y(4\tau)=0.982K$, $y(5\tau)=0.993K$.
- **Settling time:** $T_s\approx4\tau$ (2 % criterion); $T_s\approx5\tau$ for 1 %; $3\tau$ for 5 %.
- **Initial slope:** $\dot y(0)=K/\tau$. The tangent at the origin reaches the final value $K$ exactly at $t=\tau$ — this is how $\tau$ is read from a measured curve.
- Smaller $\tau$ ⇒ faster response; larger $\tau$ ⇒ slower.

### Unit-ramp response
$U(s)=1/s^2$, take $K=1$:
$$Y(s)=\frac{1}{s^2(\tau s+1)}=\frac As+\frac B{s^2}+\frac{C}{\tau s+1}.$$
Clearing denominators, $As(\tau s+1)+B(\tau s+1)+Cs^2=1$. At $s=0$: $B=1$. At $s=-1/\tau$: $C/\tau^2=1\Rightarrow C=\tau^2$. Coefficient of $s^2$: $A\tau+C=0\Rightarrow A=-\tau$. So
$$y(t)=t-\tau+\tau e^{-t/\tau},\qquad e(t)=t-y(t)=\tau\left(1-e^{-t/\tau}\right)\to\tau.$$
The output lags the ramp by $\tau$ in steady state: **the smaller $\tau$, the smaller the steady-state error**.

### Unit-impulse response
$U(s)=1$: $y(t)=\dfrac1\tau e^{-t/\tau}$. At $t=\tau$, $y(\tau)=\frac1\tau e^{-1}=0.368\cdot\frac1\tau$, i.e. **36.8 % of the initial value** $1/\tau$. (The slide phrases this as "36.7 % of the final value"; the reference level is the peak at $t=0$, since the final value is $0$.)

### Response relations
Impulse, step and ramp responses are successive integrals of each other (because $\frac1s$ = integration), a property of every [[Linear Time-Invariant System|LTI system]].

### First order with dead time
$G(s)=\dfrac{Ke^{-as}}{\tau s+1}$. By the second translation theorem, the step response is the undelayed one shifted by $a$:
$$y(t)=K\left(1-e^{-(t-a)/\tau}\right)\mathcal U(t-a).$$

## Examples
**RC settling time (slides).** $R=10\,\Omega$, $C=470\,\mu$F: $\tau=RC=0.0047$ s, $T_s=4\tau\approx0.0188$ s. MATLAB: `G=tf(1,[R*C 1]); step(G)`.

**Reading $\tau$ from a model.** $f(t)=4-3e^{-2t}$ approaches 4 with rate $2$, so $\tau=1/2$.

**Exercise (slides).** $\dfrac{Y}{U}=\dfrac{3}{4s+2}=\dfrac{3/2}{2s+1}$ ⇒ $K=\tfrac32$, $\tau=2$ s, $T_s=4\tau=8$ s, $y(\infty)=\tfrac32$, and
$$Y(s)=\frac{3/4}{s(s+1/2)}=\frac{3/2}{s}-\frac{3/2}{s+1/2}\;\Rightarrow\;y(t)=\tfrac32\left(1-e^{-t/2}\right).$$

## See also
[[Second-Order System Response]], [[Transfer Function]], [[Unit Step and Dirac Delta Functions]], [[Steady-State Error]], [[Mechanical and Electrical System Models]]
