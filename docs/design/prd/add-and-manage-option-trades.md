# Add and manage option trades

**Feature:** Option trades CRUD

**As a** retail investor, **I want** to add, edit, and delete option trades, **so that** my open option positions are accurately tracked

**Given** I want to track a new option position
**When** I enter ticker, strategy, option type (call/put), direction (long/short), strike, expiration date, contracts, entry price, and fees, and save
**Then** the trade is added and appears in my open option positions

**Given** an existing open option trade
**When** I edit its details and save
**Then** the trade reflects the new values and all computed fields (DTE, P&L, ROI) recalculate

**Given** an existing open option trade
**When** I delete it
**Then** it no longer appears in open positions and is excluded from portfolio totals

**Given** invalid input (e.g. a non-positive strike, an expiration before the open date, a missing direction)
**When** I try to save
**Then** the save is rejected with a clear validation message and no trade is created or modified

## Related
- [PRD](../prd.md)
