---
title: "Powell's Method"
domain: "Optimization & Control"
course: "Non-linear Optimization"
unit: "Unconstrained Methods"
level: BSc
status: drafted
confidence: 0
tags: [nonlinear-optimization, numerical-methods, ma2008b, exam]
---
## Definition
**Powell's conjugate-direction method** is a **derivative-free** (direct search) method for $\min f(x)$, $x\in\mathbb R^n$. It performs exact [[Line Search|line searches]] along a set of directions and, after each sweep, adds a **pattern direction** that tends to become conjugate to the others.

**One cycle (as worked in the course, Ejercicios Powell).** Given $x_0$ and directions $d_1,\dots,d_n$ (initially the coordinate axes $e_1,\dots,e_n$):
1. For $i=1..n$: $\lambda_i^*=\arg\min_\lambda f(x_{i-1}+\lambda d_i)$, $x_i=x_{i-1}+\lambda_i^*d_i$.
2. Pattern direction $d_{\text{new}}=x_n-x_0$.
3. Line search along $d_{\text{new}}$: $x_{n+1}=x_0+\lambda^*d_{\text{new}}$ (equivalently from $x_n$ — it is the same line).
4. Discard $d_1$, shift the others and append $d_{\text{new}}$; set $x_0\leftarrow x_{n+1}$ and repeat until the improvement is below tolerance.

In hand work each line search is: write $\varphi(\lambda)=f(x+\lambda d)$, solve $\varphi'(\lambda)=0$.

## Properties
### Conjugate directions and quadratic termination
Directions $d_i,d_j$ are **$Q$-conjugate** if $d_i^TQd_j=0$ ($i\ne j$). For $f=\frac12x^TQx-b^Tx$ with $Q$ PD, exact line searches along $n$ mutually conjugate directions reach the minimizer in at most $n$ steps.
*Proof.* Conjugate directions are linearly independent, so $x^*-x_0=\sum_i\sigma_id_i$. Multiply by $d_k^TQ$: $\sigma_k=\dfrac{d_k^TQ(x^*-x_0)}{d_k^TQd_k}=\dfrac{-d_k^Tg_0}{d_k^TQd_k}$ (using $Qx^*=b$). Exact line search along $d_k$ from $x_{k-1}$ gives $\lambda_k=\dfrac{-d_k^Tg_{k-1}}{d_k^TQd_k}$, and $d_k^Tg_{k-1}=d_k^T\big(g_0+Q\sum_{i<k}\lambda_id_i\big)=d_k^Tg_0$ by conjugacy. So $\lambda_k=\sigma_k$ for every $k$, and $x_n=x^*$. ∎

### Why the pattern direction is conjugate (parallel subspace property)
If $x_a$ and $x_b$ are the minimizers of a quadratic along two **parallel** lines with direction $d$, then $x_b-x_a$ is $Q$-conjugate to $d$: from $d^T\nabla f(x_a)=d^T\nabla f(x_b)=0$ we get $d^TQ(x_b-x_a)=0$. Powell's cycle manufactures exactly this situation, so for a quadratic, $n$ cycles generate $n$ conjugate directions and the method terminates (Powell, 1964). In practice the direction set can become nearly linearly dependent; Powell's safeguarded variant sometimes keeps the old set.

### Separable functions
If $f$ is a sum of one-variable terms (e.g. $(x_1-a)^2+(x_2-b)^2$, or $4(x_1-3)^2+(x_2+1)^2$), the coordinate directions are already conjugate ($Q$ diagonal) and **one sweep** reaches the minimum; the pattern step then returns $\lambda^*=1$.

## Examples
**Ejercicios Powell #3 (coupled variables).** $f=(2x_1-4)^2+(x_1-x_2)^2$, $x_0=(0,0)$, $d_1=e_1$, $d_2=e_2$.
- Along $d_1$: $\varphi(\lambda)=(2\lambda-4)^2+\lambda^2$, $\varphi'=4(2\lambda-4)+2\lambda=10\lambda-16=0\Rightarrow\lambda=1.6$; $x_1=(1.6,0)$, $f=0.64+2.56=3.2$.
- Along $d_2$: $\varphi(\lambda)=(3.2-4)^2+(1.6-\lambda)^2\Rightarrow\lambda=1.6$; $x_2=(1.6,1.6)$, $f=0.64$.
- Pattern $d_{\text{new}}=x_2-x_0=(1.6,1.6)$: $\varphi(\lambda)=(3.2\lambda-4)^2+0\Rightarrow\lambda=1.25$; $x_3=(2,2)$, $f=0$.
Since $f\ge0$, $(2,2)$ is the global minimum — reached in one cycle, as the theory predicts for $n=2$ once the pattern direction (conjugate to $e_2$) is used.

**Class example (27/05/2025).** $f=(x_1-2)^4+(x_1-2x_2)^2$, $x_0=(0,0)$.
- Along $e_1$: $\varphi=(\lambda-2)^4+\lambda^2$, $\varphi'=4(\lambda-2)^3+2\lambda=0\Rightarrow\lambda\approx1.165$ (solve $2u^3+u+2=0$ with $u=\lambda-2$); $x_1=(1.165,0)$.
- Along $e_2$: $\varphi=(1.165-2)^4+(1.165-2\lambda)^2\Rightarrow\lambda=0.583$; $x_2=(1.165,0.583)$.
- Pattern $(1.165,0.583)\approx1.165\,(1,\tfrac12)$: on this line $x_1-2x_2\approx0$, so $\varphi\approx(1.165\lambda-2)^4\Rightarrow\lambda=2/1.165$ and $x_3=(2,1)$, $f=0$ — the global minimum (non-quadratic $f$, but the valley $x_1=2x_2$ is found by the pattern step).

**Ejercicios Powell #1–#2 and exam problem 3** are separable ($(x_1-1)^2+(x_2-2)^2$ → $(1,2)$; $4(x_1-3)^2+(x_2+1)^2$ → $(3,-1)$; $(x_1-7)^2+(x_2-2)^2$ → $(7,2)$): one sweep suffices and the pattern search confirms $\lambda^*=1$.

## See also
[[Line Search]], [[Steepest Descent]], [[Newton's Method (Optimization)]], [[Hooke-Jeeves Method]], [[Conjugate Gradient Method]]
