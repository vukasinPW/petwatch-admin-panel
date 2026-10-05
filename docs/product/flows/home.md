# Home — Pet Owner and Pet Sitter

Status: captured from Figma 2026-08-18. Prototypes read 2026-08-18. `get_motion_context` has **no metronome keyframes** (`nodes: []`). Motion is **prototype SMART_ANIMATE** between screens, not after-effects / timeline animation.

App Design: `fFkKBQPGIaM1Zjk9dz7LUW`

| Section | Node |
|---|---|
| PO first time + verify hub from Home | `21638:239602` |
| PO returning (search + bookings) | `21638:240055` |
| PS Home variations | `21671:141597` |
| Join academy animation (section) | `21638:168341` |
| Join academy prototype start | `21638:168342` (Screen 60) |
| Availability animation (section) | `21638:170257` |
| Availability prototype start | `21638:170258` (Screen 63) |
| Pause availability from Home | `21849:168201` |

Figma notes on canvas are treated as product (they describe after-login logic). Copy on screens is illustrative; capture the gates and states, not the wording.

---

## Shared chrome

- Top: avatar + notifications bell.
- Bottom nav: **Home / Messages / Bookings / Services**.
- After **Let’s get started** / log in → this Home (already confirmed).

---

## Pet Owner Home

### First time (unverified, no pet)

Hero: **Book service for your pet** / 650 active services / **Book a sitter**.

Below the fold (scroll): Customer’s Fav Services, sitters with pets, Available Sitters Near You, Academy promo.

**Book a sitter** → verify hub (already captured). Canvas notes:

1. After login they land on Home.
2. Book a sitter → verify.
3. After UAE PASS verify: hub shows identity **Completed**; still **Create pet profile**. Banner: *Since you used UAE PASS, we will use that data to verify your account, so you can skip ID verification.*
4. After pet profile is created: hub **Close**. Then they can book.

Hub states drawn here (same flow as `po-verification.md`):

| State | Step 1 | Step 2 |
|---|---|---|
| Both open | Verify now | Create now (disabled until step 1) |
| Identity pending | We are currently verifying… | Create pet still shown — **allowed**. Owner can add a pet **through Profile** while identity is pending (same wizard: `pet-profile.md`). |
| Identity done, no pet | Completed! | Create now |
| Both done | Completed + info | Close |

### Returning (has searched / booked)

Same hero, plus **Recent search** and **Your bookings** (e.g. Daily sitting, dates, sitter, status **Upcoming**). Then the same marketing blocks.

---

## Pet Sitter Home

### First time (not verified)

Hero: **Become pet sitter today!** / 650 active services / **Join academy**.

Scroll: Top rated sitter, “Love for pets as a side hustle”, Stats, Academy promo.

Header: availability control + bell (availability is for later; first-time still shows it).

**Join academy** while unverified → popup **Verify your profile** / *To start the Academy, you must verify your profile.* UAE PASS + **Verify Manually**. (Same methods as PS verification.) Drawn on Home variations `21671:137452` / `21671:137730`.

**While identity is under review**, the same Home still shows **Join academy**. Prototype (below) blocks it with a toast instead of the verify popup: *You can join Academy once your profile is verified.* **UNKNOWN** whether unverified always uses the popup and under-review always uses the toast, or one replaced the other.

Under-review banner on that Home: **Your profile is under review!** / *Our team is reviewing the data you provided. It will be done within 24 hours.* That is **identity** review only — there is **no second 24h Academy-application queue**. After the team verifies the profile they become Verified and can join Academy (IBAN must also be approved; that check is ~1–2 minutes). Until then Join academy is blocked.

### Verified, not in academy

Hero **Join academy**. Tap → confirm popup **Join academy** (not the verify popup). Drawn on Home variations (`21671:139602`). **IBAN must be approved first** — if IBAN was rejected they cannot join until they fix bank details. Figma still drawing both CTAs is not product.

