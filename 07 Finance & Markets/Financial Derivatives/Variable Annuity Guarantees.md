---
title: "Variable Annuity Guarantees"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "Chapter 6 - The Black-Scholes-Merton Model"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, actuarial, insurance, embedded-options]
---
## Definition
A **variable annuity (VA)** is an investment product sold by life insurance companies: a policyholder pays premium(s) during an **accumulation period**, and receives a stream of payments during a **pay-out period**, whose amount depends on the performance of a chosen investment fund (unlike a traditional annuity's fixed payments). To make VAs attractive despite this uncertainty, insurers embed a **guarantee** on investment performance — creating risk for the insurer that is itself priced as a derivative.

Five basic types of guarantee:
- **GMDB** — Guaranteed Minimum Death Benefit;
- **GMAB** — Guaranteed Minimum Accumulation Benefit;
- **GMMB** — Guaranteed Minimum Maturity Benefit;
- **GMWB** — Guaranteed Minimum Withdrawal Benefit;
- **GMIB** — Guaranteed Minimum Income Benefit.

## Properties
### GMMB as an embedded put option
The **GMMB** is the simplest: if the fund value $F_T$ at maturity is below the guaranteed amount $K$, the insurer tops up the policyholder's account by the shortfall. The payoff (assuming the policyholder survives to maturity) is
$$
\text{pay-off} = \max\{F_T,K\} = F_T + \max\{K-F_T,0\}.
$$
The second term is exactly the payoff of a [[Put option|European put]] with strike $K$ on the fund: the insurer's GMMB liability is equivalent to writing (and needing to hold/reserve for) a European put, and can in principle be **hedged by buying a matching put option**, priced via the [[Black-Scholes formula]] (under the BSM assumptions).

## Examples
A policyholder pays a single premium of £1{,}000 with a 100% GMMB (guaranteed $K=£1{,}000$). If the fund value falls to $S_T<£1{,}000$, the insurer must pay $\max\{0,\,1000-S_T\}$ — precisely the payoff of a European put struck at £1,000, which the insurer can buy to cover the liability.

## See also
[[Put option]], [[Black-Scholes formula]], [[Black-Scholes model]], [[Reduced-Form Credit Risk Model]]
