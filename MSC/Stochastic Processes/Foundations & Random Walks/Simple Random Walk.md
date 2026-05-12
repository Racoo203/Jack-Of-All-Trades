A simple random walk is a special case of a [[Random Walk]]. Recall that 
$$
S_n = S_0 + \sum_{t=1}^{n} X_t
$$
Then it is specified the following property.
$$
Pr(X_t=1) = p, \text{ and } Pr(X_t=-1) = q = 1 - p
$$
Additionally, this simple random walk is called symmetric if $p=q=0.5$.
## Properties
### Transition Probabilities
Suppose $\{S_n, n\in \mathbb{N}\}$ is a [[Stochastic Process|stochastic process]]. The (1-step) transition probability of $\{S_n\}$ transiting from state $i$ into state $j$ is defined as the conditional probability $Pr(S_{n+1} = j | S_{n} = i )$. For a simple random walk, the transition probabilities are
$$
p_{ij}^{(1)} = Pr(S_{n+1} = j | S_{n} = i ) = \begin{cases} 
p, & j = i + 1 \\
q, & j = i - 1 \\
0, & \text{otherwise.}
\end{cases}
$$
for all $i,j \in S$ such that $i \neq j$.

In general, the $n$-step transition probability of $\{S_n\}$: 
$$
Pr(S_n=k | S_0 = 0) = \begin{cases}
\binom{n}{(n+k)/2}p^{(n+k)/2}q^{(n-k)/2}, & (n+k)/2 \in \{0,1,\cdots, N\} \\
0, & \text{otherwise.}
\end{cases}
$$
Such statement can be proven with the following:
$$
Pr(S_n=k|S_0=0) = Pr(2U_n-n = k) = Pr(U_n = (n + k) / 2 )
$$
where $U_n$ is the total of up-steps taken in the first $n$-steps. $U_n$ can be thought of as $n$ [[Independent and Identically Distributed (i.i.d)|i.i.d.]] [[Bernoulli distribution|Bernoulli trials]] with parameter $p$. Therefore, $U_n$ follows a [[Binomial distribution|Binomial distribution]] with parameters $n, p$.
$$
U_n \sim Bin(n,p)
$$
and,
$$
Pr(U_n=(n+k)/2) = \binom{n}{(n+k)/2}p^{(n+k)/2}q^{(n-k)/2}
$$
### Markov Property
All simple random walks have the [[Markov Property|Markov property]]. That is, the probability of reaching a given state is only dependent on immediate previous state. That is, for all $m, n \geq 0 \in T$ and $j, s_0, s_1, \cdots, s_m$, then
$$
Pr(S_{m+n} = j | S_m=s_m, S_{m-1}=s_{m-1}, \cdots, S_0 = s_0) = Pr(S_{m+n} = j | S_m = s_m)
$$

