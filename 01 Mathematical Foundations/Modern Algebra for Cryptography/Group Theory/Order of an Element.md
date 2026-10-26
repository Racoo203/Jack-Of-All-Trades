---
title: "Order of an Element"
domain: "Mathematical Foundations"
course: "Modern Algebra for Cryptography"
unit: "Group Theory"
level: BSc
status: drafted
confidence: 0
tags: [abstract-algebra, group-theory, cryptography]
---
## Definition
Let $G$ be a group and $g\in G$. The **order** of $g$, written $|g|$, is the smallest positive integer $n$ such that $g^n = e$, if such $n$ exists; otherwise $g$ has **infinite order**. (Here $g^n$ means $g$ combined with itself $n$ times under the group operation.)

## Properties
### $|ab| = |ba|$ for any $a,b \in G$
**Proof** (`Tarea II.pdf`, Problem 2). Let $n = |ab|$ and $m = |ba|$ (assume both finite). From $(ab)^n = e$:
$$
(ab)^{n+1} = ab, \qquad (ab)^{n+1} = a(ba)^n b,
$$
(the second identity because $(ab)^{n+1} = a\,\underbrace{(ba)(ba)\cdots(ba)}_{n}\,b$, regrouping the alternating product). Equating,
$$
a(ba)^nb = ab \;\Rightarrow\; (ba)^n = e
$$
(cancelling $a$ on the left and $b$ on the right). Since $m=|ba|$ is the *smallest* such exponent, $m \mid n$, so $m\le n$. By the symmetric argument starting from $(ba)^m=e$, $n\mid m$, so $n \le m$. Hence $n=m$, i.e. $|ab|=|ba|$. $\blacksquare$

### Consequence: $|abab| = |baba|$
Let $c = aba \in G$. Then $|abab| = |(aba)b| = |cb|$. By the property above, $|cb|=|bc| = |b(aba)| = |baba|$. $\blacksquare$

### In general $|aba| \ne |bab|$
A single counterexample suffices. In $U(16) = \{1,3,5,7,9,11,13,15\}$, $|3|=4$ and $|7|=2$ (check: $3^2=9,\ 3^4=81\equiv1$; $7^2=49\equiv1$). Computing directly,
$$
3\cdot7\cdot3 \equiv 63 \equiv 15 \pmod{16}, \qquad 7\cdot3\cdot7 \equiv 147 \equiv 3 \pmod{16}.
$$
$|15|=2$ (since $15\equiv-1$) while $|3|=4$, so $|aba|=2 \ne 4 = |bab|$ here — the statement is false in general.

### Automorphisms preserve order
**Proof** (`Tarea II.pdf`, Problem 8). Let $\phi:G\to G$ be an [[Automorphism]] and $a\in G$ with $n=|a|$. Since $\phi$ is a homomorphism, $\phi(e)=e$ (from $\phi(e\cdot e)=\phi(e)\phi(e) \Rightarrow \phi(e)=e$ after cancelling), and $\phi(a^k) = \phi(a)^k$ by induction. Then $\phi(a)^n = \phi(a^n) = \phi(e) = e$, so $|\phi(a)| \le n$. If $|\phi(a)|=m<n$, then $\phi(a)^m=e=\phi(e)$, so $\phi(a^m)=\phi(e)$; since $\phi$ is injective, $a^m=e$ with $m<n$, contradicting that $n=|a|$ is minimal. Hence $|\phi(a)|=|a|$. $\blacksquare$

## Examples
- In $U(20)$, $\alpha_n(x) := nx \bmod 20$ defines an [[Automorphism]] for each generator $n$; matching $\alpha_n(5)=5$ picks out exactly the elements $n\in\{1,9,13,17\}$, itself a subgroup of $U(20)$.
- The security of [[Diffie-Hellman Key Exchange]] and [[ElGamal Encryption]] depends on choosing a generator (or a point, in [[ECDH]]) of large order, so that the [[Discrete Logarithm Problem]] has a large search space.

## See also
[[Group (Definition)]], [[Cyclic Group]], [[Group Homomorphism]], [[Automorphism]], [[Fermat-Euler Theorem]]
