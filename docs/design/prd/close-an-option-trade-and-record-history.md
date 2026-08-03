# Close an option trade and record history

**Feature:** Options closed-trade history & total P&L

**As a** retail investor, **I want** to close an option trade and have realized P&L/ROI recorded to history, **so that** I can track my trading performance over time

**Given** an open option position
**When** I close it with a closing price and date
**Then** realized P&L and ROI are computed and the trade moves to closed-trade history

**Given** my closed-trade history
**When** I view it
**Then** I see each closed trade with its realized P&L and ROI, and an aggregate total P&L across all closed option trades

## Related
- [PRD](../prd.md)
