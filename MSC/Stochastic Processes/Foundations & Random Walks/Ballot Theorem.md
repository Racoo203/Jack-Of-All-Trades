## Definition
Consider two candidates, $A$ and $B$, that are participating in an election. It is known that the candidate $A$ received $k$ votes and the candidate $B$ received $n − k$ votes, with $k > n − k$. 

Let $S_n = S_0 + \sum_{t=1}^{n} X_t$, where $S_0 = 0$ and $X_t$ is a [[Random Variable|random variable]] such that $X_t=1$ represents the $t$-th vote for $A$, whereas $X_t=-1$ represents the $t$-th vote for $B$. 

Then, the probability that $A$ remained strictly ahead of $B$ throughout the vote count is:
$$
Pr(S_1 > 0, S_2 > 0, \cdots, S_n > 0) = \frac{2k-n}{n}
$$
Which can be proven starting by noting $S_n$ can be rewritten as follows:
$$
S_n = k(1)+(n-k)(-1) = 2k - n
$$
In total, there are $\binom{n}{k}$ ways of reaching the state $2k-n$. For $A$ to remain strictly ahead of $B$ throughout the vote count the first vote must result favorable to $A$. Thus, $S_1 = 1$, implying that in $n-1$ steps, the vote reached a final count of $2k-n$. Therefore there are $\binom{n-1}{k-1}$ ways of reaching the state $2k-n$.

However, some of these ways would reach at some point $S_i = 0$, which must be discounted from the possible paths that would lead $A$ to be strictly ahead of $B$. Notice that if $S_1=-1$, all paths are guaranteed to eventually cross 0 at some $S_i = 0$ to end in the state $2k - n$. One can see that for each of these paths, there is has to be another path starting form $S_1=1$ that mirrors up to when $S_i = 0$. Therefore, there are the same number of paths with $S_1 = 1, S_n = 2k-n, S_i = 0$ and paths with $S_1 = -1, S_n=2k-n$, being $\binom{n-1}{k}$ (recall that there are $n-1$ remaining votes and $A$ must end up with $k$ votes). 

Therefore, there must be $\binom{n-1}{k-1} - \binom{n-1}{k}$ ways in which $A$ is strictly ahead of $B$ throughout the vote count. Simplifying, the probability of said event is:
$$
Pr(S_1 > 0, S_2 > 0, \cdots, S_n > 0) = \frac{\binom{n-1}{k-1} - \binom{n-1}{k}}{\binom{n}{k}} = \frac{\frac{(n-1)!}{(k-1)!(n-k)!}-\frac{(n-1)!}{(k)!(n-k-1)!}}{\frac{n!}{k!(n-k)!}}
$$
$$
\implies \frac{\frac{(n-1)!}{(k-1)!(n-k)!}-\frac{(n-1!)}{(k)!(n-k-1)!}}{\frac{n!}{k!(n-k)!}}\cdot\frac{(n-k)!}{(n-k)!}=\frac{\frac{(n-1!)}{(k-1)!}-\frac{(n-1)!(n-k)}{(k)!}}{\frac{n!}{k!}}
$$
$$
\implies \frac{\frac{(n-1!)}{(k-1)!}-\frac{(n-1)!(n-k)}{(k)!}}{\frac{n!}{k!}} \cdot \frac{k!}{k!} = \frac{k(n-1)!-(n-1)!(n-k)}{n!}
$$
and finally,
$$
\implies \frac{k-(n-k)}{n} = \frac{2k-n}{n}
$$
