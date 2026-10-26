---
title: "Long and Short Positions"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "Chapter 4 - Financial Markets"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, positions]
---
## Definition
A **long position** involves the *purchase* of an asset, option, or future; a **short position** involves *selling* it (potentially without owning it — "short selling"). **Position diagrams** plot profit against the terminal share price $S_T$ to visualise the payoff of a strategy.

## Properties
### Long call profit diagram
For a long [[Call option]] with strike $K$ and premium $p$: profit $=\max\{S_T-K,0\}-p$, a kinked line that is flat at $-p$ for $S_T\le K$ and rises with slope $1$ thereafter, crossing zero (breakeven) at $S_T=K+p$.

### Short selling
Maintaining a short position in the underlying asset (selling assets not owned) may be required to keep a hedge [[Greeks|delta]]-neutral; a broker may require margin to cover adverse movements against the short seller, though this margin typically earns interest.

## Examples
See [[Option Trading Strategies]] for a full catalogue of long/short combinations (straddles, spreads, strangles, etc.) built from long and short calls/puts.

## See also
[[Call option]], [[Put option]], [[Option Trading Strategies]], [[Hedging]]
