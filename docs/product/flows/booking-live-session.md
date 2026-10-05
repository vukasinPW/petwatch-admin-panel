# Booking — PS live session

Status: captured 2026-08-18. These Figma links were labeled “PO POV”; product confirmed they are **sitter execution** of a booking the owner already created.

App Design: `fFkKBQPGIaM1Zjk9dz7LUW`

| Topic | Node |
|---|---|
| Bookings tab variations | `19552:126091` |
| Single pet | `21019:191825` |
| Multi pet / repeating, split walks or walk+visit | `21019:193929` |
| Canceling | `21019:206462` |
| PS cancel session flow | `25749:191832` |
| PO cancel session or booking | `21377:160841` |
| Declining | `21019:208342` |
| First-time tutorial — repeating | `21245:89142` |
| First-time tutorial — one-time | `21245:105096` |
| Unfinished booking blocks the next | `24539:193650` |

---

## After the owner pays

Sitter gets a notification + in-app popup. **Requested:** **Decline** (no reason) or **Accept**. First-time sitters get a **tutorial** (map / pickup). Then **Go to sitting**.

---

## Pickup → live → done

**Pick up** starts the service and **notifies the owner**. Sitter confirm only (*I am not with pet yet* if they opened it early).

**Drop / finish:** sitter taps drop or finish → booking (or that session) is **done**. **No PO confirmation** — even if an old frame still shows one, ignore it. Product: POs not confirming left bookings stuck.

If they drop **before** the slot ends, sitter still only confirms on their side. When **scheduled time expires**, the complete screen can appear without a tap.

Split **walks** or **walk + home visit**: extra UI for which pet / which leg.

After complete: sitter **feedback on the pet** (optional). Stored for the owner and future sitters.

---

## Cancel (PO and PS)

**Both** owner and sitter can cancel. For **repeating** and **continuous-day** bookings, cancel can be **per session** (product is applying that now). Money refund is outside admin; ops **labels** booking and/or session as refunded.

### PS cancel session — full flow (captured 2026-08-25, `25749:191832`)

Sitter opens the session → **Cancel session**:

1. **What happens if you cancel?** — applies to **this session only**; owner notified right away; *"They can get a refund, **or we can help find a substitute**"*; sitter is **not paid** for the canceled session; remaining sessions **stay with them**.
2. **Choice popup** — *Cancel this session* · *Cancel more sessions* · View cancellation policy.
3. **Select sessions** (multi-select over upcoming sessions) with a **cap of 40%** of remaining sessions (locked 2026-08-25). Completed sessions are listed but not selectable.
4. **Over the cap** → *Limit exceeded. Canceling more than 40% of sessions requires canceling the entire booking* → only exit is **Cancel the whole booking**.
5. **Reason — required.** 8 radio options: personal emergency/illness · unexpected pet behaviour or health · severe weather/natural disaster · change in personal/travel plans · pet sitter didn't show up · dissatisfaction with sitter service · service no longer needed · Other.
6. **Instructions for the substitute** — free text, **min 20 characters**, *"Leave the instructions for your potential substitute."*
7. **Success** — *"You canceled this session successfully. Your next session from this booking is on <date>."*

**Cap is 40%** (locked 2026-08-25). The choice popup still says *30%* on canvas — that copy is wrong, not a second rule.

### Reassign / substitute (locked 2026-08-25)

The substitute is **ops work** — the app promises it (*"we can help find a substitute"*).

- Sitter can cancel **several** sessions at once, so reassign handles **many sessions in one pass**, not one.
- **One sitter per pass** (locked 2026-08-26). Ops checks the sessions, picks **one** sitter, assigns. To split sessions across different sitters, ops runs the panel again — there is no per-session sitter picker. Matches how support works: one substitute found at a time.
- Sessions still without a substitute get **no special flag** — they stay `Canceled` and ops tracks the rest manually. No "needs sitter" marker, no counter banner.
- The sitter's **substitute instructions** (min 20 chars) and their **cancel reason** are written for whoever picks the job up — both must be visible to ops on reassign.
- **A whole booking canceled by the over-40% rule is still reassignable.** Ops can put the entire booking on a new sitter; it is not dead.
- **Force assign, no acceptance.** The new sitter is on immediately. Customer service reaches them separately. There is no request/accept round trip.
- **Approved sitters only** in the picker.
- **The owner is not told in the app.** Customer service contacts them over **WhatsApp** for now — no in-app substitute notification, no new-sitter card. Ops **must** still see who the job was reassigned to and from, so the assignment is visible on the admin side even though the app stays silent.
- **`Reassigned` is a session status** (locked 2026-08-26). After ops assigns a substitute the session is no longer `Canceled` — it reads `Reassigned` until it starts. Added as a variant on the admin `Booking status` component (Information blue dot).

### Refund vs substitute (the owner's fork)

When the sitter cancels, the owner is asked whether they want a **refund** or a **substitute**. Admin shows which one they picked as `Owner asked for`, and the session's main action follows it:

| Owner asked for | Session status | Main action | Sitter's substitute note |
|---|---|---|---|
| **Substitute** | `Canceled` → `Reassigned` after assignment | **Reassign** | shown — it is written for the replacement |
| **Refund** | stays `Canceled` | **Mark for refund** | hidden — nobody is taking the job |

**Refund money is Mamo**, listed on **admin Finance** ([admin-finance.md](admin-finance.md)) as Requested / Completed / Cancelled. This session page still has **Mark for refund** as a quiet label (who, when). Whether that tap **creates** the Finance row: **UNKNOWN**.

---

## One live booking at a time (with boarding exception)

Default: cannot **start** booking B if A was started and not finished — **even for a different owner**. Popup → go finish A. After A completes, return to the booking they came from.

**Exception — live boarding:** if the live booking is **boarding**, the sitter may also start **short** services the same day: **walking** and **home visit** only (leave the house and come back). **Sitting is not allowed** during live boarding. How many concurrent/short jobs: **UNKNOWN**.

---

## Admin hooks

- Accept / decline.
- Pickup starts live; sitter finish **closes** without owner confirm.
- Session-level cancel on repeating / continuous days.
- Block starting a second live booking, **except** shorts during live boarding.
- Pet behavior notes after a session.
- **Ops on session page (locked 2026-08-19):** Pickup and Drop (no separate Finish — Drop closes the session). Cancel this session. Reassign sitter **for this session**. Quiet Refunded label. Checklist per pet. Full page, not a popup. No admin notes.
- **Refund label** on booking and on session (manual). Money is Mamo / Finance list.

---

## Still unknown

- How many walk/visit jobs during one live boarding.
