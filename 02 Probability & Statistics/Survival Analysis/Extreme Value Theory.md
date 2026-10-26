---
title: "Extreme Value Theory"
domain: Probability & Statistics
course: Survival Analysis
unit: "Chapter 9 - Extreme Value Theory"
level: MSc
status: drafted
confidence: 0
tags: [survival-analysis, extreme-value-theory, gev, gpd]
---
## Definition
Insurers traditionally fit a single loss distribution to an *entire* dataset of past claims, including extremes. Because the bulk of the data is non-extreme, this majority dominates the fit, so the tail is underweighted and the resulting model can **underestimate** the likelihood and severity of rare, catastrophic events (underpricing, inadequate reserving). **Extreme value theory (EVT)** instead fits a distribution specifically to the *tail*, in one of two ways:

- **Block maxima**: split the data into blocks (e.g. one per year) and take the maximum claim in each block, $X_M=\max\{X_1,\dots,X_n\}$. These converge to a **Generalised Extreme Value (GEV)** distribution.
- **Threshold exceedances**: fix a high threshold $u$ and look at all values exceeding it. These converge to a **Generalised Pareto Distribution (GPD)**.

In both cases, convergence to a fixed limiting family holds regardless of the underlying distribution of individual claims — in the same way the CLT gives a universal limit for (normalised) sums, EVT gives a universal limit for (normalised) maxima/exceedances.

## Properties

### Distribution of the block maximum
For i.i.d. $X_1,\dots,X_n$ with common cdf $F$, and $X_M=\max\{X_1,\dots,X_n\}$:
$$
P(X_M\leq x) = P(X_1\leq x,\dots,X_n\leq x) = P(X_1\leq x)\cdots P(X_n\leq x) = [F(x)]^n
$$
Since $[F(x)]^n\to 0$ or $1$ pointwise as $n\to\infty$ (a degenerate limit), we instead standardise: find sequences $\alpha_n$ and $\beta_n>0$ such that
$$
\lim_{n\to\infty} P\left(\frac{X_M-\alpha_n}{\beta_n}\leq x\right) = \lim_{n\to\infty}[F(\beta_n x+\alpha_n)]^n
$$
converges to a non-degenerate distribution depending only on $x$.

### Extreme Value Theorem (Fisher–Tippett–Gnedenko)
There exist constants $\alpha_n,\beta_n$ such that the standardised maximum converges to
$$
\lim_{n\to\infty}[F(\beta_n x+\alpha_n)]^n = H(x)
$$
where
$$
H(x) = \begin{cases} \exp\left[-\left(1+\gamma\dfrac{x-\alpha}{\beta}\right)^{-1/\gamma}\right] & \gamma\neq 0 \\[4pt] \exp\left[-\exp\left(-\dfrac{x-\alpha}{\beta}\right)\right] & \gamma=0 \end{cases}
$$
with **location** $\alpha$, **scale** $\beta>0$, and **shape** $\gamma$ — the **Generalised Extreme Value (GEV)** distribution. In practice, $X_M\approx \alpha_n+\beta_n\,\mathrm{GEV}(\alpha,\beta,\gamma)$, so maxima can be modelled via the GEV without knowing the distribution of the individual claims.

#### Worked derivation: Exponential ($\to$ Gumbel, $\gamma=0$)
For $F(x)=1-e^{-\lambda x}$, choose $\alpha_n=\frac{1}{\lambda}\ln n$, $\beta_n=\frac{1}{\lambda}$:
$$
\lim_{n\to\infty}[F(\beta_n x+\alpha_n)]^n = \lim_{n\to\infty}\left[1-\exp\left(-\lambda\left(\tfrac{1}{\lambda}x+\tfrac{1}{\lambda}\ln n\right)\right)\right]^n = \lim_{n\to\infty}\{1-\exp(-x-\ln n)\}^n = \lim_{n\to\infty}\left(1-\frac{e^{-x}}{n}\right)^n = e^{-e^{-x}}
$$
using $\lim_{n\to\infty}(1+x/n)^n=e^x$. This is the $\gamma=0$ (Gumbel) case.

