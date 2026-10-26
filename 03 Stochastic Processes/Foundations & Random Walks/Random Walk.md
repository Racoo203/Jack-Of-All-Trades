---
title: Random Walk
domain: Stochastic Processes
course: Stochastic Processes
unit: Foundations & Random Walks
level: MSc
status: seeding
confidence: 0
tags: [seeding]
---
## Definition
A random walk is a [[Stochastic Process]] $\{S_n, n \in T\}$, defined such that
$$
S_n = S_0 + \sum_{t=1}^{n} X_t
$$
where $S_0$ is a constant and the set of [[Random Variable|random variables]] $\{X_t\}$ are [[Independent and Identically Distributed (i.i.d)|i.i.d]] for all $t$.
## Properties
### Transition Probabilities
Suppose $\{S_n, n\in \mathbb{N}\}$ is a [[Stochastic Process|stochastic process]]. The (1-step) transition probability of $\{S_n\}$ transiting from state $i$ into state $j$ is defined as the conditional probability $Pr(S_{n+1} = j | S_{n} = i )$. For a random walk, the transition probabilities are
$$
p_{ij}^{(1)} = Pr(S_{n+1} = j | S_{n} = i )
$$
for all $i,j \in S$ such that $i \neq j$.
### Spatial Homogeneity
In general, all random walks are [[Spatial Homogeneity|spatially homogenous]]. That is, the probability of reaching one state from another relies on the distance between states, and not the states themselves. Symbolically, $\forall n, m$ such that $\{n > m : n,m \in T\}$, and $\forall a,b,k \in \mathbb{Z}$ such that $Pr(S_m = a) \neq 0$ and $Pr(S_m = a + b) \neq 0$, then it follows that
$$
Pr(S_n = b | S_m = a) = Pr (S_n = b + k | S_m = a + k)
$$
To prove said statement, start by rewriting the left-hand side based on the definition of $S_n$.
$$
Pr\left(S_m + \sum_{t=m+1}^{n} X_t = b  \Bigg\vert  S_m = a \right)
$$
Since $S_m = a$, 
$$
Pr\left(\sum_{t=m+1}^{n} X_t = b - a  \Bigg\vert  S_m = a \right)
$$
Recall that all $X_t$ are [[Independent and Identically Distributed (i.i.d)|i.i.d]]. This implies that,
$$
Pr(S_n = b | S_m = a) = Pr\left(\sum_{t=m+1}^{n} X_t = b - a \right)
$$
Now, consider the right-hand side:
$$
Pr\left(S_m + \sum_{t=m+1}^{n} X_t = b + k  \Bigg\vert  S_m = a + k \right)
$$
Since $S_m = a + k$, 
$$
Pr\left(\sum_{t=m+1}^{n} X_t = (b + k) - (a + k)  \Bigg\vert  S_m = a + k \right)
$$
By the same logic, this implies that,
$$
Pr(S_n = b + k | S_m = a + k) = Pr\left(\sum_{t=m+1}^{n} X_t = b - a \right)
$$
Thus it is proven that both sides are equal, and therefore spatially homogeneous.
### Time Homogeneity
Likewise, all random walks are [[Time Homogeneity|time homogenous]]. That is, the probability of reaching one state from another relies on the distance over time, and not on the time steps themselves. Symbolically, $\forall n, m \in T$, and $\forall a,b \in \mathbb{Z}$, then it follows that
$$
Pr(S_n = b | S_0 = a) = Pr(S_{n+m} = b | S_{m} = a)
$$
To prove said property, starting by LHS:
$$
Pr\left(S_0 + \sum_{t=1}^{n}X_t = b \Bigg\vert S_0 = a\right)
$$
Since $S_0 = a$,
$$
Pr\left(\sum_{t=1}^{n}X_t = b - a \Bigg\vert S_0 = a\right)
$$Recall that all $X_t$ are [[Independent and Identically Distributed (i.i.d)|i.i.d]]. This implies that,
$$
Pr\left(\sum_{t=1}^{n}X_t = b - a \right)
$$
Now, for the RHS:
$$
Pr\left(S_m + \sum_{t= m+1}^{n + m}X_t = b \Bigg\vert S_m = a\right)
$$
Since $S_m = a$,
$$
Pr\left(\sum_{t=m+1}^{n+m}X_t = b - a \Bigg\vert S_m = a\right)
$$Recall that all $X_t$ are [[Independent and Identically Distributed (i.i.d)|i.i.d]]. This implies that,
$$
Pr\left(\sum_{t=m+1}^{n+m}X_t = b - a \right)
$$
Since both are sides involve the sum of $n$ [[Independent and Identically Distributed (i.i.d)|i.i.d.]] variables, these have the same probability. Finally, 
$$
Pr\left(\sum_{t=1}^{n}X_t = b - a \right) = Pr\left(\sum_{t=m+1}^{n+m}X_t = b - a \right)
$$
and therefore time homogeneity is proven.