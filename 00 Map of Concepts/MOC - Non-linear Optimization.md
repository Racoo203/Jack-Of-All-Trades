---
subject: Non-linear Optimization
type: MOC
course_code: MA2008B
course_name_es: "Análisis numérico para la optimización no-lineal"
domain: Optimization & Control
level: BSc
status: drafted
confidence: 0
tags:
  - moc
  - exam
  - control-theory
  - nonlinear-optimization
---
## Concept narrative

MA2008B (Tec de Monterrey, 2025, group 601) is two courses stitched together by one idea: **a dynamic system is something you can model, analyze, and then optimize**. The syllabus (Ogata, *Modern Control Engineering*, as the main textbook) runs in three movements, each taught by a different professor.

**Movement 1 — classical control (Modules 1–5).** A [[Control System Fundamentals|control system]] is modeled first by a [[Linear Time-Invariant System|linear time-invariant]] ODE. The [[Laplace Transform]] turns that ODE into algebra; the [[Unit Step and Dirac Delta Functions|unit step and Dirac delta]] model switched and impulsive inputs; the [[Convolution Theorem (Laplace)|convolution theorem]] inverts products; and the [[Initial and Final Value Theorems]] read off limiting behaviour without inverting. Setting initial conditions to zero gives the [[Transfer Function]] $G(s)=Y(s)/U(s)$, which is built from physical laws for [[Mechanical and Electrical System Models|mass–spring–damper and RLC systems]], combined through [[Block Diagram Reduction]], and — for the "modern" view — rewritten as a [[State-Space Representation]] with $G(s)=C(sI-A)^{-1}B+D$.

Analysis then asks two questions. *How does the system respond?* The [[First-Order System Response]] is governed by one time constant $\tau$; the [[Second-Order System Response]] by $(\zeta,\omega_n)$. *Is it stable?* [[BIBO Stability and Pole Location|Stability]] means all closed-loop poles in the open left half-plane, and the [[Routh-Hurwitz Criterion]] counts right-half-plane roots without solving the characteristic polynomial — including the range of a gain $K$ that keeps a [[PID Controller|proportional/PID loop]] stable. The [[Root Locus]] (with its [[Root Locus Construction Rules|construction rules]]) shows how closed-loop poles move as $K$ goes from $0$ to $\infty$. Finally, [[Frequency Response]] methods — [[Bode Diagram|Bode]], polar/[[Nyquist Stability Criterion|Nyquist]], and [[Nichols Chart|Nichols]] plots — judge closed-loop stability from the open-loop $G(j\omega)$ and quantify it through [[Gain and Phase Margins]].

