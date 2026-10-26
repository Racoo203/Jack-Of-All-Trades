---
title: "Bode Diagram"
domain: "Optimization & Control"
course: "Non-linear Optimization"
unit: "Frequency Response"
level: BSc
status: drafted
confidence: 0
tags: [control-theory, frequency-response, ma2008b]
---
## Definition
The **Bode diagram** of $G(s)$ consists of two plots against $\log_{10}\omega$:
- the **log-magnitude** $\;|G(j\omega)|_{\text{dB}}=20\log_{10}|G(j\omega)|$,
- the **phase** $\;\angle G(j\omega)$ in degrees.
It is the standard graphical form of the [[Frequency Response]].

## Properties
### Why logarithms: products become sums
For $G=G_1G_2\cdots G_k$, $20\log|G|=\sum20\log|G_i|$ and $\angle G=\sum\angle G_i$, so the diagram is the **sum of the diagrams of the basic factors**, each approximated by straight-line asymptotes. A decade is a factor of 10 in $\omega$.

### Basic factors
1. **Gain $K$:** $20\log K$ dB, phase $0°$ ($K>0$).
2. **Integrator $1/(j\omega)^p$:** $-20p\log\omega$ — a line of slope $-20p$ dB/decade through $0$ dB at $\omega=1$; phase $-90°p$. (A differentiator $(j\omega)^p$ gives $+20p$ dB/dec and $+90°p$.)
3. **First-order factor $1/(1+j\omega T)$:** $-20\log\sqrt{1+\omega^2T^2}$.
   - $\omega\ll1/T$: $\approx0$ dB; $\omega\gg1/T$: $\approx-20\log(\omega T)$, slope $-20$ dB/dec.
   - Asymptotes meet at the **corner frequency** $\omega=1/T$, where the exact error is $-20\log\sqrt2=-3.01$ dB.
   - Phase $-\arctan\omega T$: $0°\to-45°$ (at $1/T$) $\to-90°$.
   A zero $(1+j\omega T)$ mirrors this: $+20$ dB/dec and $0\to+90°$.
4. **Quadratic factor** $\left[1+2\zeta\left(\frac{j\omega}{\omega_n}\right)+\left(\frac{j\omega}{\omega_n}\right)^2\right]^{-1}$: $0$ dB below $\omega_n$, $-40$ dB/dec above; the exact curve has a **resonant peak** near $\omega_n$ when $\zeta<0.707$: $M_r=\dfrac{1}{2\zeta\sqrt{1-\zeta^2}}$ at $\omega_r=\omega_n\sqrt{1-2\zeta^2}$; at $\omega_n$ itself $|G|=\frac1{2\zeta}$. Phase $0\to-90°$ (at $\omega_n$) $\to-180°$.

*Derivation of $M_r$:* $|G|^{-2}=(1-u^2)^2+(2\zeta u)^2$ with $u=\omega/\omega_n$; $\frac{d}{du}=0\Rightarrow-4u(1-u^2)+8\zeta^2u=0\Rightarrow u^2=1-2\zeta^2$; substituting, $|G|^{-2}=4\zeta^4+4\zeta^2(1-2\zeta^2)=4\zeta^2(1-\zeta^2)$.

### Procedure (by hand)
Write $G$ in time-constant form ($K\prod(1+j\omega T_j)/[(j\omega)^p\prod(1+j\omega T_i)\cdots]$), mark the corner frequencies, start at low frequency with the $K/(j\omega)^p$ line, change the slope by $\pm20$ (or $\pm40$) dB/dec at each corner, then correct near the corners; add the phases.

### Unusual phase with RHP poles
For open-loop poles in the RHP the phase does not follow the minimum-phase pattern — each RHP pole's angle evolves differently as $\omega$ grows. MATLAB: `bode(tf(num,den))`; `margin(G)` also gives [[Gain and Phase Margins]].

## Examples
**Activity problem 2.** $G(s)=\dfrac{10(s^2+0.4s+1)}{s(s^2+0.8s+9)}$. Time-constant form: $G=\dfrac{10}{9}\cdot\dfrac{(j\omega)^2+0.4j\omega+1}{j\omega\left[\frac{(j\omega)^2}{9}+\frac{0.8}{9}j\omega+1\right]}$.
- Low frequency: $\frac{10/9}{j\omega}$ → $-20$ dB/dec, $+0.92$ dB at $\omega=1$, phase $-90°$.
- Quadratic zero at $\omega_n=1$ with $\zeta=0.2$: slope $+40$ → net $+20$ dB/dec above 1, with a sharp **notch** at $\omega=1$ ($|{\cdot}|=2\zeta=0.4$, i.e. $-8$ dB) and phase jumping up toward $+90°$.
- Quadratic pole at $\omega_n=3$ with $\zeta=\frac{0.8}{6}=0.133$: slope $-40$ → net $-20$ dB/dec above 3, with a resonant **peak** $\approx\frac{1}{2(0.133)}=3.75$ (+11.5 dB) near $\omega=3$, phase dropping back to $-90°$.
- High frequency: $G\approx\frac{10}{s}$, $-20$ dB/dec, $-90°$.

**Activity problem 3 / Tarea 2 #6.** $G=\dfrac{s+0.5}{s^3+s^2+1}$, open-loop poles $-1.4656$ and $0.2328\pm0.7926j$ (non-minimum phase). Why does the phase start at $0°$ and tend to $+180°$? Track each factor's angle continuously as $\omega:0\to\infty$:
- zero $-0.5$: $0°\to+90°$;
- LHP pole $-1.4656$: contributes $0°\to-90°$;
- RHP pair: $\angle(j\omega-p)$ with $p=0.2328+0.7926j$ goes from $-106.4°$ through $-180°$ to $-270°$ (change $-163.6°$), and for $\bar p$ from $+106.4°$ to $+90°$ (change $-16.4°$). The pair's angle sum changes by $-180°$, so it contributes $+180°$ to $\angle G$.
- $G(0)=0.5>0$ ⇒ start at $0°$. Total change: $+90°-90°+180°=+180°$. ∎
Closing the loop with unity feedback, $s^3+s^2+s+1.5$ has roots $0.102\pm1.111j$: the closed loop is **unstable** (check with the [[Nyquist Stability Criterion]]).

## See also
[[Frequency Response]], [[Gain and Phase Margins]], [[Nyquist Stability Criterion]], [[Nichols Chart]], [[Second-Order System Response]]