#### Worked derivation: Uniform ($\to$ Weibull-type, $\gamma=-1$)
For $F(x)=x$ on $[0,1]$, choose $\alpha_n=1$, $\beta_n=1/n$:
$$
\lim_{n\to\infty}[F(\beta_n x+\alpha_n)]^n = \lim_{n\to\infty}\left[\frac{x}{n}+1\right]^n = e^x
$$
which is a GEV with $\alpha=0,\beta=1,\gamma=-1$ (finite upper endpoint at $x=0$, since the standardised variable cannot exceed $0$).

### The three domains of attraction
The shape parameter $\gamma$ determines which family $H$ belongs to:
- **Weibull-type** ($\gamma<0$): underlying distributions with a **finite upper limit** (e.g. Uniform, worked above).
- **Gumbel-type** ($\gamma=0$): **light-tailed** underlying distributions (e.g. Exponential, worked above; also Normal, Gamma, Log-normal).
- **Fréchet-type** ($\gamma>0$): **heavy-tailed** underlying distributions with polynomial tail decay (e.g. Pareto, Cauchy, Student-$t$).

Densities of the three limiting families (location-scale form, $\mu,\beta$):
$$
\text{Gumbel: } f(x)=\frac{1}{\beta}e^{-\frac{x-\mu}{\beta}}e^{-e^{-\frac{x-\mu}{\beta}}}, \qquad \text{Fréchet: } f(x)=\frac{\alpha}{s}\left(\frac{x-m}{s}\right)^{-(1+\alpha)}e^{-(\frac{x-m}{s})^{-\alpha}},\ x>m
$$
$$
\text{Weibull: } f(x)=\frac{k}{\lambda}\left(\frac{x}{\lambda}\right)^{k-1}e^{-(x/\lambda)^k},\ x\geq 0
$$
Note the naming clash: this "Weibull" *domain of attraction* is a distinct object from the [[Weibull distribution|Weibull distribution]] used elsewhere in the course as a lifetime model (a Weibull-distributed lifetime does not itself belong to the Weibull maximum-domain; rather it is the *limiting law of maxima* for distributions with a finite right endpoint).

### GEV scaling laws
Since $\alpha_n,\beta_n$ depend on the block size $n$, choosing a different block size $M^*=kM$ requires rescaling rather than refitting from scratch: if $X_M\sim\mathrm{GEV}(\mu,\sigma,\xi)$, then $X_{M^*}\sim\mathrm{GEV}(\mu^*,\sigma^*,\xi)$ with
$$
\mu^* = \begin{cases}\mu+\sigma\dfrac{k^\xi-1}{\xi} & \xi\neq 0\\ \mu+\sigma\log(k) & \xi=0\end{cases}, \qquad \sigma^*=\sigma k^\xi
$$
(the shape $\xi$ is unchanged by rescaling the block size). Choosing block size in practice is a bias-variance trade-off: too large (few blocks) leaves too little data to fit the GEV; too small, and the asymptotic GEV approximation no longer holds.

### Threshold exceedances and the Generalised Pareto Distribution
For $X$ with cdf $F$ and a high threshold $u$, define the **excess** $X-u\mid X>u$, with conditional cdf
$$
F_u(x) = P(X-u\leq x\mid X>u) = \frac{P(u<X\leq x+u)}{P(X>u)} = \frac{F(x+u)-F(u)}{1-F(u)}
$$
**Threshold exceedance theorem.** As $u$ increases toward the right endpoint of $F$, $F_u(x)\to G(x)$, the **Generalised Pareto Distribution (GPD)** with shape $\gamma$ and scale $\beta$:
$$
G(x) = \begin{cases}1-\left(1+\gamma\dfrac{x}{\beta}\right)^{-1/\gamma} & \gamma\neq 0\\ 1-\exp\left(-\dfrac{x}{\beta}\right) & \gamma=0\end{cases}
$$

