# Admin Finance (platform money)

Status: restart 2026-08-25 — previous clone draft **deleted**. First screen is an **overall Finance dashboard** (not statistics). Not locked.

**PS Finance tab** in the app stays as captured in [ps-finance.md](ps-finance.md). Owners still have **no** finance surface in the app ([INDEX](../INDEX.md)). This file is the **admin** money hub.

---

## Why it exists

Ops needs one place for **all money that moves through the app**: owner payments in, **escrow**, sitter earnings, monthly payouts out, company take, refunds, averages and totals.

Not the same as the sitter’s Finance tab (one sitter, available = next payout, no withdraw). Not the same as booking **Refunded** labels (manual record on booking/session).

---

## Locked (product 2026-08-24)

Admin Finance tracks **all money flow** in the app:

- **All owner payments** (Mamo at booking create → Confirmed).
- **All payouts.** One payout cycle per month, typically on the **1st**. Sitters still cannot withdraw ([ps-finance.md](ps-finance.md)).
- **Totals**, all of these, not one number:
  - **Total payments** — what pet owners paid (GMV).
  - **PetWatch earnings** — PetWatch take.
  - **Pet sitter earnings** — credited to pet sitters (available / next-payout pot in the app).
  - **We pay / payouts** — cash actually sent to IBANs.

Do **not** assume failed-transfer retry, clawbacks, tax, or invoices until product asks. IBAN approve/reject stays **Mamo**, read-only in admin ([ps-verification.md](ps-verification.md)).

---

## Taken from the app (not re-asked)

- Owner pay is checkout only. No PO finance tab, no owner receipts/wallet.
- Prices are **platform-fixed**. Promo: one code per trip (invalid / expired / already used).
- Sitter Finance: no wallet; **available = next payout**; finished session **added to that pot immediately** (working guess, not T+n). No per-booking ledger in the app.
- Payout destination = approved IBAN (verification + Help Center change).
- Booking **Refunded** is a **label** on the booking/session. Finance now has a real refund list (Mamo + statuses). Whether the label creates that row: **UNKNOWN**.
- Pay success/fail exists at checkout. FigJam has a **failed charge** transaction type.
- Transactions cluster on the map is **read-only**. Payouts cluster has **notes** + **export** only (no trigger/hold on the map).

---

## Screens

