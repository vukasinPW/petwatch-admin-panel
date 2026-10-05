# PS profile verification

Status: captured from Figma 2026-08-18. For Pet Sitters who did **not** sign up with UAE PASS (those already Registered + Verified with bank + photo — auth Path E).

App Design: `fFkKBQPGIaM1Zjk9dz7LUW`

| Variant | Section | Node |
|---|---|---|
| Verify later with UAE PASS | If the user is not sign up with UEA PASS, but verifying profile with UEA PASS | `17858:106356` |
| Manual Emirates ID | If the user is NOT sign up with UEA PASS. Verifying mannually with Document Scanning | `21594:139902` |

Manual sub-stories: Successful `17858:107558` · Missing info `21926:125859` · Nothing scanned `21594:51220` · **Admin didn’t approve IBAN** `21594:138350` · **Team didn’t verify account** `21594:139896` · Error messages `21594:139901`

---

## Gate

PS **cannot join Academy / receive bookings** until identity is verified. Unlike PO, the hub is **one step** (no pet profile).

Entry: PS Home → **Start now** on “Complete your profile to start using PetWatch” → hub **Verify Profile**. Copy: *Before joining Academy, you must verify your account.*

Hub (`PS - Verification 01`): Step 1/1 **Complete your profile** → **Verify now**.

After success, Home CTA becomes **Join academy**. Tapping **Join academy** while still unverified opens **Verify your profile** (UAE PASS + Verify Manually). Home variations also draw an identity **under review** Home that still shows Join academy; the prototype then blocks that tap with a toast instead of the verify popup — see `home.md`.

**Join academy unlocks only when:** (1) the team has **verified the profile** (that is when they become Verified), **and** (2) **IBAN is approved**. IBAN check is fast (~1–2 minutes), not a 24h queue. There is **no** second Academy-application 24h review.

Academy happens **on the web**, not in the app. The app is connected: after they **confirm** Academy on the web they can **set up their sitter profile**, then they become **visible to pet owners**. See `academy.md`. If IBAN was rejected they **must fix bank details first**; Figma still showing Join academy next to the IBAN error is not product.

---

## Path 1 — Verify with UAE PASS (existing email/phone/social sitter)

Figma: `17858:106356`

1. Hub → native **UAE PASS APP**.
2. **Bank details** (required) — IBAN, Account holder name, Bank name. Same copy and invalid-IBAN error as UAE PASS sign-up. IBAN explainer sheet exists.
3. **Profile Picture & bio** — photo required, bio optional, same picker. Continue off without photo.
4. Success popup **Let’s get started**.
5. Home with **Join academy**.

Instant identity verify. No 24h wait. Bank is collected here (not at email/phone sign-up).

---

## Path 2 — Verify manually (Emirates ID)

Same scan pipeline as PO (front → confirm → back → confirm → scanning stories), then **PS extras**.

### Ending A — Successful scan

Confirm scanned fields (First / Last / Nationality / Gender / DOB) → **Bank details** → **Photo + bio** → submit.

**Thank you! Your information has been submitted.** *Our team will review your verification. Since this is a manual process, it may take up to 24 hours.* **Close**.

Home pending: **We are currently verifying your profile** / *This process may take up to 24 hours* / **Got it**.

Home after approve: **Join academy**.

### Ending B — Missing some info

Same “We are missing some info” form as PO, then bank → photo → 24h submit → pending → Join academy.

### Ending C — Nothing scanned

**We couldn’t scan pictures you shared with us** → **Try again** (camera). No skip-to-form on this frame.

---

## Admin outcomes drawn on canvas (PS only)

These are **not** on the PO verification file.

### IBAN not approved (`21594:138350`)

Identity can already be verified while IBAN fails separately.

Home: **Your IBAN is not matching with the name on your documents** / *Please check the IBAN you entered.* **Add Bank details**. Figma also draws **Join academy** — **product: they cannot join Academy until IBAN is fixed and approved.** IBAN approval is ~1–2 minutes after a correct resubmit.

Sitter returns to Bank details (prefilled) to correct IBAN.

**Product (2026-08-19):** PetWatch admin **cannot set or change IBAN status.** That outcome is **Mamo Pay**. Identity review stays ours (24h). The Academy gate still needs IBAN approved — we only **read** Mamo’s result, we do not click approve/reject on IBAN.

### Team did not verify the account (`21594:139896`)

Home: **Your account is not verified** / *Please contact us for more information.* **Contact us**.

**Contact us** on that reject screen is drawn as website. **Change IBAN later** from Profile is **in-app Help Center** (`ps-profile.md`). Whether identity-reject Contact us is the same Help Center now: treat as **same in-app contact** unless product says the website leftover is live.

Admin hook: identity **reject** exists as an outcome; the sitter is not told *why* in-app (matches the pet-profile rule: no rejection-reason to the user).

---

## Field errors on canvas (`21594:139901`)

- IBAN: *The IBAN number format is not valid.*
- Photo: *The format of the picture is not valid. Please upload PNG or JPEG* (and further size/format variants in the section — full copy when we ingest the error set).

---

## vs PO verification

| | PO | PS |
|---|---|---|
| Hub steps | 2 (identity + pet profile) | 1 (identity only) |
| Gate CTA | Book a sitter | Start now → later Join academy |
| UAE PASS later | photo + bio | **bank +** photo + bio |
| Manual after scan | photo + bio → 24h | **bank +** photo + bio → 24h |
| IBAN reject story | not drawn | drawn; **must fix before Academy** (Figma extra CTA is not product) |
| Account not verified + Contact us | not drawn | drawn |
| Next after verified | Create pet profile | Academy |

---

## Statuses (sitter identity / payout)

| Status | Meaning |
|---|---|
| Registered, not verified | Email/phone/social sign-up; Home “Complete your profile” |
| Verification pending | Manual ID submitted; up to 24h |
| Verified, IBAN rejected | Identity ok, bank rejected; **cannot** join Academy until IBAN is fixed (~1–2 min after resubmit) |
| Verified (+ IBAN approved) | Join academy |
| Not verified (rejected) | Contact us |

Aligns with sitter lifecycle **Registered → Verified → In academy → …** — Academy is **web**; status syncs to the app (`academy.md`).

---

## Admin hooks

- Same **manual ID review queue** as PO (front/back, extracted fields, photo, 24h).
- Extra: **show Mamo IBAN status** (read-only). Admin cannot approve/reject IBAN. Rejected IBAN still blocks Academy until the sitter fixes details and Mamo accepts. Identity approve/reject stays ours.
- Extra: **identity reject** → “Your account is not verified” + Contact us (no reason shown).
- UAE PASS later-verify: no ID review; still store bank + photo.
- Sitters who signed up with UAE PASS skip this whole flow (already verified + bank + photo).

---

## Still unknown

- Contact-us channel (in-app form vs external site).
- Whether “Mamo” in the IBAN section name is a person or a typo for admin.

Photo errors: `docs/product/flows/auth-errors.md`.
