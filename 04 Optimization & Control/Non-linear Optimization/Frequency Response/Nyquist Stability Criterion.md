---
title: "Nyquist Stability Criterion"
domain: "Optimization & Control"
course: "Non-linear Optimization"
unit: "Frequency Response"
level: BSc
status: drafted
confidence: 0
tags: [control-theory, frequency-response, stability, ma2008b, exam]
---
## Definition
A **polar plot** is the curve traced by $G(j\omega)$ in the complex plane as $\omega$ goes from $0$ to $\infty$. The **Nyquist plot** extends it to the whole **Nyquist contour** $\Gamma$: the imaginary axis from $-j\infty$ to $+j\infty$ closed by a semicircle of infinite radius enclosing the RHP, with small semicircular **indentations** around open-loop poles on the imaginary axis. Since $G(-j\omega)=\overline{G(j\omega)}$, the negative-frequency part is the mirror image of the polar plot.

**Nyquist stability criterion (Nyquist, 1932).** For the loop $1+G(s)H(s)$, let
- $P$ = number of open-loop poles of $GH$ in the RHP,
- $N$ = number of **clockwise** encirclements of the point $-1+j0$ by the Nyquist plot of $GH$,
- $Z$ = number of closed-loop poles (zeros of $1+GH$) in the RHP.
Then
$$\boxed{Z=N+P},$$
and the closed loop is stable iff $Z=0$, i.e. iff the plot encircles $-1$ **counterclockwise $P$ times** ($N=-P$). If $P=0$: stable iff $-1$ is not encircled.

## Properties
### Derivation from the argument principle
[[Argument Principle|Cauchy's argument principle]]: if $F$ is analytic on and inside a clockwise closed contour except for poles, then the image $F(\Gamma)$ encircles the origin clockwise $Z_F-P_F$ times, where $Z_F,P_F$ count zeros and poles inside. Take $F(s)=1+G(s)H(s)$ and $\Gamma$ the Nyquist contour (clockwise around the RHP):
- the poles of $F$ are the poles of $GH$ ⇒ $P_F=P$;
- the zeros of $F$ are the closed-loop poles ⇒ $Z_F=Z$;
- encircling the origin by $1+GH$ is the same as encircling $-1$ by $GH$ ⇒ $N=Z-P$. ∎
Because the check uses only the open-loop frequency response, the criterion works with measured data and with time delays, where Routh does not apply.

### Practical reading
Count encirclements by drawing a ray from $-1$ and counting signed crossings; the infinite semicircle maps to a point (usually $0$) when $GH$ is strictly proper; a pole of order $q$ at the origin maps the small indentation to $q$ half-circles of infinite radius swept clockwise.

## Examples
**Nyquist sheet #2.** $G=\dfrac{k(1-s)}{s+1}$, unity feedback, $k>0$. $|G(j\omega)|=k$ for all $\omega$ (all-pass) and the phase runs $0°\to-180°$: the plot is the circle $|G|=k$, from $k$ at $\omega=0$ to $-k$ at $\omega\to\infty$. $P=0$. It encircles $-1$ iff $k>1$. So the closed loop is **stable for $0<k<1$** — check: $1+G=0\iff(1-k)s+(1+k)=0$, whose root $-\frac{1+k}{1-k}$ is negative iff $k<1$.

**Nyquist sheet #3 (time delay).** $G(s)H(s)=\dfrac{Ke^{-2s}}{s}$. $|GH(j\omega)|=K/\omega$, $\angle GH=-90°-2\omega$ (rad → $-\frac\pi2-2\omega$). The plot first crosses the negative real axis when $-\frac\pi2-2\omega=-\pi$, i.e. $\omega=\frac\pi4$, at magnitude $\frac{K}{\pi/4}$. Stability requires this crossing to lie to the right of $-1$: $\frac{4K}{\pi}<1$, so
$$K_{\max}=\frac\pi4\approx0.785.$$

**Tarea 2 #4.** $G=\dfrac{1}{s(s-1)}$: $P=1$ (pole at $+1$), plus a pole at the origin (indent). The resulting plot encircles $-1$ once clockwise, $N=1$, so $Z=2$: **unstable** — confirmed by $1+G=0\iff s^2-s+1=0$, roots $0.5\pm0.866j$.

**Tarea 2 #3.** $G=\dfrac{20}{s^3+0.2s^2+s+1}$: $P=2$ (poles $0.262\pm1.145j$). Closed loop $s^3+0.2s^2+s+21$ has two RHP roots ($1.25\pm2.49j$), so $Z=2$ and the plot must show $N=0$ net encirclements — **unstable**.

**Nyquist sheet #5.** $G=\dfrac{s^2+2s+1}{s^3+0.2s^2+s+1}$: $P=2$. Closed loop $s^3+1.2s^2+3s+2$ has all roots in the LHP ($-0.751$, $-0.224\pm1.616j$), so $Z=0$ and the plot must encircle $-1$ **twice counterclockwise** ($N=-2$): **stable** even though the open loop is unstable.

**Nyquist sheet #4.** $G=\dfrac{1}{s^3+0.2s^2+1}$: $P=2$; closed loop $s^3+0.2s^2+2$ has roots $0.565\pm1.088j$ → $Z=2$, unstable.

**Nyquist sheet #1.** $G=\dfrac{1}{s(s^2+0.8s+1)}$: $P=0$ with a pole at the origin. The plot crosses the negative real axis at $\omega=1$ with $|G|=\frac{1}{0.8}=1.25>1$, so $-1$ is encircled (twice clockwise) and the unity-feedback loop is unstable (GM $=0.8$; closed-loop roots $0.055\pm1.047j$).

## See also
[[Frequency Response]], [[Gain and Phase Margins]], [[Bode Diagram]], [[Nichols Chart]], [[BIBO Stability and Pole Location]], [[Routh-Hurwitz Criterion]]
