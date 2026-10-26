---
title: "Gain and Phase Margins"
domain: "Optimization & Control"
course: "Non-linear Optimization"
unit: "Frequency Response"
level: BSc
status: drafted
confidence: 0
tags: [control-theory, frequency-response, stability, ma2008b, exam]
---
## Definition
For an open loop $G(s)H(s)$ whose closed loop is stable and with $P=0$ (see [[Nyquist Stability Criterion]]), **relative stability** measures how far the plot of $GH(j\omega)$ stays from the critical point $-1$.

- **Phase-crossover frequency** $\omega_{pc}$: $\angle GH(j\omega_{pc})=-180°$.
  **Gain margin:** $\displaystyle K_g=\frac{1}{|GH(j\omega_{pc})|}$, or in dB, $K_g\,[\text{dB}]=-20\log_{10}|GH(j\omega_{pc})|$. It is the factor by which the gain can be increased before the closed loop becomes unstable.
- **Gain-crossover frequency** $\omega_{gc}$: $|GH(j\omega_{gc})|=1$ ($0$ dB).
  **Phase margin:** $\gamma=180°+\angle GH(j\omega_{gc})$ — the extra phase lag that would bring the system to the verge of instability.

For a minimum-phase system, stability ⇔ $K_g>1$ ($>0$ dB) **and** $\gamma>0$. Rules of thumb for good performance: $\gamma$ between $30°$ and $60°$, $K_g>6$ dB.

## Properties
### Why they measure distance to instability
If the gain is multiplied by $K_g$, the point $GH(j\omega_{pc})$ moves onto $-1$ exactly (Nyquist). If an extra pure phase lag $\gamma$ is added, $GH(j\omega_{gc})$ (which has modulus $1$) is rotated onto $-1$. Either change puts a closed-loop pole on the imaginary axis.

### Reading them on the three plots
- [[Bode Diagram]]: $K_g$ = distance below $0$ dB of the magnitude at $\omega_{pc}$; $\gamma$ = distance above $-180°$ of the phase at $\omega_{gc}$.
- Polar/Nyquist: $1/K_g$ = where the plot crosses the negative real axis; $\gamma$ = angle between the negative real axis and the point where the plot crosses the unit circle.
- [[Nichols Chart]]: vertical and horizontal distances from the critical point $(-180°,0\text{ dB})$.

### Caution: several crossovers
If $|GH|$ crosses $0$ dB more than once (e.g. resonant open-loop poles), the phase margin is the **smallest** over all gain crossovers; a single-crossover formula can be misleading (see the $k$ example below). Conditionally stable systems can have several phase crossovers too.

## Examples
**Nichols sheet #3.** $G=\dfrac{10}{s(s+1)(s+2)}$. Phase crossover: $-90°-\arctan\omega-\arctan\frac\omega2=-180°\iff\arctan\omega+\arctan\frac\omega2=90°\iff\omega\cdot\frac\omega2=1\iff\omega_{pc}=\sqrt2$. There, $|G|=\dfrac{10}{\sqrt2\cdot\sqrt3\cdot\sqrt6}=\dfrac{10}{6}$, so $K_g=0.6=-4.44$ dB. $\omega_{gc}\approx1.80$, $\gamma\approx-13.0°$. **Unstable** (confirm with Routh: $s^3+3s^2+2s+10$, $3\cdot2<10$).

**Nichols sheet #2.** $G=\dfrac{15}{s^2+8s+15}$, $H=\dfrac1s$: $GH=\dfrac{15}{s(s+3)(s+5)}$. $\arctan\frac\omega3+\arctan\frac\omega5=90°\iff\omega^2=15$; $|GH(j\sqrt{15})|=\dfrac{15}{\sqrt{15}\sqrt{24}\sqrt{40}}=\dfrac18$ ⇒ $K_g=8=18.06$ dB. $\omega_{gc}\approx0.938$, $\gamma\approx62.0°$.

**Nichols sheet #4.** $G=\dfrac{20}{(s+2)(s+5)}$, $H=\dfrac2s$: $GH=\dfrac{40}{s(s+2)(s+5)}$. $\omega_{pc}=\sqrt{10}$, $|GH|=\dfrac{40}{\sqrt{10}\sqrt{14}\sqrt{35}}=\dfrac{40}{70}$ ⇒ $K_g=1.75=4.86$ dB; $\omega_{gc}\approx2.35$, $\gamma\approx15.3°$ (stable, poorly damped).

**Nichols sheet #1.** $G=\dfrac{3}{(s+3)(s+4)}$: $|G|\le\frac{3}{12}<1$ and the phase never reaches $-180°$, so both margins are infinite.

**Tarea 2 #7.** $G=\dfrac{20(s+1)}{s(s^2+2s+10)(s+5)}$: $K_g\approx3.14$ ($9.93$ dB) at $\omega_{pc}\approx4.01$; $\gamma\approx103.7°$ at $\omega_{gc}\approx0.443$ (computed with `python-control`, `margin(G)`).

**Tarea 2 #5 — choose $k$ for $\gamma=50°$.** $G=\dfrac{k}{s(s^2+s+4)}$, $\angle G(j\omega)=-90°-\angle(4-\omega^2+j\omega)$.
Set $\angle G(j\omega_{gc})=-130°$: $\tan40°=\dfrac{\omega}{4-\omega^2}\Rightarrow0.8391\omega^2+\omega-3.3564=0\Rightarrow\omega_{gc}=1.491$ rad/s. Then $|G(j\omega_{gc})|=1$ gives
$$k=\omega_{gc}\sqrt{(4-\omega_{gc}^2)^2+\omega_{gc}^2}=1.491\times2.320\approx3.46.$$
**Rigor check.** The open-loop poles $-0.5\pm1.94j$ are lightly damped ($\zeta=0.25$), so $|G|$ has a resonant bump near $\omega=1.63$. For $3.443<k<3.464$ the magnitude crosses $0$ dB **three times**; with $k=3.46$ the other crossings (up to $\omega\approx1.72$) have phase margin as low as $\approx31°$, and $K_g\approx1.16$ (1.3 dB). So $k\approx3.46$ satisfies the textbook procedure at the first crossover, but the true (minimum) phase margin is about $31°$, not $50°$. For $k<3.443$ there is a single crossover, but there $\gamma>61°$ — the phase margin jumps and never equals exactly $50°$. Worth raising with the professor.

## See also
[[Nyquist Stability Criterion]], [[Bode Diagram]], [[Nichols Chart]], [[Frequency Response]], [[Routh-Hurwitz Criterion]]
