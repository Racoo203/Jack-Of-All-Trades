---
title: "Block Diagram Reduction"
domain: "Optimization & Control"
course: "Non-linear Optimization"
unit: "Control Theory Foundations"
level: BSc
status: seeding
confidence: 0
tags: [control-theory, ma2008b]
---
## Definition
A **block diagram** is a graphical representation of the function of each component of a system and of the signal flow between them. Its elements (course slides):

- **Signals** — arrows, each flowing in one direction (input $X$, output $Y$, error $E$).
- **Blocks** — each holds the [[Transfer Function]] of a component (valve, motor, sensor, process, controller); output = block × input.
- **Summing point** — a circle that adds/subtracts incoming signals according to their signs.
- **Pickoff (branch) point** — where a signal is sent unchanged along several paths.

**Block diagram algebra** (Ogata Table 3-1) rewrites a diagram into a simpler equivalent one with the same input–output relation, until a single block $T(s)=C(s)/R(s)$ remains.

## Properties
### Core rules and their derivations
1. **Series (cascade).** $Y=H(GX)$ ⇒ single block $GH$.
2. **Parallel.** $Y=GX\pm HX$ ⇒ single block $G\pm H$ (sign of the summing point).
3. **Feedback loop** — "one of the most important rules". With $E=X\mp HY$ and $Y=GE$:
$$Y=G(X\mp HY)\;\Rightarrow\;Y(1\pm GH)=GX\;\Rightarrow\;\frac YX=\frac{G}{1\pm GH}$$
(upper signs: negative feedback).
4. **Summing points** can be interchanged or split into several summing points freely (addition is commutative and associative).
5. **Moving a pickoff point.** Pickoff points can be swapped when no block lies between them. Moving a pickoff point from before a block $G$ to after it: the branch now carries $GX$, so insert $1/G$ in the branch. Moving it from after $G$ to before: the branch now carries $X$, so insert $G$.
6. **Moving a summing point.** From before $G$ to after $G$: original output $G(X_1-X_2)=GX_1-GX_2$, so the moved branch needs a block $G$. From after $G$ to before: original output $GX_1-X_2=G\left(X_1-\tfrac1GX_2\right)$, so the moved branch needs $1/G$.
7. **Interchanging a summing point and a pickoff point is not always simple** — it changes which signal is picked off and must be compensated explicitly.

### Strategy
Look first for series and parallel structures, then for inner loops you can close with rule 3; move summing/pickoff points only to untangle overlapping loops. Check the reduced block with a step input in Simulink against the original diagram — both must give the same response.

## Examples
**Example 1 (slides).** A forward path with $G_1$ and $H_1$ in parallel (both added), unity forward summing, and feedback $H_2$:
$$\text{parallel: }G_1+H_1,\qquad T(s)=\frac{G_1+H_1}{1+H_2(G_1+H_1)}.$$

**Example 2 (slides; Ogata's classic).** $R\to$ summing (feedback $-1$ from $C$) → summing (feedback $+H_1$ from the output of $G_2$) → $G_1$ → summing (feedback $-H_2$ from $C$) → $G_2$ → $G_3$ → $C$.

1. The $H_1$ loop and the $H_2$ loop overlap. Move the $H_1$ pickoff point from the output of $G_2$ to the output of $G_3$ (rule 5, left → right), which puts $1/G_3$ in that branch: it becomes $H_1/G_3$.
2. Close the inner loop $G_2G_3$ with $H_2$: $\dfrac{G_2G_3}{1+G_2G_3H_2}$.
3. Series with $G_1$ and close the positive loop with $H_1/G_3$:
$$\frac{\dfrac{G_1G_2G_3}{1+G_2G_3H_2}}{1-\dfrac{H_1}{G_3}\cdot\dfrac{G_1G_2G_3}{1+G_2G_3H_2}}=\frac{G_1G_2G_3}{1-G_1G_2H_1+G_2G_3H_2}.$$
4. Close the unity negative feedback:
$$T(s)=\frac{G_1G_2G_3}{1-G_1G_2H_1+G_2G_3H_2+G_1G_2G_3}.$$
<!-- UNVERIFIED: the slide's written intermediate uses 1 + H1/G3 · (...) — the sign of the H1 loop depends on the summing-point sign in the figure; check against the slide figure (the classic Ogata version has +H1, giving the minus sign above). -->

## See also
[[Transfer Function]], [[Control System Fundamentals]], [[Signal Flow Graph]], [[Mason's Gain Formula]], [[State-Space Representation]]
