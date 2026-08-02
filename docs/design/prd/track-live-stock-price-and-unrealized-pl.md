# Track live stock price and unrealized P&L

**Feature:** Live stock pricing & unrealized P&L

**Given** I have one or more open stock holdings
**When** the app polls for current prices
**Then** each holding's current price, total cost, market value, and unrealized P&L are recalculated and displayed without any manual entry

**Given** the price source is temporarily unavailable for a ticker
**When** a poll fails for that ticker
**Then** the holding shows a clear "price unavailable" state rather than a silently stale or zeroed value

**Given** multiple open holdings
**When** I view the portfolio
**Then** I see an aggregate total cost, market value, and unrealized P&L across all holdings, not just per-row values

## Related
- [PRD](../prd.md)