#### Worked derivation: Exponential exceedances are exponential (memoryless property)
For $F(x)=1-e^{-\lambda x}$:
$$
F_u(x) = \frac{\left(1-e^{-\lambda(x+u)}\right)-\left(1-e^{-\lambda u}\right)}{1-(1-e^{-\lambda u})} = \frac{e^{-\lambda u}-e^{-\lambda(x+u)}}{e^{-\lambda u}} = 1-e^{-\lambda x}
$$
identical to the original exponential — the GPD limit is exact (not merely asymptotic) here, which is exactly the memoryless property of the exponential distribution.

### GPD scaling laws
If $X-u_0\mid X>u_0$ follows $\mathrm{GPD}(\gamma,\beta)$, then for any higher threshold $u>u_0$, $X-u\mid X>u$ follows $\mathrm{GPD}(\gamma^*,\beta^*)$ with
$$
\gamma^*=\gamma, \qquad \beta^*=\beta+\gamma(u-u_0)
$$
so once the GPD is fitted at the threshold where the asymptotic approximation starts to hold, fits at any higher threshold follow by this scaling rule rather than by refitting.

### Measures of tail weight

#### Existence of moments
A distribution's tail is "light" if all its moments $E[X^k]=\int_0^\infty x^k f(x)\,dx$ are finite; a distribution with some moments infinite has a heavier tail.

**Gamma$(\alpha,\lambda)$: all moments finite.** With $f(x)=\frac{\lambda^\alpha}{\Gamma(\alpha)}x^{\alpha-1}e^{-\lambda x}$:
$$
E(X^k) = \int_0^\infty x^k\frac{\lambda^\alpha}{\Gamma(\alpha)}x^{\alpha-1}e^{-\lambda x}dx = \frac{\Gamma(k+\alpha)}{\Gamma(\alpha)\lambda^k}\int_0^\infty \frac{\lambda^{k+\alpha}}{\Gamma(k+\alpha)}x^{k+\alpha-1}e^{-\lambda x}dx = \frac{\Gamma(k+\alpha)}{\Gamma(\alpha)\lambda^k}
$$
recognising the integrand (after rescaling) as a $\Gamma(k+\alpha,\lambda)$ density integrating to 1. Finite for every $k=1,2,3,\dots$ — a light tail.

**Pareto: only finitely many moments finite.** With $f(x;\alpha,x_m)=\alpha x_m^\alpha/x^{\alpha+1}$, $x\geq x_m$:
$$
E(X^k) = \int_{x_m}^\infty x^k\frac{\alpha x_m^\alpha}{x^{\alpha+1}}dx = \alpha x_m^\alpha\int_{x_m}^\infty x^{k-\alpha-1}dx = \alpha x_m^\alpha\left[\frac{x^{k-\alpha}}{k-\alpha}\right]_{x_m}^{\infty}
$$
which is **finite only if $k<\alpha$** — a heavy tail: e.g. $\alpha\leq 2$ means the Pareto distribution has infinite variance.

#### Limiting density ratios
An alternative comparison: for two densities $f_1,f_2$, examine $\lim_{x\to\infty} f_1(x)/f_2(x)$. If the limit is $+\infty$, $f_1$ has the thicker tail; if $0$ (equivalently $f_2(x)/f_1(x)\to\infty$), $f_2$ has the thicker tail.

**Pareto($\alpha=2$) vs. Pareto($\alpha=3$), same $x_m$:**
$$
\lim_{x\to\infty}\frac{f_{\alpha=2}(x)}{f_{\alpha=3}(x)} = \lim_{x\to\infty}\frac{2x_m^2/x^3}{3x_m^3/x^4} = \lim_{x\to\infty}\frac{2x}{3x_m}=\infty
$$
confirming the smaller shape parameter ($\alpha=2$) gives the thicker tail (consistent with the moment result above: $\alpha=2$ has infinite variance, $\alpha=3$ does not).

