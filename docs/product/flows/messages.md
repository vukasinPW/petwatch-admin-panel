# Messages

Status: captured 2026-08-18. Logic only. Copy on canvas is leftover (delivery package, “no active offer”) — ignore wording.

App Design: `fFkKBQPGIaM1Zjk9dz7LUW`

| Topic | Node |
|---|---|
| Inbox (empty + list) | `21638:187382` |
| Send a message | `21638:185427` |
| Sharing media | `21638:185744` |
| Receiving media | `21638:186278` |
| System messages | `21638:186711` |
| Actions (booking / sitter) | `21638:187534` |

**Same for PO and PS** (mirrored). Drawn as PO (nav has Services; empty copy is “message your pet sitter”). PS empty / CTAs swap owner vs sitter; **Book another sitter** is PO-only.

**Not this tab:** Help Center **Chat support — Tito** (AI) lives under Profile (`po-profile.md`). Separate from booking chat.

---

## Why it exists

PO ↔ PS **one thread per person** (the pair), not per booking. Live updates around jobs with that sitter/owner. Not a social inbox. Not owner↔owner.

---

## Inbox

Empty (PO): **No messages yet** / *Once your booking is confirmed, you’ll be able to message your pet sitter.* **Create booking**. “Confirmed” here = **Accepted**.

**First send (working assumption):** the thread appears when the sitter **Accepts** the first booking between that pair. Requested (paid, waiting) is **not** chat yet. Figma drawing a composer on Requested is **not product**. Product was not 100% sure — change if later it is Requested.

After that, they keep **one** conversation. A later booking with the same person does **not** open a second thread.

**Header chip = the most relevant booking right now**, not a picker. Example: today is Monday and they have a session today → that booking. (Live / happening today beats a future or past job.) Tie-break if two sessions the same day: **UNKNOWN** (boarding + walk same day is allowed — `booking-live-session.md`).

Filled list: other party name, last preview (text or Photo / Video / Location / File), time (clock / weekday / date), unread count.

PO empty CTA **Create booking** → booking create (`booking-po-general.md`). Inbox **Finances** in the tab bar is leftover — PO tab is **Services**.

---

## Thread

Header: other party + **Online** + **one** booking chip (SKU summary, window, **status**) for the **most relevant** job (today’s session if they have one). Composer: *Type your message here..*

Statuses drawn on the chip: Requested, Accepted, Confirmed, Live, Declined, Cancelled, Completed. **Confirmed** = PO has paid (`booking-po-general.md`), matching the Payment Completed card — not a leftover name for Accepted.

From Bookings, **Contact sitter** / contact owner opens **this same person-thread** (not a new chat).

Composer stays **open** after decline, cancel, and complete. They can still type.

---

## Send

Type + send. Attach from `+` — **all of these are in product** (working assumption; product was not 100% sure):

| Type | Drawn |
|---|---|
| Photo | Take a photo / Choose from gallery |
| Video | In-thread clip (timer e.g. 00:09) |
| Location | Share location (address) / **Live location** / Current location |
| File | PDF (or other) as a bubble |

Receiving side shows the same bubbles.

---

## System cards (in-thread)

Not typed by the user. Echo of booking status. Several bookings between the same pair can drop cards into **the same** thread.

| Card | Header status | Extra CTA |
|---|---|---|
| Booking accepted! | Accepted | View details |
| Payment Completed! | Confirmed | View details |
| Service has begun! … | Live | View details |
| Service completed! How was your experience… | Completed | View details |
| Booking Declined! Your sitter declined… | Declined | **Book another sitter** (PO) |
| Booking canceled! Your sitter canceled… | Cancelled | Book another sitter (PO) |
| Booking canceled! You canceled… | Cancelled | Book another sitter (PO) |

View details → that booking’s details (same shape as Bookings). Completed card is a nudge to **review**, not a required PO confirm of the job (job already closed by sitter — `booking-live-session.md`).

---

## Actions from the thread

- **About sitter** — public profile (distance, map, reviews, gallery, services, house rules). PS side: about the owner if drawn later; not in this file.
- **Booking details** — pets & SKUs, general details, invoice, **Cancel Booking**, Contact sitter. Opens the **chip’s** (most relevant) booking.
- Cancel follows booking cancel rules (`booking-po-general.md`). Refund still out of scope for Finance.

No report / mute / block / delete-thread on canvas.

---

## Guest / gated

Logged-in tab. Until this pair has an **Accepted** booking, inbox has no thread with them (Create booking). Guest / unverified: they can open the tab, empty; Create booking hits verify+pet gates. **UNKNOWN** if Messages is hidden for guests.

---

## Admin hooks

- Thread key is **PO–PS pair**, not booking id.
- Product is **not sure** whether ops can open the thread. **Do not design** an admin chat viewer until they confirm.
- System events already mirrored as booking status — chat cards are the in-app echo.
- No in-app report-from-chat flow. Booking **Report** is a separate queue (not ready yet — `booking-po-general.md`).
- Media: photo, video, file, location, live location.

---

## Still unknown

- Two sessions the **same day** with the same person: which chip (live boarding vs walk).
- No session today: next upcoming vs last completed — implied by “most relevant,” not spelled out.
- After pay: Confirmed vs Requested on the chip (Confirmed is payment; sequence **UNKNOWN** — `booking-po-general.md`).
- Admin can open the thread: **UNKNOWN** (product not sure). Do not design it yet.
- First-send-at-Accepted and “all attach types” are **guesses**.
