---
title: "Second-Order System Response"
domain: "Optimization & Control"
course: "Non-linear Optimization"
unit: "Transient Response and Stability"
level: BSc
status: drafted
confidence: 0
tags: [control-theory, transient-response, ma2008b]
---
<!-- Course slides only link external videos for this topic (syllabus 3.3); content below is canonical (Ogata ch. 5). -->
## Definition
The **standard second-order system** is
$$G(s)=\frac{\omega_n^2}{s^2+2\zeta\omega_n s+\omega_n^2},$$
with **undamped natural frequency** $\omega_n>0$ and **damping ratio** $\zeta\ge0$. A [[Mechanical and Electrical System Models|mass–spring–damper]] $1/(ms^2+bs+k)$ has this form (up to the gain $1/k$) with $\omega_n=\sqrt{k/m}$ and $\zeta=\dfrac{b}{2\sqrt{km}}$; a series RLC has $\omega_n=1/\sqrt{LC}$, $\zeta=\frac R2\sqrt{C/L}$.

The poles are $s=-\zeta\omega_n\pm\omega_n\sqrt{\zeta^2-1}$:
- $0<\zeta<1$ **underdamped**: $s=-\zeta\omega_n\pm j\omega_d$, **damped frequency** $\omega_d=\omega_n\sqrt{1-\zeta^2}$;
- $\zeta=1$ **critically damped**: double real pole $-\omega_n$;
- $\zeta>1$ **overdamped**: two distinct negative real poles;
- $\zeta=0$ **undamped**: poles $\pm j\omega_n$ (sustained oscillation, marginally stable).

## Properties
### Underdamped step response
With $R(s)=1/s$,
$$C(s)=\frac{\omega_n^2}{s(s^2+2\zeta\omega_ns+\omega_n^2)}=\frac1s-\frac{s+2\zeta\omega_n}{(s+\zeta\omega_n)^2+\omega_d^2}=\frac1s-\frac{s+\zeta\omega_n}{(s+\zeta\omega_n)^2+\omega_d^2}-\frac{\zeta\omega_n}{(s+\zeta\omega_n)^2+\omega_d^2}.$$
Using the first translation theorem of the [[Laplace Transform]]:
$$c(t)=1-e^{-\zeta\omega_nt}\left(\cos\omega_dt+\frac{\zeta}{\sqrt{1-\zeta^2}}\sin\omega_dt\right)=1-\frac{e^{-\zeta\omega_nt}}{\sqrt{1-\zeta^2}}\sin\!\left(\omega_dt+\theta\right),$$
where $\theta=\arccos\zeta$ (combine $\cos$ and $\sin$ with amplitude $\sqrt{1+\zeta^2/(1-\zeta^2)}=1/\sqrt{1-\zeta^2}$).

### Transient specifications
- **Peak time.** $\dot c(t)=\dfrac{\omega_n}{\sqrt{1-\zeta^2}}e^{-\zeta\omega_nt}\sin\omega_dt=0$ first at $\omega_dt=\pi$: $\;t_p=\dfrac{\pi}{\omega_d}$.
- **Maximum overshoot.** $c(t_p)-1=-\dfrac{e^{-\zeta\omega_n\pi/\omega_d}}{\sqrt{1-\zeta^2}}\sin(\pi+\theta)=e^{-\zeta\pi/\sqrt{1-\zeta^2}}$ (since $\sin(\pi+\theta)=-\sin\theta=-\sqrt{1-\zeta^2}$):
$$M_p=e^{-\zeta\pi/\sqrt{1-\zeta^2}}.$$
- **Rise time** (0 → 100 %): $c(t_r)=1\Rightarrow\sin(\omega_dt_r+\theta)=0\Rightarrow t_r=\dfrac{\pi-\theta}{\omega_d}$.
- **Settling time.** The envelope is $1\pm e^{-\zeta\omega_nt}/\sqrt{1-\zeta^2}$; using $e^{-\zeta\omega_n t}$ ≈ tolerance: $t_s\approx\dfrac{4}{\zeta\omega_n}$ (2 %), $\dfrac{3}{\zeta\omega_n}$ (5 %). The quantity $\sigma=\zeta\omega_n$ is the distance of the poles from the imaginary axis.

### Frequency-domain link
At $\omega=\omega_n$: $G(j\omega_n)=\dfrac{\omega_n^2}{-\omega_n^2+j2\zeta\omega_n^2+\omega_n^2}=\dfrac{1}{j2\zeta}$, so $|G(j\omega_n)|=\dfrac{1}{2\zeta}$ and the phase is $-90°$ (Tarea 2, M5). See [[Frequency Response]], [[Bode Diagram]].

### Higher-order systems
A higher-order response is a sum of first- and second-order terms; poles much closer to the imaginary axis than the rest (**dominant poles**) govern the transient.

## Examples
$4\ddot x+2\dot x+3x=f$ (Simulink activity): $\omega_n=\sqrt{3/4}\approx0.866$ rad/s, $\zeta=\dfrac{2}{2\sqrt{12}}\approx0.289$ → underdamped, $M_p=e^{-0.289\pi/0.957}\approx38.7\,\%$, $t_s\approx\dfrac{4}{0.25}=16$ s — consistent with the oscillatory scope trace that settles around $t\approx15$–$20$ s at $1/k=1/3$.

## See also
[[First-Order System Response]], [[BIBO Stability and Pole Location]], [[Root Locus]], [[Frequency Response]], [[PID Controller]]
