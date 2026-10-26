---
title: "State-Space Representation"
domain: "Optimization & Control"
course: "Non-linear Optimization"
unit: "Control Theory Foundations"
level: BSc
status: drafted
confidence: 0
tags: [control-theory, linear-algebra, ma2008b]
---
## Definition
The **state** of a dynamic system is the smallest set of variables $x_1,\dots,x_n$ (**state variables**) such that knowing them at $t_0$ plus the input for $t\ge t_0$ determines the behaviour for all $t\ge t_0$. They form the **state vector** $x(t)$, living in the $n$-dimensional **state space**. The state-space method describes not only input–output behaviour but the **complete internal behaviour** of a plant. The outputs of the integrators in a simulation diagram are a natural choice of state variables (their number = number of integrators). The representation is **not unique**.

For a [[Linear Time-Invariant System]] (LTI):
$$\dot x(t)=Ax(t)+Bu(t),\qquad y(t)=Cx(t)+Du(t),$$
with $A$ the **state matrix**, $B$ the **input matrix**, $C$ the **output matrix**, $D$ the **direct transmission matrix**. For nonlinear or time-varying systems: $\dot x=f(x,u,t)$, $y=g(x,u,t)$.

## Properties
### From state space to the transfer function
Laplace transform with $x(0)=0$ (see [[Laplace Transform]]):
$$sX(s)=AX(s)+BU(s)\;\Rightarrow\;(sI-A)X(s)=BU(s)\;\Rightarrow\;X(s)=(sI-A)^{-1}BU(s),$$
$$Y(s)=CX(s)+DU(s)=\left[C(sI-A)^{-1}B+D\right]U(s).$$
Hence
$$\boxed{G(s)=C(sI-A)^{-1}B+D=\frac{C\,\operatorname{adj}(sI-A)\,B}{\det(sI-A)}+D.}$$
The poles of $G$ are among the roots of $\det(sI-A)=0$, i.e. the [[Eigenvalues and Eigenvectors|eigenvalues]] of $A$ — which is why stability can be read from $A$ (see [[BIBO Stability and Pole Location]]). $\Phi(s)=(sI-A)^{-1}$ is the Laplace transform of the [[State Transition Matrix]] $e^{At}$. For MIMO systems the same formula gives the **transfer matrix** $G(s)$ ($q\times p$).

