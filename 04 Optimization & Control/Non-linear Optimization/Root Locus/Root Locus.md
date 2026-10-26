---
title: "Root Locus"
domain: "Optimization & Control"
course: "Non-linear Optimization"
unit: "Root Locus"
level: BSc
status: drafted
confidence: 0
tags: [control-theory, root-locus, ma2008b, exam]
---
## Definition
Given an open-loop transfer function $G(s)$ and feedback $H(s)$, the closed-loop transfer function is $G_{CL}(s)=\dfrac{G(s)}{1+G(s)H(s)}$ (see [[Control System Fundamentals]]). The **root locus** (Evans, 1948) is the set of all points $s\in\mathbb C$ that satisfy the characteristic equation
$$1+KG(s)H(s)=0$$
for some gain $0\le K<\infty$ — i.e. the geometric locus of the closed-loop poles as $K$ varies, drawn from the open-loop poles and zeros alone.

Writing $G(s)H(s)=\dfrac{\prod_{j=1}^m(s-z_j)}{\prod_{i=1}^n(s-p_i)}$, a point $s$ lies on the locus iff
$$\textbf{angle condition:}\quad \angle G(s)H(s)=\sum_j\angle(s-z_j)-\sum_i\angle(s-p_i)=\pm180°(2N+1),\;N=0,1,2,\dots$$
$$\textbf{magnitude condition:}\quad |KG(s)H(s)|=1\;\Longleftrightarrow\;K=\frac{\prod_i|s-p_i|}{\prod_j|s-z_j|}.$$
The angle condition decides *membership*; the magnitude condition then gives the *gain* at that point.

## Properties
### Why: moving poles by feedback (slides' motivation)
The plant $\frac{1}{s(s+2)}$ has poles $0,-2$; its step response $y=\frac14(e^{-2t}-1+2t)$ grows without bound. Changing the plant is often impossible, but feedback moves the poles:
- unity feedback: $\dfrac{1}{s^2+2s+1}$, poles $-1,-1$ (critically damped);
- with a gain $K$ in the loop: $\dfrac{K}{s^2+2s+K}$, poles $s_{1,2}=-1\pm\sqrt{1-K}$.

| $K$ | poles |
|---|---|
| 0 | $0,\,-2$ |
| 0.5 | $-0.293,\,-1.707$ |
| 1 | $-1,\,-1$ |
| 2 | $-1\pm j$ |
| 5 | $-1\pm 2j$ |
| 10 | $-1\pm 3j$ |

The poles start at the open-loop poles, meet at the **breakaway point** $-1$ when $K=1$, then move vertically along $\operatorname{Re}s=-1$: overdamped → critically damped → underdamped with constant settling time $4/\sigma=4$ s.

### Derivation of the conditions
$1+KGH=0\iff KG(s)H(s)=-1=1\angle(\pm180°(2N+1))$. Since $K>0$ is real, $\angle K=0$, which gives the angle condition; taking moduli gives the magnitude condition. The angle of a product/quotient is the sum/difference of the angles of the factors, so the angle can be read geometrically as (angles of vectors from zeros to $s$) − (angles of vectors from poles to $s$).

### Endpoints
From $K=-1/(G(s)H(s))$: as $K\to0$, $s\to$ open-loop poles; as $K\to\infty$, $s\to$ open-loop zeros. If $n>m$, $GH\to0$ as $s\to\infty$, so there are $n-m$ "zeros at infinity", reached along asymptotes. There are $n$ branches, symmetric about the real axis.

### Construction
See [[Root Locus Construction Rules]].

## Examples
**Is $s_0=-1+2j$ on the locus of $G(s)=\dfrac{K(s+1)}{s[(s+2)^2+4](s+5)}$?** (slides)
Open-loop poles $0,\,-2\pm2j,\,-5$; zero $-1$. Angles of vectors to $s_0$:
- zero $-1$: $s_0+1=2j$ → $\theta_1=90°$;
- pole $0$: $-1+2j$ → $180°-63.43°=116.57°$;
- pole $-2+2j$: $1+0j$ → $0°$;
- pole $-2-2j$: $1+4j$ → $75.96°$;
- pole $-5$: $4+2j$ → $26.57°$.
$$\angle G(s_0)=90°-116.57°-0°-75.96°-26.57°=-129.1°\neq\pm180°,$$
so $s_0$ is **not** on the root locus. (Direct evaluation: $G(s_0)/K=\frac{2j}{(-1+2j)(1+4j)(4+2j)}=0.0485\angle-129.08°$.)

## See also
[[Root Locus Construction Rules]], [[BIBO Stability and Pole Location]], [[Routh-Hurwitz Criterion]], [[PID Controller]], [[Second-Order System Response]], [[Frequency Response]]
