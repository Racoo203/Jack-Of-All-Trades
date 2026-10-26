---
title: "Group (Definition)"
domain: "Mathematical Foundations"
course: "Modern Algebra for Cryptography"
unit: "Group Theory"
level: BSc
status: drafted
confidence: 0
tags: [abstract-algebra, group-theory, cryptography]
---
## Definition
A **group** is a pair $(G, \cdot)$, a set $G$ with a binary operation $\cdot: G\times G \to G$, satisfying:

1. **Closure**: $a\cdot b \in G$ for all $a,b\in G$.
2. **Associativity**: $(a\cdot b)\cdot c = a\cdot(b\cdot c)$ for all $a,b,c\in G$.
3. **Identity**: there exists $e\in G$ with $e\cdot a = a\cdot e = a$ for all $a \in G$.
4. **Inverses**: for every $a\in G$ there exists $a^{-1}\in G$ with $a\cdot a^{-1} = a^{-1}\cdot a = e$.

$G$ is **Abelian** (commutative) if additionally $a\cdot b = b\cdot a$ for all $a,b\in G$.

## Properties
### Uniqueness of the identity and of inverses
If $e,e'$ are both identities, $e = e\cdot e' = e'$. If $b,c$ are both inverses of $a$, then $b = b\cdot e = b\cdot(a\cdot c) = (b\cdot a)\cdot c = e\cdot c = c$. So $e$ and $a^{-1}$ are well defined.

### $(ab)^{-1} = b^{-1}a^{-1}$ in general
$(ab)(b^{-1}a^{-1}) = a(bb^{-1})a^{-1} = a\cdot e\cdot a^{-1} = aa^{-1} = e$, and similarly on the other side, so $b^{-1}a^{-1}$ is the inverse of $ab$.

### $G$ is Abelian $\iff (a\cdot b)^{-1} = a^{-1}\cdot b^{-1}$ for all $a,b\in G$
**Proof** (`Tarea II.pdf`, Problem 1). ($\Rightarrow$) If $G$ is Abelian, $(ab)^{-1}=b^{-1}a^{-1} = a^{-1}b^{-1}$ by commutativity.

($\Leftarrow$) Suppose $(a\cdot b)^{-1} = a^{-1}\cdot b^{-1}$ for all $a,b$. Starting from the Abelian property to be shown, work forward from the hypothesis:
$$
(a\cdot b)(a\cdot b)^{-1} = e \;\Rightarrow\; (a\cdot b)(a^{-1}\cdot b^{-1}) = e.
$$
Left-multiply both sides by $(a\cdot b)^{-1}$... equivalently, since $(ab)^{-1}$ is always $b^{-1}a^{-1}$ (shown above) *and* by hypothesis it also equals $a^{-1}b^{-1}$, the two expressions for the same element must agree:
$$
b^{-1}a^{-1} = a^{-1}b^{-1}.
$$
Taking inverses of both sides (and using $(xy)^{-1}=y^{-1}x^{-1}$ again) gives $ab = ba$. Hence $G$ is Abelian. $\blacksquare$

## Examples
- $\left(\mathbb{Z}/n\mathbb{Z}, +\right)$ and the [[Group of Units U(n)]] $\left(\mathbb{Z}/n\mathbb{Z}\right)^*$ under multiplication — both Abelian.
- The [[Symmetric Group]] $S_n$ for $n\ge3$ — the standard example of a non-Abelian group.
- The points of an elliptic curve over a finite field under the chord-and-tangent [[Elliptic Curve Group Law]] — Abelian, which is why Diffie–Hellman-style protocols ([[ECDH]]) carry over unchanged from $U(p)$.

## See also
[[Subgroup]], [[Cyclic Group]], [[Group of Units U(n)]], [[Symmetric Group]], [[Order of an Element]]