Tools needed (slides' reminder): matrix multiplication, cofactors, transpose, adjugate.

### From an $n$-th order ODE — input without derivatives
For $y^{(n)}+a_1y^{(n-1)}+\dots+a_{n-1}\dot y+a_ny=u$, choose phase variables $x_1=y$, $x_2=\dot y$, …, $x_n=y^{(n-1)}$:
$$\dot x_1=x_2,\;\dots,\;\dot x_{n-1}=x_n,\;\dot x_n=-a_nx_1-\dots-a_1x_n+u,$$
$$A=\begin{pmatrix}0&1&0&\cdots&0\\ \vdots&&\ddots&&\vdots\\0&0&0&\cdots&1\\-a_n&-a_{n-1}&\cdots&&-a_1\end{pmatrix},\quad B=\begin{pmatrix}0\\\vdots\\0\\1\end{pmatrix},\quad C=(1\;0\;\cdots\;0).$$

### Input with derivatives (Ogata's $\beta$ method)
For $y^{(n)}+a_1y^{(n-1)}+\dots+a_ny=b_0u^{(n)}+b_1u^{(n-1)}+\dots+b_nu$, the phase variables no longer work (they need not give a unique solution). Define
$$x_1=y-\beta_0u,\quad x_2=\dot x_1-\beta_1u,\quad\dots,\quad x_n=\dot x_{n-1}-\beta_{n-1}u,$$
with
$$\beta_0=b_0,\;\beta_1=b_1-a_1\beta_0,\;\beta_2=b_2-a_1\beta_1-a_2\beta_0,\;\dots,\;\beta_n=b_n-a_1\beta_{n-1}-\dots-a_n\beta_0.$$
Then
$$\dot x_i=x_{i+1}+\beta_iu\;(i<n),\qquad \dot x_n=-a_nx_1-\dots-a_1x_n+\beta_nu,\qquad y=x_1+\beta_0u,$$
i.e. $A$ is the same companion matrix, $B=(\beta_1,\dots,\beta_n)^T$, $C=(1\,0\cdots0)$, $D=\beta_0$.

### Transfer function → state space
Cross-multiply $G(s)=Y/U$, return to the time domain, and apply one of the two constructions above.

## Examples
**Mass–spring–damper.** $m\ddot y+b\dot y+ky=u$. With $x_1=y$, $x_2=\dot y$:
$$\dot x=\begin{pmatrix}0&1\\-\frac km&-\frac bm\end{pmatrix}x+\begin{pmatrix}0\\\frac1m\end{pmatrix}u,\qquad y=(1\;0)\,x.$$
Then $sI-A=\begin{pmatrix}s&-1\\\frac km&s+\frac bm\end{pmatrix}$, $\det=s^2+\frac bms+\frac km$, and
$$G(s)=\frac{1}{\det}(1\;0)\begin{pmatrix}s+\frac bm&1\\-\frac km&s\end{pmatrix}\begin{pmatrix}0\\\frac1m\end{pmatrix}=\frac{1/m}{s^2+\frac bms+\frac km}=\frac{1}{ms^2+bs+k}.$$
*Note:* the text layer of the PDF version of "Modelos matemáticos parte uno" garbles this slide (it reads $x_1'=x_1$ with swapped coefficients); the rendered PowerPoint slide has the correct $x_1'=x_2$.

**Cart system with derivative input.** $\ddot y+\frac bm\dot y+\frac km y=\frac bm\dot u+\frac km u$: $a_1=\frac bm$, $a_2=\frac km$, $b_0=0$, $b_1=\frac bm$, $b_2=\frac km$. So $\beta_0=0$, $\beta_1=\frac bm$, $\beta_2=\frac km-\left(\frac bm\right)^2$, and
$$\dot x=\begin{pmatrix}0&1\\-\frac km&-\frac bm\end{pmatrix}x+\begin{pmatrix}\frac bm\\\frac km-\left(\frac bm\right)^2\end{pmatrix}u,\qquad y=(1\;0)x.$$

**Given $(A,B,C,D)$ (Tarea individual 2, problem 3).** $A=\begin{pmatrix}0&1\\3&-1\end{pmatrix}$, $B=\begin{pmatrix}1\\1\end{pmatrix}$, $C=(1\;0)$, $D=2$.
$\det(sI-A)=s(s+1)-3=s^2+s-3$, $(sI-A)^{-1}B=\frac{1}{s^2+s-3}\begin{pmatrix}s+1&1\\3&s\end{pmatrix}\begin{pmatrix}1\\1\end{pmatrix}=\frac{1}{s^2+s-3}\begin{pmatrix}s+2\\s+3\end{pmatrix}$, so
$$G(s)=\frac{s+2}{s^2+s-3}+2=\frac{2s^2+3s-4}{s^2+s-3}.$$
(Open-loop unstable: a root $\frac{-1+\sqrt{13}}{2}>0$.)

**Slides' MATLAB checks.** $A=\begin{pmatrix}-4&-1.5\\4&0\end{pmatrix}$, $B=\begin{pmatrix}2\\0\end{pmatrix}$, $C=(1.5\;0.625)$, $D=0$ → `ss2tf` gives $G=\dfrac{3s+5}{s^2+4s+6}$. The $3\times3$ companion example $A=\begin{pmatrix}0&1&0\\0&0&1\\-5&-25&-5\end{pmatrix}$, $B=(0,25,-120)^T$, $C=(1\,0\,0)$ gives $G=\dfrac{25s+5}{s^3+5s^2+25s+5}$ (verified symbolically; if the slide appears to read "245", that is a rendering artefact — check).

## See also
[[Transfer Function]], [[Mechanical and Electrical System Models]], [[Block Diagram Reduction]], [[BIBO Stability and Pole Location]], [[Optimal Control]], [[Linearization]]
