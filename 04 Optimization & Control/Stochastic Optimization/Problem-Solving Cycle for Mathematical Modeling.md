---
title: "Problem-Solving Cycle for Mathematical Modeling"
domain: "Optimization & Control"
course: "Stochastic Optimization"
level: BSc
status: drafted
confidence: 0
tags: [methodology, stochastic-optimization]
---
## Definition
The **problem-solving cycle** is a methodology (based on the scientific method) that formalizes applied mathematical modeling into explicit stages, making the modeler's decisions and their implications visible rather than implicit. It is a *cycle*, not a linear pipeline, because it begins and ends in the real situation being analyzed — modeling is not purely a theoretical exercise. The stages are:
$$
\text{Realidad (Reality)} \;\to\; \text{Problema (Problem)} \;\to\; \text{Modelo (Model)} \;\to\; \text{Algoritmo (Algorithm)} \;\to\; \text{Solución (Solution)} \;\to\; \text{Interpretación} \;\to\; \text{Implementación},
$$
and back to reality.

## Properties
### Formulating the problem
The essence of formulation is isolating the *real* problem from other, related problems that could mask it with irrelevant complexity. The modeler needs a clear view of the solution approach — which model(s) will represent the problem, which technique(s) will solve them, and in what order — often while collaborating with domain experts who understand the application but not the mathematics, and who may not realize their situation is actually several separable problems. Formulating the wrong problem is called out as the single biggest risk at this stage.

### The model: structure (metamodel) and size
A model is built through **modeling** — an abstraction process turning problem elements (which have explicit real-world meaning) into model elements (variables, functions, equations, which have none). Two properties of a model matter separately:
- **Structure** (also called the **metamodel**): the equations/functions and their associated variables. Two models "share a structure" if they differ only in size or in the numeric constants used, not in their functional form — the structure defines a whole *family* of models. Defining the structure is a one-time design activity by the modeler, refined and fixed once it reliably produces useful answers; it requires a clear idea of the solution technique in advance.
- **Size**: the number of elements in a specific instance of the model, built dynamically from data via a modeling language — this is what changes from one problem instance to the next even when the structure stays fixed.
A key structural decision is **relaxation**: deliberately dropping model elements under the "reasonable consideration" that their omission won't materially affect the usefulness of the solution — done either to make the model solvable by a known algorithm, or to reduce solve time for realistically sized instances.

### The algorithm and its failure modes
The algorithm is the mechanical procedure that generates solutions from the model — the step of the cycle furthest from reality. Two properties matter: whether it *can* solve the model, and how long it takes. Typical failure modes at this stage: the algorithm finds no solution; no solution is found in reasonable time; the solution isn't unique. Causes include using the wrong algorithm, bad parameterization, numerical instability, or the model itself being inconsistent or incomplete.

### Interpretation and implementation close the cycle
A mathematically valid solution must still be translated back into the problem's own language, and a solution that is "correct" but makes no practical sense is a signal that the model, the solution strategy, or the data may be flawed. **Implementation** is the final test: use the solution in reality and compare its actual effect against the expected one; if it doesn't hold up, some phase of the cycle must be revisited. This is inherently a human, collaborative process (multiple stakeholders with different interests), and factors like the cost of obtaining a solution relative to its benefit, or the availability and quality of the required data, shape the whole exercise.

## Examples
This methodology frames the rest of the course: e.g. choosing to model a queueing problem as an exact $M/M/s$ system (see [[Queueing System]]) is a *structural* choice, while choosing to fall back on [[Monte Carlo Method|Monte Carlo simulation]] instead is a *relaxation* of that exact structure when the closed-form assumptions don't hold.

## See also
[[Monte Carlo Method]], [[Queueing System]]
