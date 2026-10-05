# Admin Promo codes

Status: list + snapshot locked 2026-08-31. Create rules locked 2026-08-31 (discount, window, publish). Statistics drawn 2026-09-04 (`7615:97879`). Limits + audience: parked for now — not on Statistics. Deactivate confirm: out of scope. Not the app checkout flow — that stays in [booking-po-general.md](booking-po-general.md).

Admin-Panel: `rc6tFk9QGVqOFD3ht9Upt8`  
FigJam cluster: `9:344`

| Screen | Node | State |
|---|---|---|
| List (table) | `7558:66281` | Drawn (designer) |
| Add new | `7558:66322` / `7558:66378` | Drawn — dropdowns open; do not restyle |
| Edit | `7558:67975` | Drawn — do not restyle |
| Detail (Active) | `7561:66695` | Drawn — `WELCOME20` |
| Statistics | `7615:97879` | Drawn 2026-09-04 |
| Deactivate confirm | — | Out of scope |

App still: one code **per trip**; errors invalid · expired · already used. Applied at checkout (after address, before pay).

---

## Why it exists

Ops/marketing need one place to **see every code**, create/edit/deactivate, and glance at whether promos are actually used. Not a campaign analytics suite. Not Finance (who eats the discount is still UNKNOWN there).

---

## List (home)

Same shell as sitters/bookings: title · tabs · 4 KPI cards · segmented filter · table · Add new. **No card view.**

Tabs: **Table** | **Statistics**. Statistics is a sibling screen, not charts on this page.

Segmented: **All** · **Active** · **Expired** · **Deactivated**.

Header: Export table · **Add new**. Row eye → detail. Pencil / **Edit settings** on detail → Edit page (`7558:67975`). Deactivate lives on Edit (**Delete** on that frame) + confirm, not a primary row delete.

### Snapshot (4 cards, `General info` Property 1=4)

All cards use the 2-secondary layout (same height as sitters). Period secondaries are **this month** unless noted.

| Card | Big number | Secondary | Chip | Icon |
|---|---|---|---|---|
| Total codes | all codes | Active · Expired | Dark blue | `tag` |
| Times used | redemptions (bookings that paid with a code) | This month · Unique pet owners | Info | `activity` |
| Saved | owner discount given (AED) | This month · Avg / use | Success | `percent` |
| Payments with promo | GMV of those bookings (AED) | This month · Promo bookings | warning | `credit-card` |

Deactivated is **not** a KPI pile — it is a filter + table status. Expired is automatic (valid-until passed). Deactivated is ops turning a code off.

**Saved** is what the pet owner did not pay. **Payments with promo** is what they still paid. Do not add them together. Who funded Saved (take vs sitter vs split): **UNKNOWN** — the card still shows the owner discount.

### Table columns

Code · Discount · Status · Valid until · Uses · Saved · Created · Actions.

Discount is **% or AED** (product 2026-08-31). Status pills: Active (success) · Expired (warning) · Deactivated (neutral). Valid until can be empty = until ops turns it off.

---

## Statistics

Sibling of the list (`Table` | `Statistics`). Not the `WELCOME20` detail. Not Finance. Not incrementality / ROI / margin / who funds the discount.

**Job (locked 2026-09-04):** which codes get used, how usage moves over time, how much discount we gave, GMV of those trips.

**Use (locked 2026-09-04):** a trip that **paid** with a code. One code per trip → one use per booking, not per session. Canceled / refunded **after pay** still counts. Never-paid does not.

**First-time vs repeat (locked 2026-09-04):** first time **this owner used any promo**, vs they have used a code before. Not first paid booking.

**Period (locked 2026-09-04):** same as Notifications — This week · Last week · This month · Last month · Between. Default This month. Drives every chart and the three period KPIs. No All / Active / Expired / Deactivated on this page.

**KPI row (locked 2026-09-04):** same four cards as the list. **Total codes** = inventory (not period). **Times used** / **Discount applied** / **Payments with promo** = this period.

**Units (locked 2026-09-04):** ranking, emirate, service, and % vs AED are all **uses** (trip count). Ranking = top codes by uses. % vs AED = share of uses, not share of AED given.

**v1 panels (locked 2026-09-04):** through time (one panel: **Times used** + **Unique pet owners**) · most-used ranking · first-time vs repeat · by emirate · by service (Walking · boarding · sitting · home visit · mixed) · **% vs AED**.

**Through time (locked 2026-09-04):** one panel, two lines, both counts — Times used · Unique pet owners. Money stays on the KPI cards (not a second time chart).

**First-time vs repeat count (locked 2026-09-04):** **unique owners**, each person once. If their first-ever promo use falls in this period, they are First-time — extra uses that month do not move them to Repeat. Repeat = owners whose first promo was **before** this period.