Notice how,
$$
S_{m+n} = S_m + \sum_{t=m+1}^{m+n} X_i
$$
then the LHS:
$$
Pr\left(S_m + \sum_{t=m+1}^{m+n} X_i = j \Bigg\vert S_m=s_m, S_{m-1}=s_{m-1}, \cdots, S_0 = s_0) = Pr(S_{m+n} = j\right)
$$
That is, if $S_m$ is given, then $S_{m+n}$ is only dependent on $\{X_{m+1}, X_{m+2}, \cdots, X_{m+n}\}$. Therefore:
$$
Pr\left(\sum_{t=m+1}^{m+n} X_i = j - s_m \right)
$$
On the RHS:
$$
Pr\left(S_m + \sum_{t=m+1}^{m+n} X_i = j \Bigg\vert S_m = s_m\right)
$$
Then it follows that,
$$
Pr\left(\sum_{t=m+1}^{m+n} X_i = j - s_m \right)
$$
And finally, since both sides equate to this expression, the Markov property is proved for all random walks.
### Expected Value
$$
\mathbb{E}[S_n] = \mathbb{E}\left[S_0 + \sum_{t=1}^{n} X_t \right]
$$
By the [[linearity of expectation]],
$$
\mathbb{E}[S_n] = S_0 + \sum_{t=1}^{n} \mathbb{E} \left[ X_t \right]
$$
By definition,
$$
\mathbb{E} \left[ X_t \right] = \sum_{s \in S} Pr(X_t = s) \cdot s = (p)(1)+q(-1) = p-q
$$
Because all $X_t$ are [[Independent and Identically Distributed (i.i.d)|i.i.d]], in general the expectation is:
$$
\mathbb{E}[S_n] = S_0 + \sum_{t=1}^{n} p-q = S_0 + n(p-q)
$$
Finally, a symmetric simple random walk $(p=q=0.5)$ implies
$$
\mathbb{E}[S_n] = S_0 + n(p-q) = S_0
$$
### Variance
Recall that for all $t$, $X_t$ are independent and identically distributed. Therefore, all $X_t$ have the same variance.
$$
\text{Var}[S_n] = \text{Var}\left[S_0 + \sum_{t=1}^{n} X_t \right] = n \text{Var}[X_t]
$$
Then, the variance of $X_t$ is shown as below
$$
\text{Var}[X_t] = \mathbb{E}[(X_t)^2] - (\mathbb{E}[X_t])^2
$$
Which is equivalent to
$$
\text{Var}[X_t] = (1) - (p - q)^2 = 1-(2p-1)^2=1-(4p^2-4p+1) 
$$
Thus,
$$
\text{Var}[X_t] = 4p - 4p^2 = 4p(1-p) = 4pq
$$
Finally,
$$
\text{Var}[S_n] = 4pqn
$$
### Probability of Revisiting
Consider the probability that a simple random walk will ever return to $0$. Assume that $S_0 = 0$. Then, the probability that it ever returns to its starting point is given by
$$
Pr(\text{ever returns to } 0 | S_0=0)= 1−|p−q|
$$
To prove this, consider the event $H$, which is the event of the random walk ever revisiting $0$, and $H_N$ the event of the random walk revisiting $0$ before reaching $N$. Then, 
$$
Pr(H | S_0 = 0) = Pr(H|S_1=1)\cdot Pr(S_1 = 1 | S_0 = 0) + Pr(H|S_1=-1)\cdot Pr(S_1=-1 | S_0=0)
$$
$$
\implies Pr(H | S_0 = 0) = Pr(H|S_1=1)p + Pr(H|S_1=-1)q
$$
There are two cases to consider.
#### Case 1: $p\neq q$.
Let $p \neq q$, then $p>q$ or $q > p$. Assume $p>q$,
$$
Pr(H|S_0=1)=\lim_{N \to \infty}Pr(H_N|S_0=1)
$$
Notice how returning to zero is another way to rephrase the [[Gambler's Ruin|ruin probability]]. Therefore,
$$
Pr(H|S_0=1)=\lim_{N \to \infty}\frac{(q/p)-(q/p)^N}{1-(q/p)^N}=q/p
$$
Now, for when $S_0=-1$,
$$
Pr(H|S_0=-1)=\lim_{N \to \infty}\frac{(p/q)-(p/q)^N}{1-(p/q)^N}=1
$$
$$
Pr(H | S_0 = 0) = (q/p) \cdot (p) + (1) \cdot (q) = 2q
$$
That is,
$$
Pr(H|S_0=0) = q+(1-p) =1+(q-p)
$$
However, since $p>q$, $q-p$ is negative, which cannot be the case for any probability. Hence,
$$
Pr(H|S_0=0)=1-\lvert p - q \rvert
$$
#### Case 2: $p=q$
In the case of $p=q$, one can model the probability of $Pr(H | S_0 =1)$ as the ruin probability when $p=q$.
$$
Pr(H|S_0=1) = \lim_{N \to \infty} Pr(H_N | S_0 = 1) = \lim_{N \to \infty}(1-1/N)
$$
which implies
$$
Pr(H | S_0 = 1) = 1
$$
For the case of $S_0 = -1$, consider that $S_n$ is symmetric and therefore,
$$
Pr(H|S_0=-1) = \lim_{N \to \infty} Pr(H_N | S_0 = -1) = 1
$$
Thus,
$$
Pr(H | S_0 = 0) = (1) \cdot (p) + (1) \cdot (q) = 1
$$
Which means that the return to zero is guaranteed on a symmetric simple random walk.

#### Expected Number of Steps for Return
The expected number of steps that a symmetric simple random walk takes for its first return to the starting point $0$ is infinite. To prove as such, define $\nu_k$ as the expected value of the number of steps for return starting from $k$. Then,
$$
\nu_{0}=0.5 \nu_1 + 0.5\nu_{-1} + 1
$$
Let $T_k^{N}$ be the number of steps needed to reach either $0$ or $N$, just as defined in the expected game duration of the of the [[Gambler's Ruin]]. Then, 
$$
T_k \geq T_k^N \implies \mathbb{E}[T_k] \geq \mathbb{E}[T_k^N]
$$
Since $\mathbb{E}[T_k^N]$ is $\mu_k = k(N-k)$ when accounting for a symmetric random walk, the following is true
$$
\nu_k \geq k(N-K)
$$
However, consider that the problem studied assumes $N \to \infty$. With $k=1$, it is easy to see that,
$$
\nu_1 \geq \lim_{N \to \infty}1(N-1) = +\infty
$$
which implies that $\nu_0 = +\infty$.