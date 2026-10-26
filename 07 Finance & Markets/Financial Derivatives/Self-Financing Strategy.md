---
title: "Self-Financing Strategy"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "Chapter 5 - Binomial Trees (Appendix); Chapter 8 - Risk-Neutral Pricing"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, replication, portfolio-theory]
---
## Definition
Suppose at time $t$ we hold a portfolio $\langle\phi_t,\psi_t\rangle$: $\phi_t$ units of the risky asset $S_t$ and $\psi_t$ units of a risk-free cash bond $B_t$, both **previsible** (i.e. $\mathcal F_{t^-}$-measurable — known just before, but not including, $t$). The portfolio's value is $V(t)=\phi_tS_t+\psi_tB_t$.

The portfolio is **self-financing** if, over a small interval $[t,t+dt]$ with no cash added or withdrawn,
$$
dV(t) = \phi_t\,dS_t+\psi_t\,dB_t.
$$

## Properties
### Derivation
In general, allowing inflows/outflows,
$$
dV(t) = \phi_t\,dS_t + S_t\,d\phi_t + d\phi_t\,dS_t + \psi_t\,dB_t + B_t\,d\psi_t + d\psi_t\,dB_t.
$$
Requiring $d\phi_t=d\psi_t=0$ (no rebalancing that injects or removes cash) collapses this to the self-financing condition above: all changes in portfolio value come purely from asset-price and interest movements, not from new capital.

### Role in pricing
Self-financing is the technical condition that makes a trading strategy a legitimate candidate for [[Replicating Portfolio|replication]]: a replicating strategy is required to be self-financing so that matching the derivative's terminal payoff is genuinely equivalent to "the derivative and the portfolio have the same value throughout," not merely at the final date.

## See also
[[Replicating Portfolio]], [[Complete and Incomplete Financial Markets]], [[Risk-neutral pricing]], [[Binomial option pricing model]]
