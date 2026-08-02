---
doc_type: prd
status: draft
depends_on: []
last_updated: 2026-08-02
---

# Folio — PRD

## Problem Statement & Goals

Manual, spreadsheet-based tracking can't give a retail investor a live, accurate view of P&L across stock holdings and options positions. This is most acute for options: a stale price delays a roll/close decision and risks missing an exit window, and a spreadsheet has no way to compute DTE, ROI, or greeks on its own.

Folio exists to replace that manual tracking with a single-user tool that keeps stock and options positions in one place, refreshes prices on a regular poll, and computes every derived number (cost basis, market value, unrealized/realized P&L, DTE, ROI, greeks) server-side — so decisions, especially rolling or closing an options trade, are made from current data instead of a day-old broker statement or a manually updated cell.

**Goals:**
- Eliminate manual computation of P&L, DTE, ROI, and greeks — all derived fields are calculated automatically from stored trade data and polled prices.
- Give the user a single, current view of both stock holdings and options positions, open and closed.
- Make options position management (rolling, tracking time decay via DTE, assessing risk via greeks) fast enough to act on before an exit window closes.

## Target Persona

| Persona | Needs | Role / Permissions |
|---|---|---|
| Individual retail investor / options trader (the user) | A single, accurate, current view of stock and options positions; automatic P&L/DTE/ROI/greeks so no manual spreadsheet math; fast entry and editing of trades | Sole user of a personal desktop tool — full read/write access, no roles or permission tiers, no authentication |

## Feature Scope

### Must-haves (MVP)
- **Stock holdings CRUD** — add, edit, delete stock holdings (ticker, shares, average price, fees).
- **Live stock pricing & unrealized P&L** — polled price refresh; server-computed total cost, market value, and unrealized P&L per holding and in aggregate.
- **Stock realized P&L / transaction history** — closing (selling) a holding records a transaction and computes realized P&L; a history view lists closed stock positions.
- **Option trades CRUD** — add, edit, delete option trades (ticker, strategy, option type, direction long/short, strike, expiration date, contracts, entry price, fees).
- **Live options pricing** — polled price refresh for open option positions (bid/ask-quality where available, matching the cadence used for stocks).
- **Options DTE, open P&L, and ROI** — server-computed remaining days-to-expiration, open P&L, and ROI per open position.
- **Options rolling** — roll an open option position to a new strike and/or expiration, preserving a link back to the original trade for history.
- **Options greeks** — display delta, theta, gamma, and vega for open option positions.
- **Options closed-trade history & total P&L** — closing an option position records it to history with realized P&L and ROI; aggregate total P&L across closed trades.
- **Portfolio dashboard** — summary view with stat cards/totals across stocks and options (combined market value, combined P&L).

### Nice-to-haves
- Alerts/notifications for expiring or at-risk option positions.
- Reporting/export — CSV export and periodic performance reports.
- Multi-leg spread tracking — model a multi-leg strategy (vertical, condor, etc.) as one position instead of individual legs.

### Out-of-scope
- Multi-user accounts or authentication — this is a single-user personal tool.
- A mobile app.
- Brokerage account integration or auto-import of trades — all entry is manual.
- Tax-lot tracking or tax reporting.

## User Stories & Acceptance Criteria

| User Story | Feature | Summary |
|---|---|---|
| [Add and manage stock holdings](prd/add-and-manage-stock-holdings.md) | Stock holdings CRUD | Add, edit, and delete a stock holding |
| [Track live stock price and unrealized P&L](prd/track-live-stock-price-and-unrealized-pl.md) | Live stock pricing & unrealized P&L | See current price and computed P&L update without manual entry |
| [Close a stock holding and record realized P&L](prd/close-a-stock-holding-and-record-realized-pl.md) | Stock realized P&L / transaction history | Closing a holding computes and records realized P&L |
| [Add and manage option trades](prd/add-and-manage-option-trades.md) | Option trades CRUD | Add, edit, and delete an option trade |
| [Track live options pricing](prd/track-live-options-pricing.md) | Live options pricing | See current mark price for an open option position |
| [View DTE, open P&L, and ROI for an option position](prd/view-dte-open-pl-and-roi-for-an-option-position.md) | Options DTE, open P&L, and ROI | Computed fields update as price and time move |
| [Roll an option position](prd/roll-an-option-position.md) | Options rolling | Roll an open position to a new strike/expiration |
| [View greeks for an option position](prd/view-greeks-for-an-option-position.md) | Options greeks | See delta/theta/gamma/vega for an open position |
| [Close an option trade and record history](prd/close-an-option-trade-and-record-history.md) | Options closed-trade history & total P&L | Closing a trade records realized P&L/ROI to history |
| [View the portfolio dashboard](prd/view-the-portfolio-dashboard.md) | Portfolio dashboard | See combined stock + options totals at a glance |

## Success Metrics (KPIs)

| Metric | Target | How measured |
|---|---|---|
| Data accuracy | Displayed P&L matches the broker statement (within rounding) for 100% of spot-checks | Manual spot-check against broker statement, monthly |
| Price freshness | Prices for open positions refresh at least every 30s while the app is open during market hours | Poll interval configuration / logs |
| Task speed | Adding or editing a position takes under 30 seconds from opening the form to it being saved | Manual timing / usability check |
| Active usage | App is opened and used on every trading day the user holds an open option position | Self-reported / session log |

## Related
