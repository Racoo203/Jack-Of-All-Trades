---
title: "Nichols Chart"
domain: "Optimization & Control"
course: "Non-linear Optimization"
unit: "Frequency Response"
level: BSc
status: drafted
confidence: 0
tags: [control-theory, frequency-response, ma2008b]
---
## Definition
The **Nichols plot** (log-magnitude vs phase plot) of an open loop $G(j\omega)$ draws $20\log_{10}|G(j\omega)|$ on the vertical axis against $\angle G(j\omega)$ (degrees) on the horizontal axis, with $\omega$ as the curve parameter. It merges the two curves of the [[Bode Diagram]] into one.

The **Nichols chart** overlays, on this plane, the contours of constant **closed-loop** magnitude $M$ (dB) and phase $\alpha$ for unity feedback, where
$$T(j\omega)=\frac{G(j\omega)}{1+G(j\omega)}=Me^{j\alpha}.$$
This is the "closed-loop frequency response I" topic of Module 5.

## Properties
### Critical point and margins
$G=-1$ corresponds to $(\,-180°,\ 0\text{ dB}\,)$. For a minimum-phase open loop:
- **Gain margin** = how far below $0$ dB the curve is when it crosses the $-180°$ line;
- **Phase margin** = how far to the right of $-180°$ the curve is when it crosses $0$ dB.
(See [[Gain and Phase Margins]].) Stability requires the curve to pass **to the right of / below** the critical point as $\omega$ increases.

### Why constant-$M$ contours exist
Write $G=|G|e^{j\phi}$. Then
$$M^2=\frac{|G|^2}{1+2|G|\cos\phi+|G|^2},$$
which depends only on $(|G|,\phi)$ — the two Nichols coordinates. Solving for each fixed $M$ gives a closed curve around the critical point; the curve tangent to the open-loop plot gives the **resonant peak** $M_r$ of the closed loop, and the point where the plot crosses the $M=-3$ dB contour gives the closed-loop **bandwidth**.

### Effect of a gain change
Multiplying $G$ by $K$ shifts the whole plot **vertically** by $20\log K$ dB without changing its shape — which makes gain design (e.g. for a desired $M_r$ or margin) a matter of sliding the curve.

### MATLAB
`nichols(G); ngrid` draws the plot with the $M,\alpha$ grid; `margin(G)` returns the margins.

## Examples
See the worked margins for the four Nichols sheet systems in [[Gain and Phase Margins]]: $\frac{3}{(s+3)(s+4)}$ (never reaches $0$ dB: infinite margins); $\frac{15}{s(s+3)(s+5)}$ ($K_g=18.1$ dB, $\gamma=62°$); $\frac{10}{s(s+1)(s+2)}$ (curve passes above the critical point: $K_g=-4.4$ dB, unstable); $\frac{40}{s(s+2)(s+5)}$ ($K_g=4.9$ dB, $\gamma=15°$).

## See also
[[Bode Diagram]], [[Gain and Phase Margins]], [[Nyquist Stability Criterion]], [[Frequency Response]]
