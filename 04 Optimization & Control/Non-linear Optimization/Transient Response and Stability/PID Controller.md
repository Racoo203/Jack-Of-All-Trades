---
title: "PID Controller"
domain: "Optimization & Control"
course: "Non-linear Optimization"
unit: "Transient Response and Stability"
level: BSc
status: drafted
confidence: 0
tags: [control-theory, ma2008b]
---
## Definition
A **controller** modifies the behaviour of a system so that its output reaches the desired value, using a sensor to compare the output with the reference and feeding back the error $e(t)=r(t)-y(t)$ (see [[Control System Fundamentals]]). The controller **gain** is the ratio of output change to input change, $\Delta\text{out}/\Delta\text{in}$.

The classical controllers and their [[Transfer Function|transfer functions]] $G_c(s)=U(s)/E(s)$:
| Controller | Time law | $G_c(s)$ |
|---|---|---|
| P | $u=K_pe$ | $K_p$ |
| I | $u=K_i\int_0^te$ | $\dfrac{K_i}{s}$ |
| PD | $u=K_pe+K_d\dot e$ | $K_p+K_ds$ |
| PI | $u=K_pe+K_i\int e$ | $K_p+\dfrac{K_i}{s}$ |
| PID | $u=K_pe+K_i\int e+K_d\dot e$ | $K_p+\dfrac{K_i}{s}+K_ds=\dfrac{K_ds^2+K_ps+K_i}{s}$ |

(Ogata's equivalent form: $K_p\left(1+\frac{1}{T_is}+T_ds\right)$ with $K_i=K_p/T_i$, $K_d=K_pT_d$. Simulink's PID block uses $P+I\frac1s+D\frac{N}{1+N/s}$, a PID with a filtered derivative.)

## Properties
### Characteristics of each action (slides)
- **Proportional:** brings the output close to the reference, but with a unity-feedback type-0 plant it leaves a steady-state step error $e_{ss}=\frac{1}{1+K_pG(0)}$ — it reduces but does not eliminate the error.
- **Integral:** adds a pole at the origin of the open-loop transfer function, raising the system type by one, so the step error becomes $\lim_{s\to0}\frac{1}{1+G_c(s)G(s)}=0$ (because $G_c\to\infty$). It is destabilizing (adds $-90°$ of phase), so it is combined with proportional action. It is slow.
- **Derivative:** adds a zero at the origin (in $K_ds$) — reacts to the *trend* of the error, a projection of where the process is heading; improves damping and speed. It amplifies noise and cannot act alone (zero output for constant error).

| Controller | Advantages | Disadvantages |
|---|---|---|
| Proportional | approximates the output to the reference | does not react to error variations; does not eliminate the error |
| Derivative | anticipates error variations, fast | amplifies noise; cannot work alone |
| Integral | removes steady-state error | slow |

### Steady-state error with integral action (derivation)
Unity feedback: $E(s)=\dfrac{R(s)}{1+G_c(s)G(s)}$. For a unit step and the [[Initial and Final Value Theorems|final value theorem]] (closed loop assumed stable):
$$e_{ss}=\lim_{s\to0}s\cdot\frac{1/s}{1+G_cG}=\frac{1}{1+\lim_{s\to0}G_c(s)G(s)}.$$
With P control and finite $G(0)$, $e_{ss}=\frac1{1+K_pG(0)}>0$. With PI, $G_c(s)G(s)\sim\frac{K_iG(0)}{s}\to\infty$, so $e_{ss}=0$.

### Choosing gains that keep the loop stable
Close the loop, write the characteristic polynomial in terms of the gains, and apply the [[Routh-Hurwitz Criterion]]; the [[Root Locus]] shows how the poles move with $K_p$.

## Examples
**Slides' comparison.** Plant $G(s)=\dfrac{1}{s^3+9s^2+26s+24}=\dfrac{1}{(s+2)(s+3)(s+4)}$ with <!-- UNVERIFIED: handwritten numerator read as 1; check slide 20 of "Estabilidad segunda parte" -->
- P: $G_c=105$ → $D=s^3+9s^2+26s+129$; Routh: $9\cdot26=234>129$ ✓ stable, oscillatory, with $e_{ss}=\frac{1}{1+105/24}\approx0.186$.
- PI: $G_c=94.5+\frac{92.795}{s}$ → $D=s^4+9s^3+26s^2+118.5s+92.795$; first column $1,\ 9,\ 12.83,\ 53.4,\ 92.8$ → stable, $e_{ss}=0$, stops oscillating sooner.
- PID: $G_c=126+\frac{204.87}{s}+19.278s$ → $D=s^4+9s^3+45.28s^2+150s+204.87$; first column $1,\ 9,\ 28.6,\ 85.5,\ 204.9$ → stable; the slides conclude **PID is best** (settles fastest, zero error).

## See also
[[Control System Fundamentals]], [[Routh-Hurwitz Criterion]], [[Root Locus]], [[Steady-State Error]], [[Frequency Response]]
