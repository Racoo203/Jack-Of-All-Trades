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
