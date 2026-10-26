---
title: "Universal Hashing"
domain: "Computer Science & Data Engineering"
course: "Data Structures and Algorithms"
unit: "Hashing"
level: BSc
status: seeding
confidence: 0
tags: [data-structures-algorithms]
---
Let $m>0$ and $p$ a prime number such that $p>m$. Given integers $a,b$, define $h_{a,b}(x) = (ax+b \mod p) \mod m$. Then, if $x \neq y$, 
$$
P(h_{a,b}(x)=h_{a,b}(y)) = \frac{1}{m}
$$
Proof: ...