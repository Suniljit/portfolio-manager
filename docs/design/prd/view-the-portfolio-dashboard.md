# View the portfolio dashboard

**Feature:** Portfolio dashboard

**Given** I have open stock holdings and/or option positions
**When** I open the dashboard
**Then** I see combined totals across both — total market value, total unrealized P&L, and count of open positions

**Given** prices are refreshed on a poll
**When** a poll completes
**Then** the dashboard totals update without a manual reload

## Related
- [PRD](../prd.md)
