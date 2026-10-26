---
title: "Gambler's Ruin"
domain: Stochastic Processes
course: Stochastic Processes
unit: Foundations & Random Walks
level: MSc
status: seeding
confidence: 0
tags: [seeding]
---
## Definition
Consider the following game:
- a coin is tossed repeatedly by a gambler $G$,
- $G$ wins $1$ (pound) each time heads appears with probability $p$,
- $G$ loses $1$ each time tails appears with probability $q = 1 − p$,
- after $n$ tosses, their wealth is $S_n$.
- the gambler wins when their wealth reaches $N$, and loses when their wealth reaches $0$.
- their initial wealth is $S_0 = k \in [0,N]$,
Then, let $X_t$ be the [[Random Variable|random variable]] representing the resulting change in wealth due to the $t$-th coin toss. It follows that:
$$
S_n = S_0 + \sum_{t=1}^{n} X_t = S_{n-1} + X_n
$$
## Properties
### Ruin Probability
Let $R_k$ denote the event that the player $G$ is ultimately ruined given
$S_0 = k$, and denote $y_k = Pr(R_k)$, the associated ruin probability.

If $X_1 = 1$, it follows that $Pr(R_k | X_1 = 1) = Pr(R_{k+1}) = y_{k+1}$; that is, it is the ruin probability from the resulting wealth, $k+1$. Likewise, if $X_1 = -1$, it follows that $Pr(R_k | X_1 = -1) = Pr(R_{k-1})= y_{k-1}$.

By the [[Law of Total Probability|law of total probability]],
$$
y_k = [Pr(R_k | X_1 = 1)\cdot Pr(X_1 = 1)] + [Pr(R_k | X_1 = -1)\cdot Pr(X_1 = -1)]
$$
Which is equal to the [[second order difference equation]],
$$
y_k = y_{k+1}\cdot p + y_{k-1}\cdot q
$$
$$
\implies (y_{k+1}\cdot p) -(y_{k}) + (y_{k-1}\cdot q)=0
$$
It is reasonable to assign $y_0 = 1$ and $y_N = 0$, since a wealth of $0$ guarantees ruin and a wealth of $N$ makes it impossible. For all other $k \in [1, N-1]$, the equation can be rearranged as
$$
y_{k+1} - y_k = \frac{q}{p}(y_k - y_{k-1})
$$
Then this can be generalized as follows
$$
y_{k+1} - y_{k} = \left(\frac{q}{p}\right)^k(y_{1} - y_{0})
$$
Notice how 
$$
y_{k} - y_{0} = \sum_{i=0}^{k-1} (y_{i+1} - y_{i}) = (y_{1} - y_{0}) \sum_{i=0}^{k-1} \left(\frac{q}{p}\right)^{i}
$$
Then, there are two cases to consider. 
#### Case 1: $p \neq q$
Let $p \neq q$. Thus, using the sum of the terms of a finite geometric series,
$$
y_k-y_0 = \frac{1-(q/p)^{k}}{1-q/p}(y_1 - y_0)
$$
Thus if $k=N$, substituting with the values of $y_N$ and $y_0$ gives
$$
0 - 1 = \frac{1-(q/p)^{N}}{1-q/p}(y_1-1) \implies y_1 = \frac{q/p - (q/p)^{N}}{1-(q/p)^{N}}
$$
In general,
$$
y_k - y_0 = (y_1 - y_0) \sum_{i=0}^{k-1}\left(\frac{q}{p}\right)^{i} \implies y_k=(y_1-1)\sum_{i=0}^{k-1}\left(\frac{q}{p}\right)^{i} + 1
$$
Which is
$$
y_k=\left(\frac{q/p - (q/p)^{N}}{1-(q/p)^{N}}-\frac{1-(q/p)^N}{1-(q/p)^N}\right)\frac{1-(q/p)^{k}}{1-q/p} + 1
$$
$$
y_k=\left(-\frac{1-q/p}{1-(q/p)^N}\right)\frac{1-(q/p)^{k}}{1-q/p} + 1
$$
$$
y_k=1-\frac{1-(q/p)^k}{1-(q/p)^N} = \frac{(q/p)^{k} - (q/p)^{N}}{1-(q/p)^{N}}$
$$

Finally, it is concluded that $y_k=\frac{(q/p)^{k} - (q/p)^{N}}{1-(q/p)^{N}}$.
#### Case 2: $p = q$

