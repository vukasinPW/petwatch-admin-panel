# PS Profile

Status: captured from Figma 2026-08-18. Logic only.

App Design: `fFkKBQPGIaM1Zjk9dz7LUW`

| Topic | Section |
|---|---|
| Gallery / profile photos | `20409:20158` |
| My availability | `19962:185251` |
| Service setup | `19962:185631` |
| Environment details | `19962:186157` |
| Personal details | `19962:185974` |
| Bank details | `19962:186383` |

**Shared with PO** (not duplicated in Figma): password set/reset, notifications, reviews, rate us, help center, policy, switch account, log out, deactivate / delete. Same logic as `po-profile.md`. Help Center **Email us / contact us** is the in-app contact target.

Menu: **View gallery** · My availability · Service setup · Environment details · Personal Details · Bank details · then the shared rows.

Until Academy + operating setup are done, availability / services / environment show empty + **Go to academy** (`ps-profile-setup.md`).

---

## Gallery

Sitter photo gallery (not pet photos).

- Grid with a **Cover** (most important). Reorder by dragging; cover can be set from a photo action.
- Per photo: **Set as cover**, **Edit description** (optional, 0/200), **Delete** (confirm). Unsaved description leave → save / don’t save.
- Add: native camera/gallery, optional description, confirm **add to gallery**.
- Counts drawn as `n/6` and `n/12` — treat **12 as max** unless product says otherwise. Cover is required for a useful public profile (**UNKNOWN** if cover is mandatory to stay live).

---

## My availability

Edit of the weekly window from setup (`ps-profile-setup.md`):

- Days Mon–Sun (tap a day circle → that day appears in the list)
- Hours; **Use same hours for all days**
- Plus → extra time slot on that day
- Save appears only after a change

**Scheduled break** (separate from Home pause-availability): **Need time off?** / Update calendar → date range(s). Banner while on break. **Edit break**. Ending early → confirm popup.

Home pause = short hide for **new** services. Calendar break = planned time off. Both exist.

---

## Service setup

Summary of opted-in SKUs (dogs / cats). Edit **Main** vs **Additional**, Select all. Same catalog as setup. **Prices stay platform-fixed** — sitter only toggles which SKUs they offer.

---

## Environment details

Same fields as setup: photos, smoking, pets at home (dog/cat/other + add another), facilities. Plus **address** (house/villa vs apartment, same extra fields as PO address). One operating address for the sitter home.

---

## Personal details

Name, DOB, gender, nationality, email, phone, occupation. Same edit/delete/deactivate pattern as PO (`po-profile.md`). Identity fields vs editable occupation: same **UNKNOWN**.

---

## Bank details

IBAN is **shown**, not freely edited in-app.

**Change bank account** / **contact us** → in-app **Help Center contact us** (not a website, not a separate bank form). Product confirmed.

IBAN explainer sheet exists (what it is / where to find it).

IBAN **status** is **Mamo Pay**, not admin. Admin cannot approve/reject it. Later number changes still go through **Help Center / contact**, not self-serve; the new IBAN is then Mamo’s to accept.

---

## Admin hooks

- Gallery + cover.
- Weekly hours + **calendar breaks**.
- Service SKU opt-in (not prices).
- Environment + sitter address.
- IBAN change requests via Help Center / contact.
- Shared: deactivate (login within 30 days restores; otherwise **auto-deleted**), delete, multi-account on device.
- **Rate us / app reviews** — same queue as PO (`admin-reviews.md`). Role on the admin table is Pet Sitter.
- **Admin delete is gated.** Ops cannot delete a sitter while **Live**, **Upcoming**, or **Requested** bookings exist. Those bookings must be **reassigned or canceled** first (same actions as booking detail). Completed and Canceled do not block. After the gate is clear, the same permanent-delete confirm as PO applies. This gate is **admin-only** — it is not assumed for PO, and it does not change sitter self-delete in the app.

---

## Still unknown

- Gallery max 6 vs 12 (canvas shows both); cover required to stay live.
