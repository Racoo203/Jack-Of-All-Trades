## Definition
A [[Stochastic Process]] can be either discrete or continuous in the context of spaces (as in the sample space of the random variables) and time (the time step between the observation of said random variables).

## Examples
Let $X_1$ be the time a squirrel takes to find a first nut, and for $i>1$, $X_i$ is the time the squirrel takes to find the $i$-th nut after finding the $(i-1)$-th nut. Then the stochastic process $\{X_i\}$ is continuous-space, discrete-time.

Now, define $N_t$ as below: $$
N_t := \max\{n : \sum_{i=0}^{n} < t\}
$$ Then the stochastic process $\{N_t\}$ is discrete-space, continuous-time.