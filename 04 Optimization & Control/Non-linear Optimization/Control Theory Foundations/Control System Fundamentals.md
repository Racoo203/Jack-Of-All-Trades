---
title: "Control System Fundamentals"
domain: "Optimization & Control"
course: "Non-linear Optimization"
unit: "Control Theory Foundations"
level: BSc
status: drafted
confidence: 0
tags: [control-theory, ma2008b]
---
## Definition
A **control system** is a set of interconnected components that regulates a variable of interest inside a process, with the goal of keeping or driving the system's state to a desired behaviour. Its standard elements are:

- **Plant** — the process being controlled (output $y$, the *controlled variable*).
- **Sensor** — measures the controlled variable.
- **Controller** — computes the corrective action from the error between reference and measurement.
- **Actuator** — applies that action to the plant (the *manipulated variable* $u$).
- **Disturbance** — an external signal that pushes the output away from the reference.

**Open loop:** the control action does not depend on the output; there is no feedback, so disturbances are not corrected.

**Closed loop (feedback):** the output $Y(s)$ is fed back through $H(s)$ and compared with the reference $X(s)$ (or $R(s)$); the error drives the forward path $G(s)$. In the Laplace domain (see [[Laplace Transform]], [[Transfer Function]]):

$$[X(s)-H(s)Y(s)]\,G(s)=Y(s).$$

## Properties
### Closed-loop transfer function
Expanding and collecting $Y(s)$:

$$X(s)G(s)-H(s)G(s)Y(s)=Y(s)\;\Longrightarrow\;X(s)G(s)=Y(s)\,[1+G(s)H(s)]$$

$$\boxed{\;\frac{Y(s)}{X(s)}=\frac{G(s)}{1+G(s)H(s)}\;}$$

The equation $1+G(s)H(s)=0$ is the **characteristic equation**; its roots are the closed-loop poles, which govern [[BIBO Stability and Pole Location|stability]] and are the object of the [[Root Locus]]. With positive feedback the sign flips: $G/(1-GH)$.

### Why feedback helps
Feedback reduces the error between output and reference even in the presence of disturbances, and reduces sensitivity to plant-parameter variation, at the cost of more components (sensors) and the possibility of instability. Open loop is simpler and cheaper but cannot correct unmeasured disturbances.

### Classical vs modern control
| | Classical | Modern |
|---|---|---|
| Main tool | [[Laplace Transform]], [[Transfer Function]] (input–output) | [[State-Space Representation]] |
| Systems | linear, time-invariant, well known | may be nonlinear, time-varying |
| I/O | mainly SISO | MIMO |
| Design | [[Root Locus]], [[Frequency Response]] | [[Optimal Control]], state feedback |

When objectives decompose into subproblems, a combination of both is used.

### Historical milestones (course slides)
Watt's centrifugal governor (1788) — first significant feedback application; Nyquist's stability criterion (1932); Hazen coins "servomechanism" (1934); frequency-response methods (1940s); Evans' root locus (late 1940s–1950s). Classical designs are "acceptable but not optimal," which motivates [[Optimal Control]].

### Design process (Salinas slides)
1. Define requirements → 2. Modeling and analysis (ODEs, Laplace, block diagrams, simulation; evaluate stability and response) → 3. Design the control structure → 4. Select components (sensors, actuators, controllers) → 5. Implement and test → 6. Tune and optimize.

## See also
[[Transfer Function]], [[Block Diagram Reduction]], [[PID Controller]], [[BIBO Stability and Pole Location]], [[State-Space Representation]]
