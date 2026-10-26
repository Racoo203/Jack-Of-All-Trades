---
title: Second Order Difference Equation
domain: Stochastic Processes
course: Stochastic Processes
unit: Foundations & Random Walks
level: MSc
status: seeding
confidence: 0
tags: [seeding]
---
## Definition
A (linear) second order difference equation is a recurrence relating a sequence $\{u_n\}$ to its two preceding terms via a linear relation with constant coefficients, e.g.
$$
u_n = p\, u_{n+1} + q\, u_{n-1}
$$
(or equivalently, after rearranging, an expression in $u_n, u_{n-1}, u_{n-2}$). It is called *homogeneous* if, once rearranged with all terms on one side, the right-hand side is $0$; otherwise it is *inhomogeneous*. Second order difference equations are the discrete-time analogue of second order linear differential equations, and arise naturally when solving boundary-value problems for random walks, such as the [[Gambler's Ruin|gambler's ruin]] problem.

## Properties
### Solving the homogeneous equation
To solve a homogeneous equation such as $p\,u_{n+1} - u_n + q\,u_{n-1} = 0$, guess a solution of the form $u_n = A w^n$. Substituting and dividing through by $w^{n-1}$ gives the **auxiliary equation**
$$
p w^2 - w + q = 0 \iff (pw - q)(w-1) = 0
$$
with roots $w_1 = 1$ and $w_2 = q/p$ (using $p + q = 1$).

#### Case 1: distinct roots ($p \neq q$)
The general solution is a linear combination of the two independent solutions $w_1^n$ and $w_2^n$:
$$
u_n = A_1 (1)^n + A_2 \left(\frac{q}{p}\right)^n = A_1 + A_2 \left(\frac{q}{p}\right)^n
$$
The constants $A_1, A_2$ are fixed by two boundary conditions (e.g. $u_0$ and $u_N$ for some $N$).

#### Case 2: repeated roots ($p = q$)
When $p = q$, the auxiliary equation has a double root $w_1 = w_2 = 1$, and the naive combination $A_1 + A_2$ degenerates to a single constant. In this case the general solution instead takes the form
$$
u_n = (A_1 + A_2\, n)(1)^n = A_1 + A_2\, n
$$
i.e. an extra factor of $n$ multiplies the second, repeated solution — the same phenomenon as for repeated roots of the characteristic equation of a linear ODE.

### Solving the inhomogeneous equation
For an inhomogeneous equation such as $p\, v_{n+1} - v_n + q\, v_{n-1} = -1$, first solve the associated homogeneous equation (right-hand side set to $0$) to obtain the **complementary function**. Then find *any* particular solution $f(n)$ of the full inhomogeneous equation, and add it to the complementary function:
$$
v_n = \underbrace{A_1 + A_2 (q/p)^n}_{\text{complementary function}} + \underbrace{f(n)}_{\text{particular solution}}
$$
In this course, $f(n)$ can always be found among the quadratics $a + bn + cn^2$ with only one of $a,b,c$ non-zero:
- If $p \neq q$: try $f(n) = k n$. Substituting and using $p+q=1$ gives $k = \dfrac{1}{q-p}$ (equivalently $-\dfrac{1}{p-q}$).
- If $p = q$: the linear ansatz fails (its own contribution collapses to $0$, since $p=q$ kills the coefficient of $k$), so instead try $f(n) = k n^2$. Substituting gives $k = -1$.

As with the homogeneous case, the remaining constants $A_1, A_2$ are pinned down by the boundary conditions of the specific problem (e.g. $v_0 = v_N = 0$).

## Examples
### Gambler's ruin
The ruin probability $y_k$ in the [[Gambler's Ruin|gambler's ruin]] problem satisfies the homogeneous equation $p\, y_{k+1} - y_k + q\, y_{k-1} = 0$ with boundary conditions $y_0 = 1, y_N = 0$; the expected game duration $\mu_k$ satisfies the inhomogeneous equation $\mu_k = p\,\mu_{k+1} + q\,\mu_{k-1} + 1$ with boundary conditions $\mu_0 = \mu_N = 0$. Both are solved by the methods above.

## See also
- [[Gambler's Ruin]]
- [[Random Walk]]
