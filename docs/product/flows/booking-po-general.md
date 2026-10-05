# PO Booking — General

Status: captured from Figma 2026-08-18. **PO side only.** Logic, not copy.

App Design: `fFkKBQPGIaM1Zjk9dz7LUW`

This is the create / search / pay / details spine. Later PO booking parts (if any) add on top.

| Topic | Node |
|---|---|
| Bookings tab empty / filled | `20389:121706` |
| Single dog, one service, one-time | `23724:499300` |
| Single cat, one service, one-time | `20467:167554` |
| Multi pet, mixed services (split walks, visit+walk) | `20467:188638` |
| Multi pet, same services (board+board, sit+sit, together walks, visit+visit) | `20467:192937` |
| Boarding + walking or boarding + visit | `20467:202422` |
| Repeating schedule | `20467:208271` |
| Flexible start time | `20616:187648` |
| One-time, consecutive days | `21245:105097` |
| FDT + repeating | `20248:293421` |
| PS declined | `20389:124669` |
| Combination limits | `20241:279832` |
| Duplicate-request error | `20389:128467` |
| Payment | `21382:165386` |
| Pet-care checklist | `20389:129051` |
| Address at checkout | `20389:134884` |
| Filters | `20389:135107` |
| Search variations | `20248:331323` |
| PO viewing PS profile | `20248:330658` |
| Edit booking from search (1 pet / multi) | `20515:198577`, `20515:199005` |
| Promo code | `23111:172005` |
| Search / favorite sitters | `23724:557573` |
| Report a problem | `23737:178829` |
| **Sitter-first create** | `20467:208639` |

---

## Gate (Bookings tab)

Same as Home: cannot book until **identity verified** + **approved pet**.

| State | Bookings tab |
|---|---|
| Not verified | Empty + must verify + create pet |
| Verified, no pet | Empty + create pet |
| Ready, no bookings | Empty list |
| Has bookings | Cards: date/time, status, services, pets, sitter, View details / Contact sitter |

Multiple pets **can** share one booking.

---

## Happy path (one pet, one main service, one-time)

1. Pick service family (walking / boarding / sitting for dogs; home visit / boarding / sitting for cats) → duration SKU (30/60, day/night/daily).
2. Optional **add-ons** (same catalog as sitter setup; prices platform-fixed).
3. **Date & time:** frequency **One time** vs **Repeating schedule**; one-time is **single day** or **multiple / consecutive days**; native time picker. **Flexible start time** = a **window** (e.g. morning walk — 8, 9, or 10 is all fine). The window is the constraint, not a single clock time. On **multi-session** bookings, each session can land at a **different** time inside that window (Mon 9:00, Fri 10:00). Full FDT UI still to be shared.
4. Summary (pets, SKUs, add-ons, when) → address (saved or add first-time / new) → **promo** (optional) → **pay**.
5. Request goes to **exactly one sitter** the PO chose. No broadcast.

CTA on create is **pinned to the bottom**.

Search sitters (name, recent, filters) can happen after the service/time bag is set. PO can **edit** that bag from search (single or multi pet) without restarting from zero. **Book sitter** from a result. PO can open the **public sitter profile** (about, distance, map, reviews, gallery, house rules/facilities, experience).

---

## Two ways to start (PO)

Same booking object, same combo/pay/status rules. Only the **order** changes.

### A — Service first (General above)

Home **Book service** (or Services) → pets & SKUs → date/time → search/filter sitters → pick **one** sitter → pay.

### B — Sitter first (`20467:208639`)

Home **Book sitter** / **Book your favorite sitter** → **pick the sitter first** → then services → date/time → summary (sitter is already on the summary, **Edit**) → pay.

Sitter picker:

- Tabs: **All sitters / Favorite sitters / Recent sitters**
- Search by name
- Empty favorites: heart on the public profile
- **Recent** = sitters from about the **last 5 bookings** (even if not favorited) — canvas intent, so they can repeat without remembering the name
- **View profile** or **Book sitter**

