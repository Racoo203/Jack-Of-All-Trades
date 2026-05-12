## Definition
A discrete-time Markov chain is a sequence of [[Random Variable|random variables]]
$X_0, X_1, X_2, \cdots$ taking values in state space $S$ such that, for all $n, k \in \mathbb{N}$
and $i, j, x_0, x_1, \cdots, x_{n−1} \in S$, 
$$
Pr(X_{n+1} = j | X_n= i, X_{m-1}=x_{m-1}, \cdots, X_0 = x_0) = Pr(X_{n+1} = j | X_n = i )
$$
In other words, it is a discrete-time [[Stochastic Process]] satisfying the
[[Markov Property]]. Additionally, this property holds for any $X_{n+j}$ such that $n+j > n$.

## Properties
### Transition Probability
Recall that the one-step transition probability, $p_{ij, n}$ denotes the probability that the stochastic process will transfer from state $i$ into state $j$ in one step:
$$
p_{ij, n}=Pr(X_{n+1} = j | X_{n} = i)
$$
Further, assume that the space state is also discrete, i.e. $S \subseteq \mathbb{N}$.
