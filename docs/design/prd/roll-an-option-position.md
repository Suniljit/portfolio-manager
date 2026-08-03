# Roll an option position

**Feature:** Options rolling

**As a** retail investor, **I want** to roll an open option position to a new strike or expiration, **so that** I can manage the trade forward without losing its history

**Given** an open option position I want to roll
**When** I enter a new strike and/or expiration date and confirm the roll
**Then** the original position is closed (recorded to closed-trade history with its realized P&L) and a new position is opened at the new strike/expiration, linked back to the original trade

**Given** a rolled position
**When** I view its history
**Then** I can trace the chain of rolls back to the original trade, including the P&L realized at each roll

## Related
- [PRD](../prd.md)
