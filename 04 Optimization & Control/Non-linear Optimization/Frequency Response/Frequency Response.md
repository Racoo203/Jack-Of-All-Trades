---
title: "Frequency Response"
domain: "Optimization & Control"
course: "Non-linear Optimization"
unit: "Frequency Response"
level: BSc
status: drafted
confidence: 0
tags: [control-theory, frequency-response, ma2008b]
---
<!-- Module 5 has only problem sheets in Resources (no lecture slides); definitions are canonical (Ogata ch. 7). -->
## Definition
The **frequency response** of a stable [[Linear Time-Invariant System]] with [[Transfer Function]] $G(s)$ is its steady-state response to a sinusoidal input. It is described by the complex function
$$G(j\omega)=|G(j\omega)|\,e^{j\angle G(j\omega)},\qquad \omega\ge0,$$
i.e. $G(s)$ evaluated on the imaginary axis. $|G(j\omega)|$ is the **magnitude** (amplitude ratio) and $\angle G(j\omega)$ the **phase**.

## Properties
### Sinusoidal steady state
Let $x(t)=X\sin\omega t$, $X(s)=\dfrac{X\omega}{s^2+\omega^2}$, and suppose all poles of $G$ are in the open LHP. Then
$$Y(s)=G(s)\frac{X\omega}{(s-j\omega)(s+j\omega)}=\frac{a}{s-j\omega}+\frac{\bar a}{s+j\omega}+(\text{terms from the poles of }G).$$
The last terms decay to zero ([[BIBO Stability and Pole Location|stability]]). By the cover-up rule, $a=G(j\omega)\dfrac{X\omega}{2j\omega}=\dfrac{XG(j\omega)}{2j}$, so in steady state
$$y_{ss}(t)=\frac{X}{2j}\left(G(j\omega)e^{j\omega t}-G(-j\omega)e^{-j\omega t}\right)=X|G(j\omega)|\sin\big(\omega t+\angle G(j\omega)\big),$$
using $G(-j\omega)=\overline{G(j\omega)}$. The output is a sinusoid of the **same frequency**, amplitude scaled by $|G(j\omega)|$ and phase shifted by $\angle G(j\omega)$.

### Magnitude and phase of a factored $G$
For $G(s)=K\dfrac{\prod(s-z_j)}{\prod(s-p_i)}$:
$$|G(j\omega)|=|K|\frac{\prod|j\omega-z_j|}{\prod|j\omega-p_i|},\qquad\angle G(j\omega)=\angle K+\sum\angle(j\omega-z_j)-\sum\angle(j\omega-p_i).$$
*Tarea 2 (M5), 1a:* $G=\dfrac{1}{s(s+2)(s+4)}$:
$$|G(j\omega)|=\frac{1}{\omega\sqrt{\omega^2+4}\sqrt{\omega^2+16}},\qquad \angle G(j\omega)=-90°-\arctan\frac\omega2-\arctan\frac\omega4.$$
*1b:* $G=\dfrac{s+5}{(s+2)(s+4)}$: $|G|=\dfrac{\sqrt{\omega^2+25}}{\sqrt{\omega^2+4}\sqrt{\omega^2+16}}$, $\angle G=\arctan\frac\omega5-\arctan\frac\omega2-\arctan\frac\omega4$.

### Second-order peak at $\omega_n$
For $G=\dfrac{\omega_n^2}{s^2+2\zeta\omega_ns+\omega_n^2}$: $|G(j\omega_n)|=\dfrac{1}{2\zeta}$ (see [[Second-Order System Response]]).

### Minimum vs non-minimum phase
A system is **minimum phase** if it has no poles or zeros in the RHP. For the same magnitude curve, it has the smallest phase range. Example (Bode activity): $G_1=\dfrac{1+s}{1+2s}$ and $G_2=\dfrac{1-s}{1+2s}$ have identical magnitudes ($|1-j\omega|=|1+j\omega|$), but $\angle G_1=\arctan\omega-\arctan2\omega$ returns to $0°$ while $\angle G_2=-\arctan\omega-\arctan2\omega\to-180°$. For minimum-phase systems the magnitude curve determines the phase uniquely (Bode's gain–phase relation); for non-minimum-phase ones it does not.

### Graphical representations
- [[Bode Diagram]]: $20\log_{10}|G|$ and $\angle G$ versus $\log\omega$.
- Polar / [[Nyquist Stability Criterion|Nyquist plot]]: the curve $G(j\omega)$ in the complex plane.
- [[Nichols Chart]]: dB magnitude versus phase.
All three are used to read [[Gain and Phase Margins]].

## See also
[[Bode Diagram]], [[Nyquist Stability Criterion]], [[Nichols Chart]], [[Gain and Phase Margins]], [[Transfer Function]]
