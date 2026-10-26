---
title: "M/M/s/N Queue"
domain: "Optimization & Control"
course: "Stochastic Optimization"
level: BSc
status: drafted
confidence: 0
tags: [queueing-theory, stochastic-optimization]
---
## Definition
The $(M/M/s{>}1)/(-/N/-)$ queue combines [[M-M-s Queue|multiple servers]] with [[M-M-1-N Queue|finite capacity]]: $s$ parallel servers each at rate $\mu$, Poisson arrivals at rate $\lambda$, total system capacity $N=s+c$. As with [[M-M-1-N Queue]], arrivals that find the system full balk, so the effective arrival rate $\hat\lambda < \lambda$ in general.

## Properties
### Steady-state probabilities and $P_0$
The same state-dependent birth-death structure as [[M-M-s Queue]] applies, but now truncated at $N$:
$$
P_n = \begin{cases} \dfrac{\sigma^n}{n!}P_0 & 0\le n<s\\[4pt] \dfrac{\sigma^n}{s!\,s^{\,n-s}}P_0 & s\le n\le N\end{cases}, \qquad
P_0 = \left(\sum_{n=0}^{s-1}\frac{\sigma^n}{n!} + \sum_{n=s}^{N}\frac{\sigma^n}{s!\,s^{\,n-s}}\right)^{-1}.
$$
Because the second sum is now finite (up to $N$, not $\infty$), $P_0$ is well-defined for any $\sigma$, including $\sigma \ge s$ — no stability condition is needed, exactly as in [[M-M-1-N Queue]].

### Effective arrival rate, utilization, $L_q$
$$
\hat\lambda = \lambda\left(1 - \frac{\sigma^N}{s!\,s^{\,N-s}}P_0\right), \qquad \rho = \frac{\hat\lambda}{s\mu} = \frac{\sigma}{s}\left(1-\frac{\sigma^N}{s!\,s^{\,N-s}}P_0\right),
$$
$$
L_q = \sum_{n=s}^N (n-s)P_n, \qquad L = W\hat\lambda,\qquad W = W_q + \frac1\mu, \qquad W_q = \frac{L_q}{\hat\lambda}.
$$

### Worked example: two-pump gas station ("Eat & Gas")
$s=2$ pumps, lane capacity $N=5$ (so $c=3$ waiting), Poisson arrivals $\lambda=20$/hr, exponential service $\mu=10$/hr ($6$ min average), $\sigma=\lambda/\mu=2$:
$$
P_0 = \left(\sum_{n=0}^{1}\frac{2^n}{n!} + \sum_{n=2}^{5}\frac{2^n}{2!\cdot2^{\,n-2}}\right)^{-1} \approx 0.090909,
$$
and the proportion of cars that leave without filling up (balking) is
$$
P_5 = \frac{2^5}{2!\cdot2^{5-2}}P_0 \approx 0.181818 = 18.18\%.
$$

## See also
[[M-M-s Queue]], [[M-M-1-N Queue]], [[M-M-1 Queue]], [[Kendall's Notation]], [[Little's Law]]
