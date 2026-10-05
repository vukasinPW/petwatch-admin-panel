# PS Finance tab

Status: captured 2026-08-18. Logic only.

App Design: `fFkKBQPGIaM1Zjk9dz7LUW`

| Topic | Node |
|---|---|
| Finance section | `25700:218013` |
| Main screen | `21565:164694` |
| Time range | `21565:164213` |
| Empty / first / regular | `21565:164934` |
| View all payouts | `21565:165440` (also Live `21565:163708`) |

**PS only.** Bottom nav: Home · Messages · Bookings · **Finance** · Profile.

**No Finance for PO.** Owner pay is checkout (Mamo) on booking — `booking-po-general.md`. No receipts / wallet / refund UI in the app for owners.

---

## Why it exists

Sitters see **earnings, payouts, and booking volume** for a selected period, plus **when money goes to their bank**.

Not a wallet. Sitters **cannot** withdraw. Money is **pushed automatically once a month** to the approved IBAN.

Bank destination = IBAN from verification. Change IBAN = Help Center, not this tab (`ps-profile.md`).

---

## Money (product, not Figma copy)

- **Automatic monthly payout**, typically on the **1st of each month** (product 2026-08-24). Canvas says “every two weeks” — **not product**.
- **Available balance** and **Next payout** are the **same number** (same pot). No separate pending/held bucket **after** completion.
- A finished job is **added to that pot immediately** (as soon as the session is completed). Working assumption from product — not a confirmed hold/T+n rule. Change if ops later adds a delay.
- Before completion the owner's money sits in **escrow** (product 2026-08-25, [admin-finance.md](admin-finance.md)). That is **admin-only** — the sitter never sees escrow, because completion is exactly when the money becomes theirs. Nothing on this tab changes.
- No failed-transfer / retry / notify flow yet. Do not design it.
- Refund / cancel vs this balance: **out of scope** for now (refunds will exist later — `booking-po-general.md`).

---

## Main screen (regular)

- Header: Finance / track earnings, payouts & bookings.
- **Available balance** + amount. Subline: **Next withdraw on {date}** (next monthly send).
- Two KPI chips: **Earning** (amount + % trend) and **Nm. of bookings** (count + % trend). First-ever period draws **100%**.
- Period control: **Valuable insights** / **Last 30 days**. Canvas only shows that range — other presets **UNKNOWN**.
- **Earning over time:** daily **gross** for the selected period. Total + daily avg. Empty still draws the chart shell with no series.
- **Payout** card: next payout (same amount + next date). Last payout (date + amount). **View all**. Empty: **No payout yet**.
- **Revenue breakdown / By service type:** share of total by SKU family (walking, boarding, sitting, home visit, cat boarding, cat sitting). Empty: explainer + **0 total**. First job: one family with 1 service.

Currency on canvas is a bare number (e.g. 1,200). Treat as **AED** unless product says otherwise.

---

## Payout list (`View all`)

- Title Payout.
- **Next payout** pinned at top (amount + next monthly date).
- History rows: date + amount.
- Empty list: **No payouts yet**.

No per-booking ledger, invoice PDF, or failed-payout row.

---

## States drawn

| State | Balance | KPIs | Payout card | Breakdown |
|---|---|---|---|---|
| Empty | blank + still shows next-withdraw date | blank | No payout yet | 0 total + explainer |
| First service | small amount (55) | 100% | next payout, no last | one family, 1 service |
| Regular | 1,200 | 23.3% on both chips | next + last | split by family |

Tab is for **PS**. Empty state is drawn (sitter can open Finance with no jobs yet).

---

## Reuse (already locked elsewhere)

- Prices are **platform-fixed**; this tab reports what was earned, not what the sitter sets.
- IBAN read-only; change via Help Center.
- PO pays with **Mamo** at booking create. No PO finance surface.

---

## Admin hooks

- Admin Payouts is the **company** view of the same monthly run: **upcoming run pinned at top** (amount + date), then past months, then sitters in a month ([admin-finance.md](admin-finance.md)). This tab stays one sitter, date + amount.
- Monthly payout run + next-run date shown in-app.
- Same amount as the sitter’s available / next payout.
- IBAN on file = payout destination (verification + Help Center change).
- Per-sitter earnings / booking counts / mix by service family (mirrors this dashboard).
- Platform money hub (pay-in, escrow, payouts, refunds, totals) is **admin Finance** — [admin-finance.md](admin-finance.md). Intent 2026-08-24, not locked. Sitter tab rules above do not change until product says they do.

---

## Still unknown

- Immediate-on-complete is a **guess** — confirm if a hold appears later.
- What the KPI % compares to (previous 30 days?).
- Period options besides Last 30 days.
- Currency / tax / invoices (not drawn).