Board: [Admin Panel — Screen Map](https://www.figma.com/board/ZvOWTgEbuXGidiMGNK1QGN).

**Build order (restart 2026-08-25):** one screen at a time. Do **not** clone Bookings and retarget.

**First:** [Finance — Dashboard](https://www.figma.com/board/ZvOWTgEbuXGidiMGNK1QGN?node-id=98-502) — overall look at company money. **Not** a statistics page.

In Figma: Design page → **Finance - Overview** (`7432:73211`), **Finance - Payouts** (`7512:63015`), **Finance - Payouts - August 2026** (`7538:66309`). Not green on FigJam.

**Overview is a landing only.** It links into three child lists. Do not keep adding metrics here. VAT, fees, aging, blocked IBANs belong on those later screens if they appear at all.

Child sections (product 2026-08-26). Payouts year list is drawn (`7512:63015`). Sitters-in-month is drawn (`7538:66309`, dummy August 2026). Transactions and Refunds lists are drawn.

**1. Payouts** (`6:200`) — year list: [Finance - Payouts](https://www.figma.com/design/rc6tFk9QGVqOFD3ht9Upt8/Admin-Panel?node-id=7512-63015) (`7512:63015`). Two levels, not a flat sitter table. Same pin as the sitter’s View all ([ps-finance.md](ps-finance.md)).

- **Upcoming payout pinned at the top** — next 1st, **how much will go out**, how many sitters. It sits in this list before money sends (not only on the overview banner).
- **Below:** past monthly runs. One row per **calendar month** (e.g. August 2026, company total, sitter count).
- **Open a month** → sitters in **that** run. Product 2026-08-26: whatever belongs to August is in the August run and is sent as August. Do not put July’s work inside August.
- Per-sitter payout history on the sitter profile stays. This list is the **company** run.

**Sitters-in-month** (product 2026-08-31). One payout cycle. Snapshot + sitter list. Third grain is a **popup** on that list (product 2026-09-01), not a later included-bookings page.

Snapshot (4): **bookings** (count) · **earnings** (AED sent to pet sitters) · **pet sitters** (count) · **date** (when this run sends / sent). Not a through-time chart.

List grain = **sitter**. Row has the details for that sitter in this run (name, bookings in the run, amount, status). View → **payout detail popup** for that sitter in this month.

**Payout detail** (product 2026-09-01). Popup on the sitters-in-month list, not a full page. Ops **see only** — no edit, no retry, no IBAN.

Fields: **sitter** · **paid** (AED to this sitter in this run) · **date** (the run date) · **bookings** (count) · **sessions** (count) · **ratio** (sessions per booking). A one-day booking with one visit is still one session. Do **not** list the bookings or sessions. No IBAN. Not a 2-column profile-report grid.

August table/snapshot stays **Bookings** for now (product 2026-09-01). The popup shows **both** counts plus the ratio — do not retitle the month list yet.

**Didn’t receive** does **not** open this popup (product 2026-09-01). View is **Paid sitters only**. Failed sitters stay on the August list (pin, filter, status + reason). No extra overlay.

**Didn't receive** is a real status (product 2026-08-31). Some sitters in the run do not get the money — bank / IBAN: none on file, Mamo rejected, or the send failed. Exact reason enum **UNKNOWN** (examples, not locked). Placement (product 2026-08-31): **pin above the table** (count + amount not sent) **and** a Paid / Didn't receive filter. Status + reason on the row. Ops **see it only** — no retry, skip, or drop from the run. IBAN approve/reject stays Mamo; admin still cannot fix the bank.

Snapshot **earnings** = AED **sent to pet sitters** this run (same number as that month on the year list). Not pet owner payments.

**No edit** on this page (product 2026-08-31). Date, amount, and who is in the run are read-only. Ops cannot reschedule the send from admin.

**2. Transactions** (`6:229`) — one ledger of **every money movement**. Not grouped by month. Not the refund queue.

- Filters: **positive** (money in) · **negative** (money out) · **failed**. Charge / refund / payout still exist as types; they sit behind these filters.
- A **Completed** refund also lands here as type Refund (money actually went out). **Requested** and **Canceled** do not — nothing moved.
- Read-only on the map (export only).

**3. Refunds** (`103:504`) — **keep split** (product 2026-08-30). This is the **request queue**, not a second ledger. Money goes back through **Mamo**.

Legal source (product 2026-08-30, [refund-policy](https://petwatchapp.com/legal/refund-policy/) + [cancellation-policy](https://petwatchapp.com/legal/cancellation-policy/)). Refund policy is **owners only**. Amounts follow cancellation fees. Read together.

**Three paths to a refund** (legal):

1. **Owner cancels a Short service** (< 24h) — more than **2 hours** before start: eligible. 2 hours or less: **no refund**, full charge.
2. **Owner cancels a Long service** (24h+) — >24h: full (no fee). 24h–2h: AED 30 fee withheld. Within 2h of start: first-day amount + AED 30. After start, remaining days: **partial** if canceled ≥2h before the next cycle; else that day + AED 30, later days refunded.
3. **Disputed completed service** — owner files within **7 days** of the service date. PW investigates 30–90 days. Refund only if the dispute is proven, **PW discretion**. Platform chat only.

Also: PW cancels → no cancellation fee. Sitter cancel is **not** an eligibility case on the refund page — in the app the owner then picks refund vs substitute ([booking-live-session.md](booking-live-session.md)).

Processing (legal): min **2 weeks**; back to the **same** payment method; card/gateway 14–45 days. Gateway/bank fees are **not** reversed. Full vs partial is PW discretion once a path above is met.

- **Grain follows the cancel:** whole booking canceled → one refund for the **booking**. One session canceled → one refund for that **session**. Both appear in the same list. Row says which it is.
- **Statuses** (working names, not copy-locked): **Requested** → **Completed** (Mamo sent it back) → or **Canceled** (someone asked, then they cannot get it). Past refunds stay on the list; status is how you tell them apart. **Requested** is why this list exists separately.
- Do not duplicate the booking breakdown here. Booking still has the quiet **Refunded** label.
- **Refund logic parked** (product 2026-08-26): who flips statuses, whether Mark for refund creates this row, refund after money left escrow — discuss with the team. Do not block the list screens on it.

**Refund detail** (product 2026-09-01). A **popup** on the Refunds list, not a full page. Drawn: `Finance - Refunds - Detail` (`7562:94663`). List **View** opens it. Ops **review + add a note** only — no edit amount, no fire Mamo, no change destination.

Fields: refund **ID** · booking **or** session (link to the existing Bookings page) · **owner** · **requested** at · **sent** at (empty while Requested) · **status** · **canceled by**. Destination is the **original payment method**, read-only (card last4 / Apple Pay / Google Pay) — **not** an IBAN.

**Amount is a 3-way split:** full charge · withheld (fee / not returned) · refunded. Note is for why that split is what it is (edge cases). Visual: not a 2-column label/value “profile report” grid.

**App vs legal window:** app copy still says Short = **1 hour** ([booking-po-general.md](booking-po-general.md)). Legal says **2 hours**. Not reconciled.

Working click-through from overview (not locked): next-payout banner → that month’s payout; Payouts / Transactions / Refunds are the three places you leave this page for.

Money that stays **outside** Finance pages: PO Financial Info tab · sitter Payout History · booking costings / split earnings / payment attempts · Analytics Revenue.

---

## Relation to the sitter tab

Still true on the sitter tab ([ps-finance.md](ps-finance.md)) and unchanged by escrow:

- No wallet, no withdraw.
- Available balance **=** next payout (same pot). No pending bucket **after** completion.
- Finished job **added to that pot immediately** — that is the moment money leaves escrow.
- Refund / cancel vs that balance: **out of scope** on the sitter tab.

Booking ops today ([booking-po-general.md](booking-po-general.md)): **Refunded** is a quiet **label**. Actual payout reversal is outside the booking panel.

---

## Money states

**Escrow is real** (product 2026-08-25). Three stages:

1. PO pays (Mamo) → money is **in escrow**. PetWatch holds it; the job is not done. Fail → **failed charge**. The owner pays the **full amount upfront** whatever the duration — a six-month repeating booking is paid in one go at create ([booking-po-general.md](booking-po-general.md)). Escrow is therefore a **long-lived balance**, not a short buffer, and grows with the book of future work.
2. Session **completes** → the amount leaves escrow and is **credited to the sitter** (the app's available / next-payout pot). Company take is the gap vs owner pay (promo **UNKNOWN**).
3. **~1st of month** → **payout** to approved IBAN.
4. **Refund** — money returns through **Mamo**. Finance list tracks the request. Grain = booking or session, matching what was canceled. Refund out of **escrow** (job not done) is the clean case; refund after the money already moved to the sitter pot or was paid out: **UNKNOWN**. Booking **Refunded** label still exists; it is not the money movement.

This does **not** contradict [ps-finance.md](ps-finance.md). The app's "no pending bucket, credited immediately" rule describes what happens **after** completion. Escrow sits **before** completion, and the sitter never sees it — money they cannot earn yet is not on their tab.

Escrow is admin-only. Do not add an escrow surface to the sitter or owner app.

**Working assumption (2026-08-25, not yet confirmed by finance):** escrow sits in a **separate account**, not mixed with operating money. Two consequences:

- The escrow figure is **verifiable**. The overview can show calculated escrow against the account balance, and flag a mismatch. A mismatch means something moved without a record (unlogged refund, manual transfer, failed send).
- Moving money out of escrow is a **real transfer**, not just a ledger entry — escrow → sitter IBAN on payout, and escrow → operating for company take. That implies a **fifth movement type** (internal transfer) beyond the four on the FigJam Transactions cluster (charge · refund · payout · failed charge). Do not add it to the map until finance confirms the separate account.

---

## Admin hooks (intent)

- Platform totals on the **dashboard** first, then lists.
- Same monthly run + next-run date the sitter already sees.
- Per-sitter payout history on the sitter profile stays.
- Booking still owns bag + **Refunded** label. Finance owns the **refund list + Mamo statuses**.

**Ops can / cannot** on money (trigger payout, hold, fire the Mamo refund): **parked** with refund logic. Transactions stay read-only on the map.

---

## Overview screen (product 2026-08-25)

Hero is **company take** — what PetWatch actually earns. That is the most important number on the page (product 2026-08-25). Money in (owners paid) stays on the card as the secondary number, because take rate needs both, but it does not get the big type.

**Layout (product 2026-08-26):** 2×2 grid of tinted metric cards on the left, earnings-over-time chart card on the right. Reference is a tinted-card dashboard, not the standard four-across `General info` row used on every other admin page — Finance overview is deliberately the one page with a landing-page look. Tinted cards map to `Surface/*/Light`; the chart card reads as Success `#23a9af`.

The four cards:

| Card | Shows | Period-driven |
|---|---|---|
| Total payments | What pet owners paid in the period | Yes, with trend |
| PetWatch earnings | PetWatch take | Yes, with trend |
| Pet sitter earnings | Pet sitters' share | Yes, with trend |
| In escrow | Held now for work not yet done | **No** — stock, no trend |

Period presets: today / this week / this month / total. The control governs the three flow cards and the chart only — it is a normal control, no special interaction.

**Next payout is a banner**, full width under the grid: date · amount · number of sitters in the run. Drawn on **Finance - Overview** (`7422:56869`). View opens that month. Below: three section cards — **Payouts**, **Transactions**, **Refunds** — View goes to those lists. Period control is **today / this week / this month / total** in the header (This month selected). Not inside the chart.

**Chart:** stacked — PW on PS, summing to Total — so it reconciles with the cards beside it and shows take rate over time. A single flat earnings line only repeats a card.

**Escrow is not the payout pot.** Escrow = job not done, money cannot go anywhere yet. Ready to pay out = job done, money is the sitter's, waiting for the 1st. Only the **ready** pot goes out on the 1st. Money in escrow for future sessions stays in escrow across payout runs. Two cards, never one.

The two blocks must reconcile: money in = company take + sitters' share, for the same period. Held = escrow + ready to pay out.

Not on this screen: by-service / by-emirate / month-over-month breakdowns. Those are the Statistics pages.

---

## Still unknown

- Sitters-in-month: exact **Didn't receive** reason labels (no IBAN / Mamo rejected / send failed are examples).
- **When company take splits off** — at payment (escrow holds only the sitter share) or at completion (escrow holds the full owner payment). Working read: escrow holds the **full** owner payment and splits at completion, so escrow = money we hold.
- **Escrow aging** (how long money has been sitting) — un-parked 2026-08-25. Full upfront payment on bookings up to ~6 months means escrow can hold money for months. Worth showing on the overview.
- Promo: reduces GMV, company take, or both.
- **Refund logic** (who can do what, Mark for refund → Finance row, refund after escrow) — parked for the team. List UI can proceed.
- **Short cancel window:** legal refund/cancellation = **2 hours**; app copy = **1 hour**. Which is live.
- Whether a **dispute** is a Refunds-list row (path = Dispute) or stays off this list until PW approves.
- What ops can **do** besides notes/export (hold an escrow release? nothing on the map yet).