**Movement 2 — optimal control (Module 6).** Instead of *placing* poles, choose the control signal $u(t)$ that maximizes a functional: [[Optimal Control]]. The workhorse is [[Pontryagin's Maximum Principle]] — form the Hamiltonian, solve the costate equation with a transversality condition, optimize $H$ in $u$, then integrate the state equation.

**Movement 3 — nonlinear programming (Modules 7–9).** A [[Nonlinear Programming Problem]] has decision variables, an objective and a [[Feasible Region|feasible region]]. [[Convex Set|Convexity]] of the region and [[Convex Function|of the objective]] (checked through [[Definiteness of Quadratic Forms|definiteness]] of the [[Hessian Matrix|Hessian]]) is what turns local optima into global ones. [[Optimality Conditions (Unconstrained)]] come from Taylor's theorem; [[Lagrange Multipliers]] handle equality constraints and the [[Karush–Kuhn–Tucker conditions]] handle inequalities. Numerically: [[Line Search]] reduces multivariable descent to one-dimensional problems, solved by bracketing ([[Fibonacci Search]], [[Golden Section Search]]) or curve fitting ([[Quadratic Interpolation Search]]); multivariable directions come from [[Steepest Descent]], [[Newton's Method (Optimization)|Newton]], the derivative-free [[Powell's Method]], or accelerated [[Nesterov Momentum]]. Constraints are pulled into the objective via [[Penalty and Merit Functions]] or [[Barrier Method|barrier (interior-point) functions]].

A side thread — aggregate production planning (Chopra & Meindl) — appears as a modeling exercise for the course challenge; it is an LP-modeling application rather than a concept, so it lives here only as a pointer to [[Linear Programming]].

---

## Concept map

### Unit 1 — Control theory foundations (Módulos 1–2)
- [[Control System Fundamentals]] — plant, sensor, controller, actuator; open vs closed loop; classical vs modern control
- [[Linear Time-Invariant System]] *(prerequisite, not yet written)*
- [[Laplace Transform]] — $\mathcal L\{f\}(s)=\int_0^\infty f(t)e^{-st}\,dt$; linearity, derivative rule, translation theorems
- [[Unit Step and Dirac Delta Functions]] — $\mathcal L\{\mathcal U(t-a)\}=e^{-as}/s$, $\mathcal L\{\delta(t-t_0)\}=e^{-st_0}$
- [[Convolution Theorem (Laplace)]] — $\mathcal L\{f*g\}=F(s)G(s)$
- [[Initial and Final Value Theorems]] — $f(\infty)=\lim_{s\to0}sF(s)$
- [[Transfer Function]] — zero initial conditions; impulse response $g(t)=\mathcal L^{-1}\{G\}$
- [[Mechanical and Electrical System Models]] — $ms^2+bs+k$, RC, RLC, coupled systems
- [[Block Diagram Reduction]] — series, parallel, feedback $G/(1+GH)$, moving summing/pickoff points
- [[State-Space Representation]] — $\dot x=Ax+Bu,\;y=Cx+Du$, $G(s)=C(sI-A)^{-1}B+D$

### Unit 2 — Transient response and stability (Módulos 2–3)
- [[First-Order System Response]] — $G=K/(\tau s+1)$; 63.2 % at $t=\tau$, $T_s\approx4\tau$
- [[Second-Order System Response]] — $\omega_n^2/(s^2+2\zeta\omega_n s+\omega_n^2)$; overshoot, settling time
- [[BIBO Stability and Pole Location]] — LHP poles ⇔ stable; marginal stability on $j\omega$ axis
- [[Routh-Hurwitz Criterion]] — sign changes in first column = # RHP roots; zero-row case
- [[PID Controller]] — P, PI, PD, PID actions; gain ranges via Routh

### Unit 3 — Root locus (Módulo 4)
- [[Root Locus]] — locus of $1+KG(s)H(s)=0$; magnitude and angle conditions
- [[Root Locus Construction Rules]] — real-axis segments, asymptotes/centroid, breakaway, $j\omega$ crossing, departure angles

### Unit 4 — Frequency response (Módulo 5)
- [[Frequency Response]] — $G(j\omega)$; minimum vs non-minimum phase
- [[Bode Diagram]] — magnitude (dB) and phase vs $\log\omega$; asymptotes
- [[Nyquist Stability Criterion]] — $Z=N+P$; polar plots; time delay
- [[Gain and Phase Margins]]
- [[Nichols Chart]] — dB magnitude vs phase

### Unit 5 — Optimal control (Módulo 6)
- [[Optimal Control]] — state, control, objective functional
- [[Pontryagin's Maximum Principle]] — $H=F+\lambda f$, $\dot\lambda=-H_x$, $\lambda(T)=0$, $H_u=0$

### Unit 6 — NLP foundations and optimality (Módulos 7, 9)
- [[Nonlinear Programming Problem]] — formulation, classification, feasible region, NP-hardness remark
- [[Convex Set]] — extreme points, convex combinations
- [[Convex Function]] — Jensen-type definition, first- and second-order criteria, local ⇒ global
- [[Definiteness of Quadratic Forms]] — eigenvalue and principal-minor tests
- [[Optimality Conditions (Unconstrained)]] — $\nabla f=0$, Hessian test, Taylor
- [[Lagrange Multipliers]]
- [[Karush–Kuhn–Tucker conditions]]

### Unit 7 — Unconstrained algorithms (Módulo 8)
- [[Line Search]] — exact vs inexact; Armijo backtracking
- [[Fibonacci Search]]
- [[Golden Section Search]] — ratio $R=(\sqrt5-1)/2$
- [[Quadratic Interpolation Search]] — DSC bracketing + parabola fit
- [[Steepest Descent]] — $x_{k+1}=x_k-\alpha\nabla f(x_k)$; zig-zag; step-size stability
- [[Newton's Method (Optimization)]] — $x_{k+1}=x_k-H^{-1}\nabla f$; modified Newton; Levenberg–Marquardt; Cholesky
- [[Powell's Method]] — conjugate directions without derivatives
- [[Nesterov Momentum]] — look-ahead gradient

### Unit 8 — Constrained algorithms (Módulos 7, 9)
- [[Penalty and Merit Functions]] — Newton on the KKT system, exact/augmented penalty
- [[Barrier Method]] — log barrier, $\mu\to0$, fraction-to-boundary step

---

## Key dependency chains

```
Linear ODE ──> Laplace Transform ──> Transfer Function ──┬──> Block Diagram Reduction
     │               │                                  │
     │        Step/Delta, Convolution,                  ├──> Closed-loop G/(1+GH)
     │        Initial/Final Value                       │          │
     └──> State-Space Representation ──(C(sI-A)^-1B+D)──┘          ▼
                                             Poles ──> BIBO Stability ──> Routh-Hurwitz ──> PID gain ranges
                                                │
                                                ├──> Root Locus (1+KGH=0) ──> Construction Rules
                                                └──> Frequency Response G(jω) ──> Bode / Nyquist / Nichols
                                                                                        └──> Gain & Phase Margins

Optimal Control ──> Hamiltonian ──> Pontryagin's Maximum Principle

Taylor's theorem ──> Optimality Conditions ──> Lagrange Multipliers ──> KKT
       │                     ▲
Quadratic forms ──> Hessian definiteness ──> Convex Function ──(local = global)──┘
                                                                    
Line Search (Fibonacci / Golden / Quadratic / Armijo)
      └──> Steepest Descent ──> Newton ──> modified Newton / Levenberg–Marquardt
      └──> Powell (derivative-free)        Nesterov Momentum
KKT ──> Newton on KKT system ──> Penalty/Merit functions ──> Barrier (interior point)
```

---

## Exam focus

The evaluation weights the *examen argumentativo* at 50 %, and the Module 4–5 and Module 6 exams in `Resources/` are procedural, hand-worked problems. High-priority, in rough order of how often they appear in homework/exams:

1. **Root locus by hand** — poles/zeros, real-axis segments, centroid & asymptote angles, breakaway points ($dK/ds=0$, then check membership), $j\omega$ crossing and $K_{\max}$ (Routh or $s=j\omega$), departure angles. (Tarea 1 M4, Actividad 2, Module 4–5 exam.)
2. **Pontryagin 5-step recipe** — $H$, costate, transversality $\lambda(T)=0$, $H_u=0$, integrate state with $x(0)$. (Module 6 exam, Laboratorio Pontryagin, Tarea Principio del Máximo.)
3. **Routh arrays**, including the zero-row (auxiliary polynomial) case and finding the stabilizing range of $K$.
4. **Transfer function from a physical system** by two methods (mesh/Newton equations and state space). (Actividad 4.)
5. **Block diagram reduction** to $C(s)/R(s)$. (Entregable diagramas de bloques.)
6. **Bode/Nyquist/Nichols + margins**, e.g. choose $K$ for a 50° phase margin; Nyquist with right-half-plane open-loop poles; maximum $K$ with time delay.
7. **Hand iterations of Powell, gradient ascent/descent, Nesterov** (Laboratorio Multimodal, June 2025 exam sheets) and **golden-section** (Python script).
8. **KKT case analysis** (enumerate active sets; check sign of multipliers and feasibility; argue sufficiency by convexity).

Question types: "draw and justify", "compute to k iterations", "determine stability and justify with the criterion", "find $K$ such that…", conceptual multiple choice on control history and vocabulary (Actividad colaborativa 2), and short-answer definitions (transfer function quiz).

---

## Open questions

- Syllabus topics with **no material in Resources yet**: [[Second-Order System Response]] (slides only link videos), steady-state error constants, [[Hooke-Jeeves Method]], univariate/cyclic search, [[Davidon-Fletcher-Powell Method]], subgradients, [[Method of Feasible Directions]], [[Quadratic Programming]] (Wolfe and Beale algorithms), separable programming. Drafts for these would be canonical-only.
- The **Nesterov update** used in the labs, $v_{k+1}=\beta v_k-\lambda(1-\beta)\nabla f(x_k+\beta v_k)$, has a $(1-\beta)$ damping factor that differs from the textbook form — confirm it is the professor's convention.
- Two Pontryagin homework problems (Tarea Principio del Máximo #2 and #3) have Hamiltonians that are **not concave/convex in $u$ in the direction the objective needs** — as posed, the stationary point is not the optimum and the problem is unbounded. Check what the professor intended (bounded control? sign typo?). See [[Pontryagin's Maximum Principle]].
- Tema 7 slides (Elizalde) conclude the KKT example with the wrong point — see [[Karush–Kuhn–Tucker conditions]].
- The root-locus script in the Module 4 submissions reports a departure angle of $+90°$ at $-1+2j$ for $G=1/[s(s+2)(s^2+2s+5)]$; hand computation gives $-90°$. It also lists $-3.5078$ as a breakaway point for $1/[s(s+3)(s+4)(s+8)]$, but that point is not on the real-axis locus. See [[Root Locus Construction Rules]].
