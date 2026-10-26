---
title: "Routh-Hurwitz Criterion"
domain: "Optimization & Control"
course: "Non-linear Optimization"
unit: "Transient Response and Stability"
level: BSc
status: drafted
confidence: 0
tags: [control-theory, stability, ma2008b, exam]
---
## Definition
Let $D(s)=a_0s^n+a_1s^{n-1}+\dots+a_{n-1}s+a_n$ ($a_0>0$) be the characteristic polynomial of a closed loop (see [[BIBO Stability and Pole Location]]). The **Routh array** has one row per power $s^n,s^{n-1},\dots,s^0$:
$$\begin{array}{c|cccc}
s^n & a_0 & a_2 & a_4 & \cdots\\
s^{n-1} & a_1 & a_3 & a_5 & \cdots\\
s^{n-2} & b_1 & b_2 & b_3 & \cdots\\
s^{n-3} & c_1 & c_2 & \cdots\\
\vdots & \vdots\\
s^0 & *
\end{array}
\qquad
b_1=\frac{a_1a_2-a_0a_3}{a_1}=-\frac{1}{a_1}\begin{vmatrix}a_0&a_2\\a_1&a_3\end{vmatrix},\quad
b_2=\frac{a_1a_4-a_0a_5}{a_1},$$
$$c_1=\frac{b_1a_3-a_1b_2}{b_1},\quad c_2=\frac{b_1a_5-a_1b_3}{b_1},\;\dots$$
Each new entry is minus the $2\times2$ determinant formed by the first column ("pivot") and the next column of the two rows above, divided by the pivot. Missing entries are $0$. A row may be multiplied by a **positive** constant to simplify arithmetic.

**Routh's criterion.** The number of roots of $D(s)$ with positive real part equals the **number of sign changes in the first column**. Consequently (necessary and sufficient): the system is stable iff **all first-column entries are positive** (given $a_0>0$).

## Properties
### Why it works (sketch)
The array is the Euclidean-type algorithm applied to the even and odd parts $E(s)=a_0s^n+a_2s^{n-2}+\dots$ and $O(s)=a_1s^{n-1}+a_3s^{n-3}+\dots$ of $D$. Each row step is polynomial division $E=q\,O+R$ with $q=\frac{a_0}{a_1}s$, and the remainder's coefficients are the next row. The ratio $O/E$ evaluated along $s=j\omega$ is a real rational function, and the Cauchy-index / argument-principle count (the same argument that underlies the [[Nyquist Stability Criterion]]) shows the number of RHP roots equals the number of sign variations in the sequence of leading coefficients. The full proof is in Gantmacher; for the course, the criterion is applied, not proved.
<!-- Proof sketch is canonical, not covered in slides. -->

### Necessary condition first
Before building the array, check that all coefficients are present and positive; if not, the system is already not (asymptotically) stable. This test is necessary but not sufficient.

### Special case 1 — zero in the first column only
Replace the $0$ by a small $\varepsilon>0$, continue, and let $\varepsilon\to0^+$ when counting signs.

*Example (slides):* $D(s)=s^5+3s^4+2s^3+6s^2+6s+9$.
$$\begin{array}{c|ccc}
s^5&1&2&6\\ s^4&3&6&9\\ s^3&0\to\varepsilon&3&0\\ s^2&\dfrac{6\varepsilon-9}{\varepsilon}&9&\\ s^1&\dfrac{18\varepsilon-27-9\varepsilon^2}{6\varepsilon-9}&0&\\ s^0&9&&
\end{array}$$
As $\varepsilon\to0^+$: $s^2$ entry $\to-\infty$ and $s^1$ entry $\to3$. First column signs $+,+,+,-,+,+$ → **two** sign changes → two RHP roots (numerically $0.6567\pm1.2881j$). Unstable.