**Gamma$(0.5,0.005)$ vs. Pareto$(4,300)$** (matched to have the same mean 100 and variance 20000):
$$
\lim_{x\to\infty}\frac{f_{\text{gamma}}(x)}{f_{\text{Pareto}}(x)} = \lim_{x\to\infty} C\cdot\frac{x^{-0.5}e^{-0.005x}}{(300+x)^5} = 0
$$
since the exponential decay dominates any polynomial growth or decay — the Gamma (Gumbel-type, light-tailed) has a strictly lighter tail than the Pareto (Fréchet-type, heavy-tailed) despite matching mean and variance, illustrating that first and second moments alone do not characterise tail weight.

### Tails of common distributions (reference table)
| Distribution | Tail behaviour as $x\to\infty$ | EVT domain |
|---|---|---|
| Pareto | $\propto x^{-\alpha-1}$ | Fréchet |
| Fréchet | $\propto x^{-\alpha-1}$ | Fréchet |
| Cauchy | $\propto x^{-2}$ | Fréchet |
| Log-normal | $\propto x^{-3}$ (super-exponential decay, but polynomial-*like* comparison) | Gumbel |
| Exponential | $\propto e^{-\lambda x}$ | Gumbel |
| Chi-squared | $\propto e^{-x/2}$ | Gumbel |
| Gumbel | $\propto e^{-x}$ | Gumbel |
| Normal | $\propto e^{-x^2}$ | Gumbel |
| Gamma | $\propto e^{-x/\beta}$ | Gumbel |
| Weibull (as a lifetime model) | $\propto e^{-(x/\beta)^\alpha}$ | Weibull-type (bounded case aside) |

### Relevance to actuarial applications
EVT is used to model extreme claim sizes, catastrophic mortality shocks, and the tails of loss distributions for reinsurance pricing and reserving — related in spirit to [[Tail Dependence]], though EVT concerns the marginal tail of a single variable while tail dependence concerns the *joint* tail behaviour of two variables via a [[Copula|copula]].

## Examples
**Pareto claims, GEV (Fréchet) approximation.** Claims follow $\mathrm{Pareto}(\kappa=50,\alpha=2)$. $P(X>400)=1-(1-(50/400)^2)=1/64$. For the maximum of 100 claims, the exact probability is $1-(1-1/64)^{100}=0.7929$; the Fréchet-GEV approximation (using $a_{100}=1/\alpha=0.5$, $b_{100}=\kappa\cdot100^{1/\alpha}=500$, $c_{100}=\kappa\cdot100^{1/\alpha}/\alpha=250$) gives $0.7904$ — close agreement even at $n=100$.

**Exponential claims, GEV (Gumbel) approximation.** Claims follow Exponential with mean $1/\lambda=100$. $P(X>400)=e^{-4}=0.0183$. The exact probability the maximum of 100 claims exceeds 400 is $1-(1-e^{-4})^{100}=0.8425$; the Gumbel-GEV approximation (using $\alpha_{100}=\frac{1}{\lambda}\ln100=460.517$, $\beta_{100}=1/\lambda=100$) gives $0.8398$.

**Ratio-limit exam questions.** Typical question: compute $\lim_{x\to\infty} f_1(x)/f_2(x)$ for two named densities (e.g. $t_3$ vs. Normal: the $t_3$ density decays polynomially ($\sim x^{-5}$) against the Normal's $e^{-x^2/2}$, so the ratio $\to\infty$, confirming $t_3$ has the heavier tail; or Gamma($k{=}2,\lambda{=}1$) vs. Exponential($\lambda{=}1$): ratio $=xe^{-x}/e^{-x}=x\to\infty$, so the Gamma has the heavier tail here).

## See also
[[Parametric Survival Models]], [[Tail Dependence]], [[Weibull distribution]], [[Gamma distribution]], [[Pareto distribution]]
