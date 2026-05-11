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
p_{0k}^{(n)} = \begin{cases}

\end{cases}
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