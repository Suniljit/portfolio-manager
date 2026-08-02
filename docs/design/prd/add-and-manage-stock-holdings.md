# Add and manage stock holdings

**Feature:** Stock holdings CRUD

**Given** I want to track a new stock position
**When** I enter a ticker, number of shares, average price, and fees, and save
**Then** the holding is added to my portfolio and appears in the holdings list

**Given** an existing holding has incorrect shares or average price
**When** I edit the holding and save the corrected values
**Then** the holding reflects the new values and all computed fields (cost basis, market value, P&L) recalculate

**Given** an existing holding
**When** I delete it
**Then** it no longer appears in the holdings list and is excluded from portfolio totals

**Given** invalid input (e.g. a negative share count, a malformed ticker, an empty required field)
**When** I try to save
**Then** the save is rejected with a clear validation message and no holding is created or modified

## Related
- [PRD](../prd.md)
