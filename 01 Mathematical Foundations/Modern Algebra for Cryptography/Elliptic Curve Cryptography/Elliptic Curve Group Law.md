---
title: "Elliptic Curve Group Law"
domain: "Mathematical Foundations"
course: "Modern Algebra for Cryptography"
unit: "Elliptic Curve Cryptography"
level: BSc
status: drafted
confidence: 0
tags: [cryptography, elliptic-curves, number-theory, group-theory]
---
## Definition
For $E: y^2=x^3+c_1x+c_0 \pmod p$ (see [[Elliptic Curve over a Finite Field]]) and points $P=(x_1,y_1),\, Q=(x_2,y_2) \in E$ with $x_1 \ne x_2$, define **point addition**:
$$
P+Q = (\hat x,\hat y), \qquad \lambda = \frac{y_2-y_1}{x_2-x_1} = (y_2-y_1)(x_2-x_1)^{-1} \bmod p,
$$
$$
\hat x = \lambda^2 - x_1 - x_2 \bmod p, \qquad \hat y = \lambda(x_1-\hat x) - y_1 \bmod p.
$$
**Point doubling** ($P=Q$, i.e. $2P$):
$$
2P = (\hat x,\hat y), \qquad \mu = \frac{3x_1^2+c_1}{2y_1} = (3x_1^2+c_1)(2y_1)^{-1} \bmod p,
$$
$$
\hat x = \mu^2 - 2x_1 \bmod p, \qquad \hat y = \mu(x_1-\hat x) - y_1 \bmod p.
$$
**Negation**: $-P = (x_1,-y_1)$. **Identity**: the point at infinity $\mathcal{O}$, with $P + \mathcal{O} = P$ and $P+(-P)=\mathcal{O}$ for every $P$ (the case $x_1=x_2,\,y_1=-y_2$ not covered by the addition formula above).

## Properties
### Why $\lambda,\mu$ are slopes
$\lambda$ is the slope of the secant line through $P$ and $Q$; $\mu$ is the slope of the tangent line to $E$ at $P$, obtained by implicit differentiation of $y^2=x^3+c_1x+c_0$: $2y\,dy = (3x^2+c_1)\,dx \Rightarrow dy/dx = (3x^2+c_1)/(2y)$. Geometrically, $P+Q$ (resp. $2P$) is defined as $-R$, where $R$ is the third intersection point of the secant (resp. tangent) line with $E$ — reflecting across the $x$-axis is exactly the negation $(\hat x,\hat y)\mapsto(\hat x,-\hat y)$ built into the formulas above.

### The point group is Abelian
Addition is manifestly symmetric in $P,Q$ up to the sign of $\lambda$'s numerator and denominator (both flip together), so $P+Q=Q+P$; associativity is a deeper fact (provable via the divisor-class-group interpretation of the curve, beyond this course's scope) that is assumed/used throughout. Together with the identity $\mathcal{O}$ and inverses $-P$, this makes $(E,+)$ an Abelian group.

### Scalar multiplication by repeated doubling
$kP$ (for $k\in\mathbb{Z}^+$) is computed efficiently via the binary expansion of $k$, doubling and adding — exactly [[Congruence Relation|repeated squaring]] transported to additive notation.

**Worked example** (`A01722401_Actividad_Criptografía_Elíptica.pdf`): computing $A=5G$ for $G=(6,4)$ on $E:y^2=x^3+x+1 \pmod{23}$. Writing $5 = 2^2+2^0$, first compute $2G$ (doubling) and $4G=2(2G)$, then $A = G + 4G$ (addition):
$$
2G = (13,7), \qquad 4G=(5,4), \qquad A = G+4G = (6,4)+(5,4) = (12,19).
$$

## Examples
- $P+Q$ and $2P$ for $E:y^2=x^3+2x+3 \pmod{13}$, $P=(3,6)$, $Q=(4,7)$: $\lambda = (7-6)/(4-3)=1 \Rightarrow P+Q=(7,3)$; $\mu = (3\cdot9+2)/12 \equiv 3\cdot12^{-1} \equiv 3\cdot12 \equiv 10 \pmod{13} \Rightarrow 2P = (3,7)$ (`A01722401_Actividad_Criptografía_Elíptica.pdf`).
- This group law is exactly what [[ECDH]] and [[ECDSA]] build on, replacing $g^k \bmod p$ everywhere with $kP$.

## See also
[[Elliptic Curve over a Finite Field]], [[Modular Inverse]], [[Group (Definition)]], [[Elliptic Curve Discrete Logarithm Problem]]
