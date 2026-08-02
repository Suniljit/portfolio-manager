# Close a stock holding and record realized P&L

**Feature:** Stock realized P&L / transaction history

**Given** an open stock holding
**When** I record a sale (full or partial) with a sale price and date
**Then** realized P&L is computed for the sold portion and the transaction is added to my closed-position history

**Given** a partial sale
**When** the sale is recorded
**Then** the remaining open position reflects the reduced share count and unchanged average cost, and the sold portion moves to history

**Given** my transaction history
**When** I view it
**Then** I see each closed position with its realized P&L and an aggregate total realized P&L across all closed stock transactions

## Related
- [PRD](../prd.md)
