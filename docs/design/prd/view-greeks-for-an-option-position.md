# View greeks for an option position

**Feature:** Options greeks

**Given** an open option position
**When** I view it
**Then** I see its current delta, theta, gamma, and vega

**Given** the greeks source is unavailable for a contract
**When** a poll fails
**Then** greeks show a clear "unavailable" state rather than stale or zeroed values

## Related
- [PRD](../prd.md)
