# PO Profile

Status: captured from Figma 2026-08-18. Logic only.

App Design: `fFkKBQPGIaM1Zjk9dz7LUW`

| Topic | Section |
|---|---|
| Pet profile (view / edit / add) | `20393:177018` |
| Personal details | `20393:179036` |
| Address details | `20393:184463` |
| Reset password | `20393:183980` |
| Set up a password (social / UAE PASS) | `22937:43237` |
| Notifications | `20393:184462` |
| Reviews | `19962:159858` |
| Rate us | `19962:158424` |
| Help center | `19962:159409` |
| Policy | `19962:157372` |
| Switch account | `19962:157742` |
| Verification (from Profile) | `20582:182264` |

Password, notifications, reviews, rate us, help, policy, switch account, log out, deactivate/delete are **shared with PS** — same logic, not redrawn (`ps-profile.md`).

---

## Pet profiles (from Profile)

**Add pet** here is the same create wizard as Home (`pet-profile.md`). Allowed even while **identity is pending**. Booking still needs verified identity + **approved** pet.

Menu states:

- **No pet:** Create pet profile
- **One or more:** pet card(s) + **Add new pet profile**
- **Several pets** listed together (e.g. Lazar | Vukasin | Petar)

Card tint follows **gender** (female pink, male blue). Multiple pets: tint of the **first** pet.

Detail: identity fields (type, name, breed, gender, neutered, age, weight, height, microchip) + tabs whose edit logic is shared: **Medical conditions, Feeding timings & instructions, Allergies, Bio**. Save stays off until something changes. Unsaved leave is drawn (prototype); exact discard vs keep is **UNKNOWN**.

Photo change: native camera/gallery; **auto-saved** (no extra Save).

**Vaccination record:** mandatory Rabies + DHPPi with due dates; optional extras. **Expired** → Update record (same redo as create-flow expiry). App tracks due dates.

**Couldn’t verify pet:** banner + **Redo verification** (back into scan/review). Canvas note “Need a discussion” — treat redo as real; extra outcomes **UNKNOWN**.

---

## Personal details

Shown: Name, DOB, Gender, Nationality (from identity). Occupation + Bio are editable. Whether name/DOB/gender/nationality are locked after verify: **UNKNOWN** (they look like display fields).

Profile photo: native picker, **auto-save**.

Chooser (old design, treated as **current product logic** until a newer flow replaces it):

- **Deactivate** — temporary. Profile is **disabled**. Logging in again **within 30 days** reactivates. Confirm sheet before it applies.
- **Delete** — **permanent**. Profile is permanently deleted. Confirm (current App Design already has a delete confirm). After delete, Figma goes to the sign-up identifier screen.

UI chrome on that old screen is not current DS. The rules are. If they do **not** log in within 30 days, the account is **auto-deleted**. **PS uses the same deactivate / delete logic** (twin of PO).

---

## Saved addresses

List with **tags** (Home, Office, Mum’s home, or none) + **Add new address**. Same add flow as PS setup (search / current location, House/villa vs Apartment, number, area, street optional, extra instructions optional). Additional fields are the same for house and apartment.

**Tags are unique.** If the user applies a tag already used on another address and saves, that tag is **removed from the old address**. Confirm sheet before steal.

Optional fields can be cleared and saved. Mandatory fields cannot.

**Delete address** exists.

---

## Password

Same 5 rules as sign-up (8–12 chars, capital, special, number — plus the fifth from auth).

**Email / phone accounts:** menu **Reset password**. Current password + new password. **Forgot current password?** → same Forgot password path as login (email/phone OTP, then create new).

**Apple / Google / UAE PASS (no password yet):** menu **Set a password**. After they set it, the row becomes **Reset / Restart password**. Confirmed by product + canvas note.

---

## Notifications

Two channels: **Push** and **Email**.

- Push categories: Marketing, General, Personal
- Email: **Necessary** (always-on on canvas) + Marketing, General, Personal

Pause (push or email): 15 minutes / 1 hour / 6 hours / 12 hours / Temporary. While paused they still see notifications **in the app**. Helper: paused temporary / paused for mm:ss.

---

## Reviews

PO sees reviews **of them** (reputation after bookings). Empty: no reviews yet → Book a service. Filled: rating + list.

---

## Rate us

Profile **Rate us** → star sheet → in-app rate (3 drawn: Communication, Sitter service, App Flows, Response Time, Prices, App design + optional text, Submit). That Submit **is** the admin feedback table — **general app feedback**, not a booking review (`admin-reviews.md`). Canvas still draws 5 → native store; **product 2026-09-11:** Rate us does **not** log a store tap as a Feedback row. Public App Store / Google Store ratings are a **separate** admin list (`Store reviews - Table View`).

---

## Help center

- **FAQ** — use the **website** FAQ (canvas note)
- **Chat support — Tito** (in-app AI)
- **Email us** — form (email, question, details, optional photo). This is also the in-app **Contact us** target (e.g. PS **change bank details**).

---

## Policy

Opens legal list / **website**: PO terms, PS terms, T&C, Privacy, Refund, Cancellation, Trust & safety, Disclaimers.

---

## Switch account

**Not** changing PO→PS on the same account. **One account = one role** still holds.

This is **multiple accounts on the device**:

- Switch between already-added accounts (e.g. this PO + a **Pet sitter** account)
- **Add existing account** (email + password / forgot)
- **Create new account** (sign-up, including phone / UAE PASS)
- Empty: No accounts found

So a person can be PO and PS only via **two accounts**, not one.

---

## Verification (from Profile)

Shows **ID expiry date**. When expired: **Your ID expired** / **Verify account**. Closing the popup is not enough — **booking brings it back** (canvas note). Re-enters the same identity methods (UAE PASS / Emirates ID scan). Pet create is still the other hub step.

Admin: **Emirates ID expiry** returns the owner to unverified / not bookable until they re-verify (same idea as vaccine / microchip expiry on pets).

---

## Admin hooks

- Pet list + add/edit from Profile; pet verify fail → redo; vaccine due/expired.
- Owner identity fields; photo; occupation/bio.
- **Delete account** (permanent, immediate) and **Deactivate account** (temporary; login within **30 days** restores). No login in 30 days → **auto-deleted**. Same for **PS**.
- Address book + unique tags.
- Password set vs reset (auth method).
- Notification prefs.
- Reviews of the PO (booking reputation — not the Rate us list).
- **Rate us / app reviews** — read-only admin table (`admin-reviews.md`). No edit, no delete.
- **ID expiry** re-verify queue.
- Device can hold multiple accounts (PO + PS as separate users).

---

## Still unknown

- Identity fields editable after verify, or display-only.
- Unsaved pet-edit leave behavior.
- “Couldn’t verify pet” extra outcomes (note: needs discussion).