After the sitter is locked, the rest of the wizard is the same **shape** as path A (one-time or repeating; repeating asks for **at least 2 weekdays**), but **scoped to that sitter**:

- Only **services they offer**
- Only **dates/times they are available**
- Request still goes to **that one sitter**

**No swapping sitter mid-flow.** Figma **Edit** next to the sitter on summary is **not** a sitter change. To use someone else they start over from Book sitter.

---

## Frequency

- **One time** — one day, or several consecutive days (each day becomes a **session**).
- **Repeating schedule** — date range + weekdays (e.g. Mon, Tue). Sessions listed on booking details (Upcoming / Next / Live / Completed). When the **last session** is done, the booking completes.

FDT + repeating is drawn (`20248:293421`). Same window logic: repeating days can each start at different times **inside** the window.

---

## Multi-pet combination rules (product — live)

Canvas notes, confirmed:

1. **One pet = one main service.** A pet cannot have two main SKUs on the same booking (no boarding + walk on Luna). **Add-ons** still attach to that one main. Combos are **across pets**, not stacked on one pet.
2. **Sitting only with sitting.** If one pet has sitting, other pets cannot have boarding / walk / visit on that booking.
3. **Boarding** only combines with **walking**, **home visit**, or **the same boarding SKU** (day care with day care — not daily/night mixed). Same idea for sitting SKUs: only the **same** sitting variant together.
4. **Boarding + max 3 small services** (walks/visits) on the booking.
5. **Walk together** question appears only if **dog walking for 2+ dogs**. If durations differ (30 vs 60), together is **blocked** — auto **separate**; tapping together shows an error.
6. Walk-together question does **not** appear for mixed visit+walk etc. unless it’s multi-dog walking.

---

## Duplicate request

Cannot send **another request for the same pet, same service, same date & time**. Inline error; change details or open existing booking.

---

## Statuses (PO)

Labeled statuses: **Requested**, **Accepted**, **Confirmed**, **Live**, **Completed**, **Declined**, **Canceled**.

**Confirmed** is when the owner **pays**. For grouping it is the same pile as **Live** — Live is Confirmed that has **started**. **Accepted** is only when the sitter accepts the request (not Confirmed). How pay sits vs Accept in time is **UNKNOWN** if it disagrees with checkout-first; treat Confirmed as nearer Live than Requested.

**Ready** = about to start (before Live). Product: it exists. **Do not label** it in admin snapshot/filters until asked.

**Live** = sitter picked up / service started. Also **Declined** (sitter, **no reason** to the PO) and **Canceled**.

Pickup on the pet card: **Not picked up** / **Picked up** / **Dropped**.

**Finish is sitter-only in the app** (owner does **not** confirm). When the sitter drops/finishes, the session/service is **done**. Old frames that ask the owner to confirm are not product. **Ops can Finish** a **session** or a **service** if the sitter did not — not the whole repeating series in one tap. **Ops cannot Start.**

**Cancel:** both PO and PS. Repeating / continuous-day: can cancel a **session**. Refund **money** is Mamo, tracked on **admin Finance** ([admin-finance.md](admin-finance.md)): booking cancel → booking refund; session cancel → session refund. Statuses: Requested / Completed / Cancelled. Booking panel still has the quiet **Refunded** label; whether that label creates the Finance row is **UNKNOWN**.

PO has **Cancel session** and **Cancel booking** as separate actions on the booking (`21377:160841`). Both run: confirm sheet (with the fee policy below) → **required reason** (same 8 options as PS; *Other* opens a free-text field) → success. Success CTA is **Book another sitter** / Go back home. PS session cancel is captured in [booking-live-session.md](booking-live-session.md).

**Cancellation fees (app copy, `21019:206462`).** Money is not an admin action, but the fee rules explain what ops sees:

