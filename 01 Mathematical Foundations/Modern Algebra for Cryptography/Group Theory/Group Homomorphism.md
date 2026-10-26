---
title: "Group Homomorphism"
domain: "Mathematical Foundations"
course: "Modern Algebra for Cryptography"
unit: "Group Theory"
level: BSc
status: drafted
confidence: 0
tags: [abstract-algebra, group-theory, cryptography]
---
## Definition
Let $G,H$ be groups. A map $\phi: G \to H$ is a **group homomorphism** if it preserves the operation:
$$
\phi(a\cdot b) = \phi(a)\cdot\phi(b) \quad \text{for all } a,b\in G.
$$
A homomorphism that is also a bijection is an **isomorphism**, written $G \cong H$; two isomorphic groups are structurally identical (same multiplication table, up to relabeling).

## Properties
### Homomorphisms send the identity to the identity
$\phi(e_G\cdot e_G) = \phi(e_G)\cdot\phi(e_G)$, i.e. $\phi(e_G)=\phi(e_G)\phi(e_G)$. Left-cancelling $\phi(e_G)$ in $H$ (multiply both sides by $\phi(e_G)^{-1}$) gives $e_H = \phi(e_G)$.

### Homomorphisms send powers to powers
By induction on $k$ using the defining property: $\phi(a^k) = \phi(a)^k$ for all $k \in \mathbb{Z}$ (the base case $k=1$ is trivial, $k=0$ follows from the identity property, and negative $k$ follows since $\phi(a^{-1}) = \phi(a)^{-1}$, itself a consequence of $\phi(a)\phi(a^{-1})=\phi(aa^{-1})=\phi(e)=e$).

### Isomorphisms preserve order
An immediate corollary of the previous property plus injectivity — see the full argument in [[Order of an Element]] (proved there for the special case of an [[Automorphism]], which is the same argument for any injective homomorphism).

### $H=\{g\in G : \alpha(g)=\beta(g)\}$ is a subgroup, for isomorphisms $\alpha,\beta: G\to G$
**Proof** (Ejercicios Módulo I, Problem 15). $H\ne\emptyset$ since $\alpha(e)=e=\beta(e)$. For $a,b\in H$: $\alpha(ab^{-1}) = \alpha(a)\alpha(b)^{-1} = \beta(a)\beta(b)^{-1} = \beta(ab^{-1})$, using $\alpha(a)=\beta(a)$, $\alpha(b)=\beta(b)$, and that homomorphisms send inverses to inverses. So $ab^{-1}\in H$, and by the [[Subgroup|one-step subgroup test]], $H\le G$. $\blacksquare$

## Examples
- The isomorphism $(\mathbb{Z}/n\mathbb{Z})^* \cong (\mathbb{Z}/p\mathbb{Z})^*\times(\mathbb{Z}/q\mathbb{Z})^*$ used in [[RSA Cryptosystem]] (see [[Direct Product of Groups]]).
- $\mathrm{Aut}(\mathbb{Z}_{20}) \cong \{1,9,13,17\}\le U(20)$ via $f(\alpha_n)=n$ — see [[Automorphism]].
- The map $k \mapsto kP$ from $(\mathbb{Z}, +)$ to the point group of an elliptic curve (restricted to $\{0,1,\dots,n-1\}$ for $n=|P|$) is a group isomorphism onto $\langle P\rangle$ — the structural reason [[ECDH]] mirrors [[Diffie-Hellman Key Exchange]] exactly.

## See also
[[Group (Definition)]], [[Automorphism]], [[Order of an Element]], [[Direct Product of Groups]]
