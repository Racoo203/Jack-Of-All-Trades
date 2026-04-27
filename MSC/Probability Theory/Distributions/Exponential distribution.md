## [[Probability Density Function (PDF)]]
$$
f(x | \lambda) = \begin{cases} 
	\lambda \exp(-\lambda x), & x \geq 0 \\ 
	0, & x<0
\end{cases} 
$$
$\lambda$ being the distribution's parameter. The exponential distribution support is $x \in [0, \infty)$.

## [[Cumulative Distribution Function]]
$$
F(x | \lambda) = \begin{cases} 
	1 - \exp(-\lambda x), & x \geq 0 \\ 
	0, & x<0
\end{cases} 
$$