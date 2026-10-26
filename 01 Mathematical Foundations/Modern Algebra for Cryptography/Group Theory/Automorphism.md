---
title: "Automorphism"
domain: "Mathematical Foundations"
course: "Modern Algebra for Cryptography"
unit: "Group Theory"
level: BSc
status: drafted
confidence: 0
tags: [abstract-algebra, group-theory, cryptography]
---
## Definition
An **automorphism** of a group $G$ is a [[Group Homomorphism|group isomorphism]] $\phi: G \to G$ from $G$ to itself. The set of all automorphisms of $G$, denoted $\mathrm{Aut}(G)$, is itself a group under composition.

## Properties
### $\mathrm{Aut}(\mathbb{Z}_n) \cong U(n)$
For $\mathbb{Z}_n = \langle 1\rangle$ cyclic, any automorphism $\phi$ is determined by where it sends the generator $1$: $\phi(k) = k\cdot\phi(1) \bmod n$ for all $k$. For $\phi$ to be a bijection, $\phi(1)$ must itself generate $\mathbb{Z}_n$, i.e. $\gcd(\phi(1),n)=1$. So automorphisms of $\mathbb{Z}_n$ correspond exactly to elements of $U(n)$, via $\alpha_m(x) := mx \bmod n \leftrightarrow m \in U(n)$, and composition of automorphisms corresponds to multiplication in $U(n)$: $\alpha_m\circ\alpha_{m'}(x) = m(m'x) = (mm')x = \alpha_{mm'}(x)$.

### Worked example: automorphisms of $\mathbb{Z}_{20}$ fixing $\phi(5)=5$
**(Tarea II Gran Final, Problem 9.)** The generators of $\mathbb{Z}_{20}$ are $U(20)=\{1,3,7,9,11,13,17,19\}$, each giving an automorphism $\alpha_m(x)=mx\bmod20$. Checking $\alpha_m(5) = 5m \bmod 20$ against each $m$:
$$
\alpha_1(5)=5,\quad \alpha_3(5)=15,\quad \alpha_7(5)=15,\quad \alpha_9(5)=5,
$$
$$
\alpha_{11}(5)=15,\quad \alpha_{13}(5)=5,\quad \alpha_{17}(5)=5,\quad \alpha_{19}(5)=15.
$$
So $\phi(5)=5$ forces $\phi \in \{\alpha_1,\alpha_9,\alpha_{13},\alpha_{17}\}$. This subset is closed under composition (its Cayley table only involves these four maps), forms a subgroup of $\mathrm{Aut}(\mathbb{Z}_{20})$, and is isomorphic to $\{1,9,13,17\} \le U(20)$ via $f(\alpha_n)=n$:

| $\mathrm{Aut}(\mathbb{Z}_{20})$ | $\alpha_1$ | $\alpha_9$ | $\alpha_{13}$ | $\alpha_{17}$ |
|---|---|---|---|---|
| $\alpha_1$ | $\alpha_1$ | $\alpha_9$ | $\alpha_{13}$ | $\alpha_{17}$ |
| $\alpha_9$ | $\alpha_9$ | $\alpha_1$ | $\alpha_{17}$ | $\alpha_{13}$ |
| $\alpha_{13}$ | $\alpha_{13}$ | $\alpha_{17}$ | $\alpha_9$ | $\alpha_1$ |
| $\alpha_{17}$ | $\alpha_{17}$ | $\alpha_{13}$ | $\alpha_1$ | $\alpha_9$ |

(products taken as $\alpha_m\circ\alpha_{m'} = \alpha_{mm' \bmod 20}$).

### Automorphisms preserve the order of every element
Proved in full in [[Order of an Element]] (an automorphism is, in particular, an injective homomorphism, so the argument there applies directly).

## Examples
- $\mathrm{Aut}(U(n))$ can itself be studied the same way for small $n$, though this course only develops $\mathrm{Aut}(\mathbb{Z}_n)$ explicitly.
- The correspondence $\mathrm{Aut}(\mathbb{Z}_n)\cong U(n)$ is a small-scale preview of the same "which maps preserve structure" question that underlies choosing a valid generator $g$ for [[Diffie-Hellman Key Exchange]].

## See also
[[Group Homomorphism]], [[Order of an Element]], [[Group of Units U(n)]], [[Cyclic Group]]
