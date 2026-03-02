# ONDO_analysis


## Data
- **On-chain (Dune, Ethereum):** USDY ERC-20 `Transfer` events to construct daily mint/burn, net mint, cumulative supply proxy, and holder balances (Top holders + bucket distribution).
- **Market price (CoinGecko CSV):** USDY USD price history to measure market price deviation vs $1 (premium/discount proxy).

## Method
- **Supply & flows:** plot cumulative supply and daily mint/burn/net mint; identify top mint/burn days; compute “flow concentration” (share of total volume explained by Top-N days).
- **Holder concentration:** compute Top-N holder share (Top 1/5/10/20/50), cumulative concentration curve (Top 50), and concentration metrics (HHI, effective number of holders).
- **Market price deviation:** time series + distribution of deviation vs $1, plus summary stats (mean, P95/P99, premium vs discount days).
- **Stress harness (capacity planning):** calibrate burn shocks from historical burn tail events (p95/p99/max of burn as % of lagged supply) and compute days-to-clear backlog under assumed daily processing capacity (% of supply/day). Produce monitoring thresholds (High/Severe/Extreme) based on empirical quantiles.

## Findings
- **Whale-driven structure:** USDY supply is highly concentrated (Top holders dominate).
- **Flows are lumpy:** a small number of days explain most mint/burn volume; redemption risk is tail-event driven.
- **Persistent premium:** USDY trades above $1 on most days; deviations are structural rather than occasional noise.
- **Operational implication:** clearing tail redemptions within a short window requires materially higher processing capacity; extreme outliers motivate a contingency mode.

## Limitations
- Cumulative supply from transfers is a **proxy** (sensitive to data completeness and token mechanics); holder stats use a snapshot and may include contracts/exchanges.
- CoinGecko “close” is **market price**, not official NAV/redemption price; deviation vs $1 is a **premium/discount proxy**, not a strict peg test.
- Stress harness is a **planning model** (capacity/backlog), not a full buffer/gate mechanism design or a price-forecast model.


























