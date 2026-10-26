---
title: "Hashing Tables"
domain: "Computer Science & Data Engineering"
course: "Data Structures and Algorithms"
unit: "Hashing"
level: BSc
status: drafted
confidence: 0
tags: [data-structures-algorithms]
---
A hashing table consists of:
1. A hashing function that transforms keys to indexes
2. A list of buckets that contains the entries we wish to store.

Resolving collisions by keeping a list per index is called **separate chaining**. Compare with [[Dictionary]], which uses **open addressing** (one entry per slot, probe on collision).

Example: for list $L = [9, 43, 58, 71, 22, 94, 72, 4]$ and a hashing function $\mod 8$, we have. 
$$ \matrix{ 
	\text{Index} & \text{Bucket} \\ 
	0 & [72] \\ 
	1 & [9] \\ 
	2 & [58] \\ 
	3 & [43] \\ 
	4 & [4] \\ 
	5 & [] \\
	6 & [22, 94] \\ 
	7 & [71] 
}$$
 Example: Let $L = [0, 8, 16, 24, 32, 40, 48, 56]$. To construct the corresponding hashing function using $\mod 8$: $$ \matrix{
	\text{Index} & \text{Bucket} \\ 
	0 & [0,8,16,24,32,40,48,56] \\ 
	1 & [] \\
	2 & [] \\ 
	3 & [] \\ 
	4 & [] \\ 
	5 & [] \\ 
	6 & [] \\ 
	7 & []
}$$
This hashing function is useless **for this input**: every key is $\equiv 0 \pmod 8$, so everything lands in one bucket and lookup degrades to $O(n)$. Any fixed hash function has some input set like this. That is the motivation for choosing the function at random from a family.

**[[Universal Hashing]]**: for a prime $p \geq |U|$ (universe of keys), the family $$H = { h_{a,b}(x) = ((ax + b) \bmod p) \bmod m ;:; a \in {1,\dots,p-1},\ b \in {0,\dots,p-1} }$$ is universal: for any $x \neq y$, $\Pr_{a,b}[h_{a,b}(x) = h_{a,b}(y)] \leq \tfrac{1}{m}$. The theorem bounds the _expected_ number of collisions; it does not guarantee zero collisions for a particular $(a,b)$.

Taking $p = 71$ (prime, $\geq 57$), $a = 9$, $b = 1$, i.e. $h(x) = ((9x + 1) \bmod 71) \bmod 8$, we have 
$$ \matrix{ 
	\text{Index} & \text{Bucket} \\
	0 & [56] \\ 
	1 & [0] \\ 
	2 & [8] \\ 
	3 & [16] \\ 
	4 & [24] \\ 
	5 & [32] \\ 
	6 & [40] \\ 
	7 & [48] 
}$$
 This particular choice happens to be perfect (no collisions) on this set.