### Special case 2 — an entire row of zeros
A zero row appears when $D$ has roots symmetric about the origin (e.g. $\pm j\omega$ pairs). Form the **auxiliary polynomial** $P(s)$ from the row just above (starting at that row's power of $s$ and skipping every other power), replace the zero row with the coefficients of $P'(s)$, and continue. The roots of $P(s)$ are also roots of $D(s)$.

*Example (slides):* $D(s)=s^5+5s^4+11s^3+23s^2+28s+12$.
$$\begin{array}{c|ccc}
s^5&1&11&28\\ s^4&5&23&12\\ s^3&6.4&25.6&\\ s^2&3&12&\\ s^1&0\to6&0&\\ s^0&12&&
\end{array}$$
$s^3$: $\frac{5\cdot11-23}{5}=6.4$, $\frac{5\cdot28-12}{5}=25.6$; $s^2$: $\frac{6.4\cdot23-5\cdot25.6}{6.4}=3$, $12$; $s^1$: $\frac{3\cdot25.6-6.4\cdot12}{3}=0$ → zero row. $P(s)=3s^2+12$, $P'(s)=6s$. No sign changes, but $P(s)=0\Rightarrow s=\pm2j$ are roots of $D$: **marginally stable** (roots $-3,-1,-1,\pm2j$).

### Designing a gain with Routh
The criterion is most useful when a coefficient depends on a parameter $K$: require every first-column entry to be positive and intersect the resulting inequalities.

## Examples
**Tarea 2 (a).** $s^5+2s^4+6s^3+48s^2+8s+160$.
Rows: $s^5:1,6,8$; $s^4:2,48,160$; $s^3:\frac{12-48}{2}=-18,\ \frac{16-160}{2}=-72$; $s^2:\frac{(-18)(48)-2(-72)}{-18}=40,\ 160$; $s^1:\frac{40(-72)-(-18)(160)}{40}=0$ → zero row, $P=40s^2+160$, $P'=80s$ → $s^1:80$; $s^0:160$.
First column $1,2,-18,40,80,160$: **two sign changes** → two RHP roots; plus $P=0\Rightarrow\pm2j$. Unstable (roots $-4,\ 1\pm3j,\ \pm2j$).

**Tarea 2 (b).** $s^5+7s^4+6s^3+42s^2+8s+56$. The $s^4$ row $7,42,56$ is $7\times$ the $s^5$ row $1,6,8$, so the $s^3$ row is zero immediately. $P=7s^4+42s^2+56$, $P'=28s^3+84s$:
$s^3:28,84$; $s^2:\frac{28\cdot42-7\cdot84}{28}=21,\ 56$; $s^1:\frac{21\cdot84-28\cdot56}{21}=\frac{28}{3}$; $s^0:56$. No sign changes; $P=0\Rightarrow s^2=-2,-4$, i.e. simple roots $\pm j\sqrt2,\pm2j$ → **marginally stable** (remaining root $-7$).

**Two sign changes (slides).** $s^6+4s^5+3s^4+2s^3+s^2+4s+4$: first column $1,4,\tfrac52,2,3,-\tfrac{76}{15},4$ → two RHP roots ($0.7797\pm0.7488j$).

**Range of $K$ (Ogata, slides Ejemplo 1).** Unity feedback around $\frac{K}{s(s^2+s+1)(s+2)}$: $D(s)=s^4+3s^3+3s^2+2s+K$.
$$s^4:1,3,K;\quad s^3:3,2;\quad s^2:\tfrac73,K;\quad s^1:2-\tfrac97K;\quad s^0:K.$$
Stability ⇔ $K>0$ and $2-\frac97K>0$ ⇔ $\boxed{0<K<\tfrac{14}{9}}$.

**Unstable plant stabilized by P control (slides Ejemplo 2).** Plant $\frac{s+1}{s(s-1)(s+6)}$, controller $K$: $D=s^3+5s^2+(K-6)s+K$. Rows $1,K-6$; $5,K$; $\frac{4K-30}{5}$; $K$ ⇒ $K>7.5$.

**No $K$ works (Ogata A-5-8, Ejemplo 3).** $s^4+Ks^3+s^2+s+1$: rows $1,1,1$; $K,1$; $\frac{K-1}{K},1$; $1-\frac{K^2}{K-1}$; $1$. Need $K>1$ and $\frac{K-1-K^2}{K-1}>0$, i.e. $K^2-K+1<0$, impossible (discriminant $-3$). Unstable for every $K$.

**Practice (joystick positioner).** $G=\dfrac{s+0.6}{s^4+6.1s^3+11.6s^2+7.1s+0.6}$ with gain $k$: $D=s^4+6.1s^3+11.6s^2+(7.1+k)s+0.6(1+k)$. Working the array numerically gives stability for $-1<k\lesssim44.0$ (so $0<k<44$ for a positive gain).

## See also
[[BIBO Stability and Pole Location]], [[Root Locus]], [[Root Locus Construction Rules]] (the $j\omega$ crossing uses the same computation), [[PID Controller]], [[Nyquist Stability Criterion]]
