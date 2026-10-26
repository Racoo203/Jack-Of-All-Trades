---
title: "Unit Step and Dirac Delta Functions"
domain: "Optimization & Control"
course: "Non-linear Optimization"
unit: "Control Theory Foundations"
level: BSc
status: drafted
confidence: 0
tags: [control-theory, differential-equations, ma2008b]
---
## Definition
**Unit step (Heaviside).** For $a\ge0$,
$$\mathcal U(t-a)=\mathcal U_a(t)=\begin{cases}0,&0\le t<a\\1,&t\ge a\end{cases}$$
It models systems that are switched on at $t=a$.

**Impulse and Dirac delta.** For small $\varepsilon>0$ define the rectangular pulse of unit area
$$\delta_\varepsilon(t-t_0)=\begin{cases}\frac{1}{2\varepsilon},&t_0-\varepsilon<t<t_0+\varepsilon\\0,&\text{otherwise}\end{cases}$$
and $\delta(t-t_0)=\lim_{\varepsilon\to0}\delta_\varepsilon(t-t_0)$. Formally $\delta(t-t_0)=\infty$ at $t_0$, $0$ elsewhere, and $\int_0^\infty\delta(t-t_0)\,dt=1$. It is a [[Distribution (Generalized Function)|generalized function]], not an ordinary one; it models a very large force acting over a very short time (a hammer blow).

## Properties
### Transform of the step
$$\mathcal L\{\mathcal U(t-a)\}=\int_a^\infty e^{-st}dt=\frac{e^{-as}}{s}.$$

### Writing piecewise functions with steps
A function equal to $g(t)$ on $[0,a)$ and $h(t)$ on $[a,\infty)$ is
$$f(t)=g(t)+[h(t)-g(t)]\,\mathcal U(t-a),$$
since the bracket switches on exactly at $a$. With three pieces ($g$ on $[0,a)$, $h$ on $[a,b)$, $i$ on $[b,\infty)$):
$$f(t)=g(t)+[h(t)-g(t)]\mathcal U(t-a)+[i(t)-h(t)]\mathcal U(t-b).$$
Non-constant pieces are then transformed with the second translation theorem of the [[Laplace Transform]], $\mathcal L\{f(t)\mathcal U(t-a)\}=e^{-as}\mathcal L\{f(t+a)\}$.

### Transform of the delta
$$\mathcal L\{\delta_\varepsilon(t-t_0)\}=\frac{1}{2\varepsilon}\int_{t_0-\varepsilon}^{t_0+\varepsilon}e^{-st}dt=e^{-st_0}\,\frac{e^{s\varepsilon}-e^{-s\varepsilon}}{2s\varepsilon}=e^{-st_0}\frac{\sinh(s\varepsilon)}{s\varepsilon}.$$
Since $\sinh(x)/x\to1$ as $x\to0$ (L'Hôpital),
$$\mathcal L\{\delta(t-t_0)\}=e^{-st_0},\qquad \mathcal L\{\delta(t)\}=1.$$
Consequently, with input $\delta(t)$ and zero initial conditions, $Y(s)=G(s)$: the **impulse response** is $\mathcal L^{-1}\{G(s)\}$ (see [[Transfer Function]]).

### Sifting property
For $f$ continuous at $t_0$: $\int_0^\infty f(t)\delta(t-t_0)\,dt=f(t_0)$.

## Examples
**Piecewise constant.** $f=-2$ on $[0,1)$, $3$ on $[1,2)$, $1$ on $[2,\infty)$:
$f=-2+5\,\mathcal U(t-1)-2\,\mathcal U(t-2)$, so $F(s)=-\frac2s+\frac5se^{-s}-\frac2se^{-2s}$.

**Struck spring (slides).** $y''+y=4\delta(t-2\pi)$, $y(0)=1$, $y'(0)=0$:
$$(s^2+1)Y=s+4e^{-2\pi s}\Rightarrow y(t)=\cos t+4\sin(t-2\pi)\,\mathcal U(t-2\pi)=\cos t+4\sin t\;\mathcal U(t-2\pi).$$
The mass oscillates with amplitude 1 until $t=2\pi$, then with amplitude $\sqrt{17}$.

## See also
[[Laplace Transform]], [[Transfer Function]], [[First-Order System Response]]
