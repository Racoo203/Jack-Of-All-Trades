---
title: "Laplace Transform"
domain: "Optimization & Control"
course: "Non-linear Optimization"
unit: "Control Theory Foundations"
level: BSc
status: drafted
confidence: 0
tags: [control-theory, differential-equations, ma2008b]
---
## Definition
Let $f:[0,\infty)\to\mathbb R$ be **piecewise continuous** and of **exponential order** $\alpha$ (there are $M,T$ with $|f(t)|\le Me^{\alpha t}$ for $t>T$). Its Laplace transform is

$$\mathcal L\{f(t)\}=F(s)=\int_0^\infty f(t)\,e^{-st}\,dt,\qquad \operatorname{Re}(s)>\alpha,$$

with $s=\sigma+j\omega$ a complex variable. The integral is an [[Improper Integral]]; the conditions guarantee convergence since $|f(t)e^{-st}|\le Me^{-(\sigma-\alpha)t}$.

The transform turns a [[Linear Ordinary Differential Equation|linear ODE with constant coefficients]] into an algebraic equation in $s$, which is the basis of the [[Transfer Function]].

## Properties
### Linearity
$\mathcal L\{af_1+bf_2\}=aF_1(s)+bF_2(s)$, immediate from linearity of the integral.

### Basic transforms
- $\mathcal L\{1\}=\int_0^\infty e^{-st}dt=\left[-\tfrac{1}{s}e^{-st}\right]_0^\infty=\frac1s$ ($s>0$).
- $\mathcal L\{e^{at}\}=\int_0^\infty e^{-(s-a)t}dt=\frac{1}{s-a}$ ($s>a$). E.g. $\mathcal L\{e^{-6t}\}=\frac1{s+6}$.
- $\mathcal L\{t^n\}=\frac{n!}{s^{n+1}}$ (induction with integration by parts).
- $\mathcal L\{\sin\omega t\}=\frac{\omega}{s^2+\omega^2}$, $\mathcal L\{\cos\omega t\}=\frac{s}{s^2+\omega^2}$ — take real/imaginary parts of $\mathcal L\{e^{j\omega t}\}=\frac{1}{s-j\omega}=\frac{s+j\omega}{s^2+\omega^2}$.

### Transform of a derivative
Integrating by parts with $u=f(t)$, $dv=e^{-st}dt$... more directly, with $u=e^{-st}$, $dv=f'(t)dt$:

$$\mathcal L\{f'\}=\big[e^{-st}f(t)\big]_0^\infty+s\int_0^\infty f(t)e^{-st}dt=sF(s)-f(0).$$

Applying this repeatedly:

$$\mathcal L\{f^{(n)}\}=s^nF(s)-s^{n-1}f(0)-s^{n-2}f'(0)-\dots-f^{(n-1)}(0).$$

The subtracted terms are exactly the initial conditions; setting them to zero is what defines the [[Transfer Function]].

### Transform of an integral
Let $g(t)=\int_0^t f(\tau)d\tau$, so $g'=f$ and $g(0)=0$. Then $F(s)=sG(s)-0$, hence $\mathcal L\left\{\int_0^t f\right\}=\frac{F(s)}{s}$; for $n$ nested integrals, $F(s)/s^n$.

### First translation theorem (shift in $s$)
$$\mathcal L\{e^{at}f(t)\}=\int_0^\infty f(t)e^{-(s-a)t}dt=F(s-a).$$
Example: $\mathcal L\{5e^{-3t}\sin 2t\}=5\cdot\frac{2}{(s+3)^2+4}=\frac{10}{s^2+6s+13}$.

### Second translation theorem (shift in $t$)
With the [[Unit Step and Dirac Delta Functions|unit step]] $\mathcal U(t-a)$, $a>0$:
$$\mathcal L\{f(t-a)\,\mathcal U(t-a)\}=\int_a^\infty f(t-a)e^{-st}dt\overset{\tau=t-a}{=}e^{-as}\int_0^\infty f(\tau)e^{-s\tau}d\tau=e^{-as}F(s).$$
Equivalent form used in class: $\mathcal L\{f(t)\,\mathcal U(t-a)\}=e^{-as}\,\mathcal L\{f(t+a)\}$. Inverse form: $\mathcal L^{-1}\{e^{-as}F(s)\}=f(t-a)\,\mathcal U(t-a)$.

### Inverse transform and partial fractions
$\mathcal L^{-1}$ is computed by decomposing $F(s)$ into [[Partial Fraction Decomposition|partial fractions]]. For distinct real linear factors the "cover-up" rule gives the coefficient of $\frac{1}{s-p}$ as $\lim_{s\to p}(s-p)F(s)$.

Other key results have their own notes: [[Convolution Theorem (Laplace)]], [[Initial and Final Value Theorems]].

## Examples
**ODE by Laplace (slides, Ejemplo 1).** $y''+3y'+2y=m(t)$, $y(0)=a$, $y'(0)=b$:
$$s^2Y-sa-b+3(sY-a)+2Y=M(s)\;\Rightarrow\;Y(s)(s^2+3s+2)=M(s)+as+b+3a.$$
With zero ICs, $G(s)=\frac{Y}{M}=\frac{1}{(s+1)(s+2)}$. With $m=0$, $Y(s)=\frac{as+(b+3a)}{(s+1)(s+2)}=\frac{2a+b}{s+1}-\frac{a+b}{s+2}$, so $y(t)=(2a+b)e^{-t}-(a+b)e^{-2t}$.

**RC circuit with delayed step (slides, Problema 1).** $R=2.5\,\Omega$, $C=0.08$ F, $q(0)=0$, $E(t)=4\,\mathcal U(t-3)$. Kirchhoff: $2.5q'+12.5q=4\mathcal U(t-3)$, so
$$Q(s)=\frac{1.6\,e^{-3s}}{s(s+5)},\qquad \frac{1.6}{s(s+5)}=1.6\left(\frac{1/5}{s}-\frac{1/5}{s+5}\right),$$
$$q(t)=0.32\left(1-e^{-5(t-3)}\right)\mathcal U(t-3),\qquad i(t)=q'(t)=1.6\,e^{-5(t-3)}\,\mathcal U(t-3).$$

## See also
[[Transfer Function]], [[Unit Step and Dirac Delta Functions]], [[Convolution Theorem (Laplace)]], [[Initial and Final Value Theorems]], [[Mechanical and Electrical System Models]]