**Join academy** sends them to **web** Academy (not an in-app course). When they **confirm** Academy on the web, Home shows academy-success then **profile setup** (`ps-profile-setup.md`). Only after that setup are they **visible to pet owners**.

### Active sitter (has bookings)

Hero **PS main cta** is replaced by **Your bookings** + **Earnings**, then Top rated sitter. Marketing “Become pet sitter” is gone.

Info banner variant exists (identity/IBAN/account messages from verification still apply on Home).

---

## PS availability (from Home)

Header control: **Available** (green) / off. The control is visible on first-time Home, but the prototype **blocks** it until Academy is complete (toast below). Pause sheet is the path after they are allowed to use it.

### Gated (Academy not complete)

Tapping the availability toggle → toast *To use this feature, you need to complete the Academy.* Toggle stays **Available** in every prototype frame (the off action does not apply).

### Pause sheet (when allowed) — `21849:168201`

Turn off → sheet: *You won’t appear as available, but you can turn availability back on anytime.*

Duration buttons (exact labels):

- Pause for 30 minutes
- Pause for 1 hour
- Until end of current slot
- Until end of the day
- Until next week

Then **Close**. **UNKNOWN** whether Close **applies** the selected pause or only dismisses the sheet.

**Product:** pause only changes **visibility for new services**. In-progress bookings are not cancelled or hidden.

While paused, helper under the toggle (examples on canvas; not 1:1 with every duration label):

- *You will be available again at 08:00 PM*
- *You will be available again tomorrow at 08:00 PM*
- *You will be available again on next Monday at 08:00 PM*

---

## Prototypes — toast motion

Neither prototype is a success / celebration flow. Both are the same **Message** toast: compact → expand → settle. No metronome keyframes. Prototype never shows a fully dismissed toast (it stays on screen in all three frames; Screen 62/65 loops back to start).

Shared timing (both protos):

| Step | Trigger | Transition |
|---|---|---|
| Compact → expanded | `ON_CLICK` | `NAVIGATE` + `SMART_ANIMATE`, `EASE_OUT`, **150ms** |
| Expanded dwell | `AFTER_TIMEOUT` **5s** | then `SMART_ANIMATE`, `EASE_OUT`, **300ms** |
| Settle → loop to start | `ON_CLICK` | `SMART_ANIMATE`, `EASE_OUT`, **150ms** |

Treat **5s** as prototype dwell unless product confirms it is live toast duration.

Toast sizes as drawn (approx): compact 250×37 → expanded 327×48 → settle 270×40, sitting just above the tab bar.

### Join academy — start `21638:168342`

Home (under-review banner + Join academy). Click **Join academy** (`Large Button`) → expanded toast *You can join Academy once your profile is verified.* → 5s → settle (same copy) → click Join academy loops to start.

### Availability — start `21638:170258`

Same Home chrome. Click **Toggle - Switch** → expanded toast *To use this feature, you need to complete the Academy.* → 5s → settle → click toggle loops to start.

---

## Admin hooks

- PO: identity + pet-profile gates; Home is the entry. Pet can be created from **Profile** even while identity is pending.
- PS: **one** identity review (manual up to 24h). IBAN match is a **separate, fast** check (~1–2 min). No Academy-application 24h queue — Join academy unlocks when profile is Verified **and** IBAN is approved. Academy itself is **web**; confirm on web → app profile setup → visible to POs (`academy.md`).
- Availability: gated on Academy complete; pause = visibility for **new** services only.
- Admin may later need: on/off, pause until when, Academy complete, IBAN status.

---

## Still unknown

- Unverified Join academy: **verify popup** vs **blocked toast** — which state uses which? (UX, not a logic gate.)
- **Close** on the pause sheet: apply vs dismiss.
- Exact Academy curriculum after they are allowed to join — **N/A in-app**; it is web. Remaining: how Join academy opens the web, and post-Academy profile setup (`academy.md`).
- Pet profile via Profile (user will share later) — wizard captured in `pet-profile.md`.