Let $p=q$. Then, 
$$
y_k-y_0 = k(y_1 - y_0)
$$
Thus if $k=N$, substituting with the values of $y_N$ and $y_0$ gives
$$
0 - 1 = N(y_1-1) \implies y_1 = 1-\frac{1}{N}
$$
In general,
$$
y_k - y_0 =k(y_1 - y_0) \implies y_k=ky_1-(k-1)y_0
$$
Which is
$$
y_k = k\left(1 - \frac{1}{N}\right) - (k+1) = k - \frac{k}{N}-k+1
$$
Finally, it is concluded that $y_k=1-\frac{k}{N}$.
### Expected Game Duration
Let $\mu_k$ denote the expected game duration starting with $S_0 = k$. Whatever the outcome of the first coin toss is, that next step can be thought of as a new game starting from that point. Therefore:
$$
\mu_k = \begin{cases}
1 + \mu_{k+1}, & X_1 = 1 \\
1 + \mu_{k-1}, & X_1 = -1
\end{cases}
$$
Therefore the expectation of $\mu_k$ is,
$$
\mu_k = (1+\mu_{k+1})(p) + (1+\mu_{k-1})(q)
$$
$$
\implies \mu_k = p\mu_{k+1} + q\mu_{k-1} + 1
$$
which is an inhomogeneous [[second order difference equation]]. It is reasonable to assign $\mu_0 = 0$ and $\mu_N = 0$, since both conditions guarantee the game to end. Just as for finding the ruin probability, there are two cases to consider.
#### Case 1: $p \neq q$
Let $p \neq q$. Then,
$$
p(\mu_{k+1} - \mu_k + a) = q(\mu_k - \mu_{k-1} + a)
$$
where $a = \frac{1}{p-q}$. Rewriting,
$$
\mu_{k+1} - \mu_k + a = \frac{q}{p}(\mu_k - \mu_{k-1} + a)
$$
and thus the following holds:
$$
\mu_{k+1} - \mu_k + a = \left(\frac{q}{p}\right)^{k}(\mu_1 - \mu_0 + a)
$$
Notice how,
$$
\mu_k - \mu_0 + ka = \sum_{i=0}^{k-1} (\mu_{i+1} - \mu_{i} + a) = (\mu_{1} - \mu_{0} + a) \sum_{i=0}^{k-1} \left(\frac{q}{p}\right)^{i}
$$
Consider $k=N$. Then, substituting for the known values of $\mu_0$ and $\mu_k$, 
$$
Na = \frac{1 - (q/p)^N}{1 - (q/p)}(\mu_1 + a)
$$
Then solving for $\mu_1$,
$$
\mu_1 = a\left(\frac{N(1 - (q/p))}{1 - (q/p)^N}-1 \right)
$$
Which then, generalizing for $\mu_k$,
$$
\mu_k - \mu_0 + ka = (\mu_{1} - \mu_0 + a) \sum_{i=0}^{k-1} \left(\frac{q}{p}\right)^{i}
$$
$$
\implies\mu_k = \left(a\left(\frac{N(1 - (q/p))}{1 - (q/p)^N}-1 \right) + a \right) \frac{1 - (q/p)^k}{1 - (q/p)} - ka
$$
Simplifying, finally $\mu_k$ is:
$$
\mu_k = a\frac{N(1-(q/p))}{1-(q/p)^N} \cdot \frac{1 - (q/p)^k}{1 - (q/p)} - ka
$$
$$
\mu_k = a\left(\frac{N(1 - (q/p)^k)}{1-(q/p)^N} - k\right)
$$
or $\mu_k = \frac{1}{p-q}\left(\frac{N(1 - (q/p)^k)}{1-(q/p)^N} - k\right)$.
#### Case 2: $p = q$
Let $p = q$. Then,
$$
\mu_{k+1} - \mu_k = \mu_k - \mu_{k-1} - 2
$$and thus the following holds:
$$
\mu_{k+1} - \mu_k = \mu_1 - \mu_0 - 2k
$$
Notice how,
$$
\mu_k - \mu_0 = \sum_{i=0}^{k-1} (\mu_{i+1} - \mu_{i}) = \sum_{i=0}^{k-1} (\mu_1 - \mu_0 - 2i)
$$
Consider $k=N$. Then, substituting for the known values of $\mu_0$ and $\mu_k$, 
$$
0-0 = N\mu_1-2\sum_{i=0}^{k-1}i = N\mu_1-2\frac{(N-1)(N)}{2}
$$
Then solving for $\mu_1$,
$$
N\mu_1=(N-1)(N) \implies \mu_1 = N-1
$$Which then, generalizing for $\mu_k$,
$$
\mu_k = k(\mu_1)-{(k-1)k}=k(N-1)-(k-1)(k)
$$
$$
\implies \mu_k = k(N-k)
$$