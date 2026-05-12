## Definition
Let $X_n$ be a [[Discrete-Time Markov Chain]], time homogeneous, with state space $S$. Then, the Chapman-Kolmogorov equation (C-K equation) holds, i.e.
$$
p_{ij}^{(m+n)} = \sum_{k \in S} p_{sk} ^{(m)} \cdot p_{kj}^{(n)}
$$
To prove it, recall
$$
p_{ij}^{(m+n)} = Pr(X_{m+n} = j | X_{0} = i)
$$
By the law of total probability,
$$
p_{ij}^{(m+n)} = \sum_{k \in S} Pr(X_{m+n} = j, X_{m} = k | X_0 = i)
$$
which can be rewritten as follows, using the definition of conditional probability,
$$
p_{ij}^{(m+n)} = \sum_{k \in S} \frac{Pr(X_{m+n} = j, X_{m} = k, X_0 = i)}{Pr(X_0 = i)}
$$
Notice how $Pr(X_{m+n} = j, X_{m} = k, X_0 = i)$ is equal to $Pr(X_{m+n} = j | X_{m} = k, X_0 = i) \cdot Pr(X_m = k, X_0 = i)$, which gives,
$$
p_{ij}^{(m+n)} = \sum_{k \in S} \frac{Pr(X_{m+n} = j | X_{m} = k, X_0 = i) \cdot Pr(X_m = k, X_0 = i)}{Pr(X_0 = i)}
$$
Once again rewriting with the definition of conditional probability:
$$
p_{ij}^{(m+n)} = \sum_{k \in S} Pr(X_{m+n} = j | X_{m} = k, X_0 = i) \cdot Pr(X_m = k | X_0 = i)
$$
Due to the Markov property,
$$
p_{ij}^{(m+n)} = \sum_{k \in S} Pr(X_{m+n} = j | X_{m} = k) \cdot Pr(X_m = k | X_0 = i)
$$
Which finally can be rewritten as
$$
p_{ij}^{(m+n)} = \sum_{k \in S} p_{kj}^{(n)} \cdot p_{ik}^{(m)}= \sum_{k \in S} p_{ik}^{(m)} \cdot p_{kj}^{(n)}
$$
In matrix form:
$$
P^{(m+n)} = P^{(m)} \cdot P^{(n)}
$$