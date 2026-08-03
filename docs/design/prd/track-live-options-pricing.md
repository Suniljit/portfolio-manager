# Track live options pricing

**Feature:** Live options pricing

**As a** retail investor, **I want** open option positions' prices to refresh automatically, **so that** I can assess them using current market data

**Given** I have one or more open option positions
**When** the app polls for current option prices
**Then** each position's current mark price is refreshed without manual entry, on the same poll cadence as stock prices

**Given** the pricing source is unreachable for a contract
**When** a poll fails
**Then** the position shows a clear "price unavailable" state rather than a stale or silently zeroed value

## Related
- [PRD](../prd.md)