- **Short service** (< 24h, e.g. walking): no fee if canceled **more than 1 hour** before start; **full charge** at 1 hour or less.
- **Long service** (24h+, e.g. multi-day sitting): no fee if canceled **more than 24 hours** before start; **AED 30** between 24 and 2 hours before.
- **After start, multi-day:** remaining days can be canceled by notifying at least **2 hours** before the next cycle; otherwise **AED 30 + that day's full amount**, and subsequent days are refunded.

Legal site (product pointed here 2026-08-30, [refund-policy](https://petwatchapp.com/legal/refund-policy/) + [cancellation-policy](https://petwatchapp.com/legal/cancellation-policy/)): Short window is **2 hours**, not 1. Long and after-start match. Refund eligibility and dispute path live in [admin-finance.md](admin-finance.md). **Not reconciled** — do not assume the app copy is wrong until product says the site wins.

Popups + push (same pattern):

- Sitter **accepts** → PO sees it on next open.
- Sitter **picks up** (service starts) → same.
- Service **done** → completed screen on next open.

---

## Pay

**Mamo.** Methods: Apple Pay / Google Pay / card (Visa, Mastercard, etc.). Success or fail screens. After pay, booking is **Confirmed** (PO paid). Whether the list also shows **Requested** at that moment: **UNKNOWN**.

**Owner pays the full amount upfront** (product 2026-08-25), regardless of how long the booking runs — a one-day walk and a six-month repeating booking are both paid in full at create. No instalments, no per-session charging. The money then sits in **escrow** until each session completes ([admin-finance.md](admin-finance.md)).

---

## Promo

One code **per trip**. Errors: invalid · expired · already used.

---

## Filters (search)

Rating, distance (3 / 5 / 10 / +10 km), non-smoking, plus the service/time already chosen. No results empty state. Search by sitter name.

---

## Address

First booking can force **add address**. Later: pick saved tag or add new (same address model as Profile).

---

## Checklist

**Pet care checklist** is **per pet × per session**, not a booking-level list. Water, snacks, extras (grooming, medicine, etc.). Ops opens it from **session detail**, not from the booking breakdown. Empty: no extra details from sitter.

---

## Report

Shown when status is **Live** or **Completed**. Topic + optional details → team contacts them.

**Repeating:** until the **whole booking** is completed, **Cancel & report** is also shown; after fully complete, cancel is gone, report remains.

**Admin:** this **should** be an ops queue. **Not ready yet** — do not design the report inbox until product asks. App side still collects the report.

---

## Admin hooks

- Booking as a bag of pets × SKUs × add-ons × sessions, with **hard combination rules**.
- Status pipeline + pickup/drop.
- Decline (**no reason** shown or required).
- Request is always **one targeted sitter**.
- Duplicate-slot guard.
- Payments (Mamo) success/fail.
- Promo validity / one-per-trip.
- **Report** — app can file it; **admin queue is intended but not ready**. Do not invent the ops UI yet. (Ops may get a report action later — not locked.)
- Both parties can cancel; session cancel on repeating/continuous.
- Search filters (distance, rating, smoking).

**Ops can (locked 2026-08-19):** cancel the whole booking; cancel a **session**; **reassign** sitter (**any** status, one or many sessions at once, **force assign** with no acceptance, **Approved** sitters only — see [booking-live-session.md](booking-live-session.md)); **change status** (**any** → any); **finish** a **session** or a **service** if the sitter did not. **Ops cannot start.** **No edit dates** for now; no other edit of the bag until product asks. **Refund label** (not a primary action on this panel): mark booking and/or **session** as refunded. Actual money is **Mamo**, listed on **admin Finance** — [admin-finance.md](admin-finance.md). Outside this booking panel.

---

## Still unknown

- Full FDT UI (window length options, who confirms the actual minute) — product will share.
- Payment fail retry.
- After pay: Confirmed vs Requested vs Accepted (Confirmed = paid, nearer **Live**; sequence **UNKNOWN**).
- **Ready** vs Accepted / Live (exists; unlabeled in admin for now).
