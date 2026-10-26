---
title: "Mechanical and Electrical System Models"
domain: "Optimization & Control"
course: "Non-linear Optimization"
unit: "Control Theory Foundations"
level: BSc
status: drafted
confidence: 0
tags: [control-theory, modeling, ma2008b]
---
## Definition
**Modeling** a control system means going from a schematic to a mathematical model (ODEs from physical laws), then to a functional/block diagram, reducing it, and obtaining the system response (course slides, "Modelado en teoría de control"). The laws used are Newton's second law for mechanical systems and Kirchhoff's voltage law (with element laws) for circuits. Each model is then turned into a [[Transfer Function]] via the [[Laplace Transform]] with zero initial conditions, or into a [[State-Space Representation]].

## Properties
### Translational mass–spring–damper (MRA)
Mass $m$, viscous friction $b$, spring $k$, applied force $f(t)$, displacement $x(t)$. Newton: $m\ddot x=f-b\dot x-kx$, i.e.
$$m\ddot x+b\dot x+kx=f,\qquad x(0)=\dot x(0)=0.$$
Laplace: $(ms^2+bs+k)X(s)=F(s)$, so
$$G(s)=\frac{X(s)}{F(s)}=\frac{1}{ms^2+bs+k}.$$
For simulation (Simulink), solve for the highest derivative, $\ddot x=\frac1m(f-b\dot x-kx)$, and chain two integrators with gain feedbacks $b$ and $k$ — e.g. $4\ddot x+2\dot x+3x=f$ gives $\ddot x=\tfrac14(f-2\dot x-3x)$.

### Spring–damper on a moving cart (base excitation)
Input: cart displacement $u(t)$; output: mass displacement $y(t)$. Damper force $\propto \dot y-\dot u$, spring force $\propto y-u$:
$$m\ddot y=-b(\dot y-\dot u)-k(y-u)\;\Longrightarrow\;m\ddot y+b\dot y+ky=b\dot u+ku.$$
Zero ICs:
$$G(s)=\frac{Y(s)}{U(s)}=\frac{bs+k}{ms^2+bs+k}.$$
The input derivative on the right is why its state-space form needs the "derivative input" construction (see [[State-Space Representation]]).

### Rotational system
Satellite attitude with torque $T$ and inertia $J$, no friction: $J\ddot\theta=T$ ⇒ $\Theta(s)/T(s)=1/(Js^2)$.

### Element laws and impedances
| Element | $v$–$i$ | $i$–$v$ | $v$–$q$ | Impedance $Z(s)=V/I$ |
|---|---|---|---|---|
| Resistor | $v=Ri$ | $i=v/R$ | $v=R\dot q$ | $R$ |
| Inductor | $v=L\,di/dt$ | $i=\frac1L\int v$ | $v=L\ddot q$ | $Ls$ |
| Capacitor | $v=\frac1C\int i$ | $i=C\,dv/dt$ | $v=q/C$ | $\dfrac{1}{Cs}$ |

Impedances in series add, exactly like resistors, which avoids writing the ODE first ("modelado en frecuencia").

### Series RLC, capacitor voltage as output
KVL: $L\frac{di}{dt}+Ri+\frac1C\int_0^t i\,d\tau=v_i(t)$. Three equivalent ODEs exist (in $i$, in $q$ with $\dot q=i$, and in $v_C$). Using $v_C=\frac1C\int i$, so $i=C\dot v_C$ and $\frac{di}{dt}=C\ddot v_C$:
$$LC\,\ddot v_C+RC\,\dot v_C+v_C=v_i.$$
Laplace with zero ICs:
$$\frac{V_C(s)}{V_i(s)}=\frac{1}{LCs^2+RCs+1}.$$
Same result by impedances: $I(s)=\dfrac{V_i(s)}{R+Ls+\frac{1}{Cs}}$ and $V_C=\dfrac{I}{Cs}$, so $\dfrac{V_C}{V_i}=\dfrac{1/(Cs)}{R+Ls+1/(Cs)}=\dfrac{1}{LCs^2+RCs+1}$.

### Cascaded RC circuits and loading
For two RC sections $R_1C_1$ then $R_2C_2$ (mesh equations $R_1i_1+\frac1{C_1}\int(i_1-i_2)=e_i$, $R_2i_2+\frac1{C_2}\int i_2+\frac1{C_1}\int(i_2-i_1)=0$, $e_o=\frac1{C_2}\int i_2$), Ogata's result is
$$\frac{E_o(s)}{E_i(s)}=\frac{1}{R_1C_1R_2C_2s^2+(R_1C_1+R_2C_2+R_1C_2)s+1}.$$
The cross term $R_1C_2$ is the **loading effect**: the result is *not* the product $\frac{1}{(R_1C_1s+1)(R_2C_2s+1)}$. Only when the sections are isolated by an amplifier (negligible loading) does the overall transfer function equal the product of the individual ones.

## Examples
**Step response of an RLC (slides).** $L=15$, $C=1$, $R=8$: $\dfrac{V_C}{U}=\dfrac{1}{15s^2+8s+1}=\dfrac{1}{(3s+1)(5s+1)}$. With $U=1/s$:
$$V_C(s)=\frac{1}{15\,s\,(s+\frac13)(s+\frac15)}=\frac1s+\frac{3/2}{s+\frac13}-\frac{5/2}{s+\frac15},$$
$$v_C(t)=1+\tfrac32e^{-t/3}-\tfrac52e^{-t/5}\quad(v_C(0)=0\ \checkmark,\ v_C(\infty)=1).$$

**Ladder circuit (Actividad 4, two methods).** Source $e_i$ – $R$ – node $a$ (inductor $L$ to ground) – $R$ – node $b$ (capacitor $C$ to ground), $e_o=v_b$, with $R=L=C=1$. Node equations: $E_i-V_a=\frac{V_a}{s}+(V_a-V_b)$ and $V_a-V_b=sV_b$, so $V_a=(1+s)V_b$ and
$$E_i=V_b\left[(1+s)\left(2+\tfrac1s\right)-1\right]=V_b\,\frac{2s^2+2s+1}{s}\;\Longrightarrow\;\frac{E_o}{E_i}=\frac{s}{2s^2+2s+1},$$
which matches both the mesh-equation and the state-space ($C(sI-A)^{-1}B$) answers in the submission.

## See also
[[Transfer Function]], [[State-Space Representation]], [[Block Diagram Reduction]], [[Laplace Transform]], [[Second-Order System Response]]
