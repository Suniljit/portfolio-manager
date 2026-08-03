# View DTE, open P&L, and ROI for an option position

**Feature:** Options DTE, open P&L, and ROI

**As a** retail investor, **I want** to see DTE, open P&L, and ROI for each option position, **so that** I can judge timing and performance without calculating it myself

**Given** an open option position with an expiration date
**When** I view it
**Then** remaining days-to-expiration (DTE) is computed and displayed, counting down as time passes

**Given** an open option position and its current mark price
**When** the price updates
**Then** open P&L and ROI are recomputed, correctly signed for the position's direction (long vs. short)

## Related
- [PRD](../prd.md)