**Parked — do not draw:** failed applies (invalid / expired / already used). **Promo vs none** stays on booking stats (P3), not a headline here.

Drawn 2026-09-04: `Promo Codes - Statistics Dashboard` (`7615:97879`), right of the list. Same chrome. Statistics tab selected. Period **This month** on Uses through time (drives the page). No All / Active / Expired / Deactivated. Dummy this month: **214** uses · **168** unique owners.

---

## Detail (one code, Active)

Drawn 2026-09-01: `Promo Codes - WELCOME20` (`7561:66695`). Breakdown only — not Statistics, not the edit form.

Dummy: **WELCOME20**, Active. **Edit settings** goes to Edit (`7558:67975`).

Same four piles as the list, scoped to this code:

| Card | Big number | Meaning | Secondary |
|---|---|---|---|
| Times used | redemptions | How many bookings paid with this code | This month · Unique pet owners |
| Unique pet owners | distinct pet owners | How many pet owners it applied to | This month · Repeat (extra uses) |
| Discount applied | owner discount AED | Saved | This month · Avg / use |
| Payments with promo | GMV of those bookings AED | What pet owners still paid (not Saved) | This month · Promo bookings |

Do not add Discount applied + Spent. Who funds the discount: still UNKNOWN.

No settings fields — those stay on Edit.

### Booking usage log

Same page, under the snapshot. Every booking that paid with this code (one code per trip). Eye → booking detail. Dummy first page of 412.

Columns: Booking · Owner · Status · Dates · Service · Saved · Total · Actions (View only).

Status is **booking** status (`Booking status`), not code status. Search / Filters / Sort / Export stay. No Add new. No card view.

---

## Statuses

| Status | Meaning |
|---|---|
| Active | Redeemable now (create publishes live — no draft) |
| Expired | Valid-until passed. If there is **no** end date, this never fires — only deactivate. |
| Deactivated | Ops turned it off. Keep usages. |

No hard **delete** on a code that has usages — same idea as not deleting a sitter with open bookings. FigJam already has deactivate confirm.

---

## Create (locked 2026-08-31)

**Add new** publishes. No draft. Default start = now → **Active**.

| Field | Rule |
|---|---|
| Code | What the owner types. Unique. |
| Discount | **Percent or AED** (both exist). One value per code. |
| Start | Now (default) or a date. |
| End | A date **or** until ops deactivates (no end). |

One code per trip still applies in the app.

Limits and audience are **separate**. Date range is the window above, not a limit type.

### Limits (how many times it can fire)

Stack is allowed: global cap **and** per-owner cap.

| Limit | Meaning |
|---|---|
| Unlimited | Until end date or deactivate |
| First N | Global cap (e.g. first 500 redemptions) |
| Per owner | Once, or X times |

Not limits (those are audience): first booking, new sitters, species, booking count.

When First N is hit: **UNKNOWN** (auto-off vs stay Active and reject).

### Audience (who can redeem)

Filters **AND** together. Default = anyone (no rows).

Create is a **full page** (not a 760 overlay). Designer lock 2026-08-31 (`7508:69820`): do not restyle.

| Block | Control |
|---|---|
| Code | text |
| Discount | value + type (Percent / AED) in one row |
| Date range | Start · End · **Until I turn off** (hides end when on) |
| User preferences | repeating type + value + add (limits, e.g. First X users · 500) |
| Additional preferences | repeating type + value + add (audience). Empty = anyone |
| Actions | Cancel · **Save** |

Default = no additional-preference rows = anyone. Later types join the same type dropdown — layout does not change. Checkout already rejects invalid / expired / already used; extra rules fail the same gate until product asks for a specific error.

**v1 types:** First paid booking · Dog owners · Cat owners · At least X completed bookings · Fewer than X completed bookings.

**Later types (same dropdown, not a new overlay):**

| Type | Value |
|---|---|
| Emirate | one or more emirates |
| Service family | walking / boarding / sitting / home visit |
| Min trip value | AED |
| No booking in X days | winback |
| Account younger than X days | not the same as first booking |
| Named owners | search + chips (VIP / influencer) |

Named owners is still a rule row — only the value control is a people picker, not a number.

**New sitters** is not an owner checkout filter until product says what it means (sitter-facing code vs owners booking a newly approved sitter).

---

## Still unknown

- v1 cut of audience + whether First N auto-turns the code off.
- What **new sitters** means on an owner promo.
- Who pays: take vs sitter vs split ([admin-finance.md](admin-finance.md)).
- After live: edit value/dates vs deactivate only. Refund → does the use return.
- Future start date vs list status (Scheduled, or Active but not redeemable yet).
