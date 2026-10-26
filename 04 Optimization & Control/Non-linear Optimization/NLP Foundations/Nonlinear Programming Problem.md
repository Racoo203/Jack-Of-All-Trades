---
title: "Nonlinear Programming Problem"
domain: "Optimization & Control"
course: "Non-linear Optimization"
unit: "NLP Foundations"
level: BSc
status: drafted
confidence: 0
tags: [nonlinear-optimization, ma2008b]
---
## Definition
**Nonlinear programming (NLP)** is the set of techniques for optimizing a function subject to equality and/or inequality constraints when the objective or some constraint is **not linear**. General formulation (course slides):
$$\min_{x\in\mathbb R^n}f(x)\quad\text{s.t.}\quad g_i(x)\le0\;(i=1,\dots,m),\qquad h_j(x)=0\;(j=1,\dots,p),$$
or, in the maximization form used in Tema 7 (Elizalde),
$$\max z=f(x)\quad\text{s.t.}\quad g_i(x)\le b_i,\;x_j\ge0.$$
Basic **components of a model**:
- **decision variables** $x$ — what we want to determine;
- **objective** $f(x)$ — the goal to maximize or minimize (cost, profit, time…);
- **constraints** — what any solution must satisfy.

The **[[Feasible Region|feasible region]]** is the set of all points satisfying every constraint (all possible solutions); a **feasible solution** is any point in it; an **optimal solution** is a feasible point with the best objective value (local if best only in a neighbourhood, global if best over the whole region).

## Properties
### Classification (slides)
- By linearity: *linear programming* (objective and constraints linear, see [[Linear Programming]]) vs *nonlinear programming*.
- By constraints: *unconstrained* vs *constrained*.
- By dimension: *one-dimensional* vs *multidimensional*.
- By number of objectives: *single-objective* vs *multi-objective* — with $M$ objectives the decision space maps to a multidimensional **objective (search) space** $Z=\{z=f(x)\in\mathbb R^M:x\in X\}$ (see [[Multi-objective Optimization]]).
- By modality: an objective with a single minimum is **unimodal**; with several local/global minima, **multimodal**.
- Model types from OR: deterministic vs stochastic; static vs dynamic; simulation vs non-simulation (optimization) models.

### Standing assumptions in the course
Objective and constraints are continuous with continuous first partial derivatives (small changes in $x$ give small changes in values); only $\le,\ge,=$ constraints (no strict inequalities, so the feasible set is closed); deterministic data; continuous (not integer) variables; the domain is a connected region.

### Size and difficulty
Small scale (≤ 5 variables/constraints, by hand), intermediate (5–100, a PC), large scale (>100, specialized hardware and structure-exploiting algorithms). Many optimization problems are **NP-hard**: no known polynomial-time algorithm, and complexity grows super-polynomially with input size. Unlike the simplex method for LP, there is **no general algorithm** for NLP; each problem class needs its own method, and no method is a universal "panacea".

### Iterative algorithms and convergence
NLP algorithms generate a sequence $x_0,x_1,\dots$ that **converges toward** the optimum rather than reaching it in finitely many steps (as simplex does); we stop when close enough. Their theory splits into *global convergence* (does it converge from any start?) and *local convergence* (how fast near the solution — linear, superlinear, quadratic). "A good theory is better than a thousand runs." Algorithms are compared by: number of function evaluations, reliability, speed, user preparation time, precision, degree of constraint satisfaction, difficulty.

### Local vs global
Convexity is what guarantees that a local optimum is global: for $\max f$ with constraints $g_i(x)\le b_i$, it suffices that $f$ is **concave** and every $g_i$ **convex** (see [[Convex Function]], [[Convex Set]]).

### Method families (slides' taxonomy)
- **Analytical (conventional):** differential calculus, [[Lagrange Multipliers]], [[Karush–Kuhn–Tucker conditions|Kuhn–Tucker theory]], geometric, [[Quadratic Programming|quadratic]] and convex programming.
- **Search (numerical):** one-dimensional searches ([[Fibonacci Search]], [[Golden Section Search]], [[Quadratic Interpolation Search]]), [[Newton's Method (Optimization)|Newton–Raphson]], [[Steepest Descent|steepest ascent/descent]], direct search ([[Powell's Method]]), gradient methods (Fletcher, Davidon, Powell), Broyden–Fletcher, Fletcher–Reeves, penalty functions ([[Penalty and Merit Functions]]), feasible directions, sequential linear/quadratic programming.
- Linearization and graphical techniques.

## Examples
**Graphical (Tema 7).** $\max z=3x_1+5x_2$ s.t. $x_1\le4$, $9x_1^2+5x_2^2\le216$, $x_1,x_2\ge0$ (the slide prints "$\le0$", a typo). $\nabla z=(3,5)$ points to the direction of increase; the optimum is where a level line $3x_1+5x_2=z$ is tangent to the ellipse: tangency requires $(3,5)\parallel(18x_1,10x_2)$, i.e. $x_2=3x_1$, then $9x_1^2+45x_1^2=216\Rightarrow x_1=2$, $x_2=6$, $z^*=36$. Unlike LP, the optimum is not at a corner point.

**Non-convex region (Tema 7).** Replace the ellipse by $8x_1-x_1^2+14x_2-x_2^2\le49$ (plus $x_1\le4$, $2x_2\le14$). The constraint function is concave, so the region is not convex, and a local maximum need not be global (Hillier & Lieberman: local maxima at $(4,3)$ with $z=27$ and $(0,7)$ with $z=35$).

**Modeling exercise.** The aggregate production-planning case (Chopra & Meindl) asks for sets, decision variables, constraints and several objectives — an LP/goal-programming model.

## See also
[[Convex Set]], [[Convex Function]], [[Optimality Conditions (Unconstrained)]], [[Lagrange Multipliers]], [[Karush–Kuhn–Tucker conditions]], [[Line Search]]
