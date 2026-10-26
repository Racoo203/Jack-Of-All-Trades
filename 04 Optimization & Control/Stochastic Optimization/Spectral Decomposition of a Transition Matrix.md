---
title: "Spectral Decomposition of a Transition Matrix"
domain: "Optimization & Control"
course: "Stochastic Optimization"
level: BSc
status: drafted
confidence: 0
tags: [markov-chains, linear-algebra, stochastic-optimization]
---
## Definition
For a diagonalizable [[Transition Matrix]] $P$ (or $A$) of a [[Discrete-Time Markov Chain]] with $|S| = k$ states, the **spectral (eigen-) decomposition**
$$
P = Q\Lambda Q^{-1}, \qquad \Lambda = \operatorname{diag}(\lambda_1, \dots, \lambda_k),
$$
writes $P$ in terms of its eigenvalues $\lambda_i$ (the columns of $Q$ are the corresponding right eigenvectors) found from the characteristic equation $\det(P - \lambda I) = 0$. Because $Q\Lambda Q^{-1}$ satisfies $P^n = Q\Lambda^n Q^{-1}$ for every $n$, this is the course's preferred route to the long-run behavior $\lim_{n\to\infty}P^n$ of an [[Ergodic Markov Chain]] whenever solving $\pi = \pi P$ directly is inconvenient, or when the *entire* limiting matrix (not just $\pi$) is wanted.

A stochastic matrix always has $\lambda = 1$ as an eigenvalue (with right eigenvector $\mathbf{1}$, since rows sum to 1), and for an ergodic chain every other eigenvalue satisfies $|\lambda_i| < 1$.

## Properties
### The limit isolates the $\lambda=1$ term
Since $P^n = Q\Lambda^n Q^{-1}$ and $\Lambda^n = \operatorname{diag}(\lambda_1^n, \dots, \lambda_k^n)$, taking $n \to \infty$ with $\lambda_1 = 1$ and $|\lambda_i| < 1$ for $i > 1$ gives $\lambda_i^n \to 0$ for $i>1$ and $\lambda_1^n \to 1$, so
$$
\lim_{n\to\infty} \Lambda^n = \operatorname{diag}(1, 0, \dots, 0) \quad\Longrightarrow\quad \lim_{n\to\infty} P^n = Q\operatorname{diag}(1,0,\dots,0)Q^{-1}.
$$
Every row of this limiting matrix equals the [[Stationary Distribution]] $\pi$ (consistent with [[Ergodic Markov Chain]]).

### Worked example: 3-floor elevator
An elevator in a ground-floor + two-floor building has transition matrix (rows/columns ordered Bajo, Piso 1, Piso 2)
$$
A = \begin{bmatrix} 0.00 & 0.50 & 0.50 \\ 0.75 & 0.00 & 0.25 \\ 1.00 & 0.00 & 0.00 \end{bmatrix}.
$$
**Step 1 — characteristic polynomial.** $\det(A - \lambda I) = -\lambda^3 + \tfrac{7}{8}\lambda + \tfrac{1}{8} = 0$. Since $\lambda = 1$ is always a root for a stochastic matrix, synthetic division factors this as $-(\lambda-1)\left(\lambda^2 + \lambda + \tfrac{1}{8}\right) = 0$, and the quadratic formula on the second factor gives
$$
\lambda_1 = 1, \qquad \lambda_{2,3} = \frac{-2 \mp \sqrt{2}}{4}.
$$
Both $|\lambda_2|, |\lambda_3| < 1$, confirming the chain (already known to be ergodic) has a unique limit.

**Step 2 — eigenvectors.** Solving $(A - \lambda_i I)v_i = 0$ for each root gives
$$
v_1 = \begin{bmatrix}1\\1\\1\end{bmatrix}, \quad
v_2 = \begin{bmatrix} -\tfrac{2+\sqrt2}{4} \\ \tfrac{2\sqrt2-1}{4} \\ 1\end{bmatrix}, \quad
v_3 = \begin{bmatrix} \tfrac{2-\sqrt2}{4} \\ -\tfrac{1+2\sqrt2}{4} \\ 1\end{bmatrix},
$$
so $Q = \begin{bmatrix}v_1 & v_2 & v_3\end{bmatrix}$, and inverting (e.g. by cofactor expansion) gives
$$
Q^{-1} = \frac{1}{17}\begin{bmatrix} 8 & 4 & 5 \\ -5\sqrt2-4 & 6\sqrt2-2 & -2+6\sqrt2 \\ 5\sqrt2-4 & -6\sqrt2-2 & 2+6\sqrt2 \end{bmatrix}.
$$

**Step 3 — take the limit.** Since only the $\lambda_1 = 1$ term survives,
$$
\lim_{n\to\infty}A^n = Q\begin{bmatrix}1&0&0\\0&0&0\\0&0&0\end{bmatrix}Q^{-1} = \begin{bmatrix} 8/17 & 4/17 & 5/17 \\ 8/17 & 4/17 & 5/17 \\ 8/17 & 4/17 & 5/17 \end{bmatrix}.
$$
So $\pi = (8/17, 4/17, 5/17) \approx (0.471, 0.235, 0.294)$ — matching the direct solution of $\pi = \pi A$, $\sum_i \pi_i = 1$, and confirming the chain is ergodic (all states recurrent, none periodic).

### Cross-check: solving $\pi = \pi P$ directly
The same $\pi$ can be found without eigen-decomposition by solving the linear system $\pi_1 = 0.75\pi_2 + 1.00\pi_3$, $\pi_2 = 0.50\pi_1$, $\pi_3 = 0.50\pi_1 + 0.25\pi_2$, together with $\pi_1+\pi_2+\pi_3=1$ — the course uses both routes interchangeably, and the spectral method is preferred specifically when the *rate* of convergence (via $|\lambda_2|$) or the full matrix $\lim_n A^n$ (not just $\pi$) is also wanted.

## See also
[[Ergodic Markov Chain]], [[Stationary Distribution]], [[Equilibrium Distribution]], [[Mean Recurrence Time]], [[Transition Matrix]]
