# PO profile verification

Status: captured from Figma 2026-08-18. For Pet Owners who did **not** sign up with UAE PASS (those users are already Registered + Verified — see auth Path E).

App Design: `fFkKBQPGIaM1Zjk9dz7LUW`

| Variant | Section | Node |
|---|---|---|
| Verify later with UAE PASS | If the user is not sign up with UEA PASS, but verifying profile with UEA PASS | `17115:87360` |
| Manual Emirates ID | parent `21594:42901` — Successful / Missing some info / Nothing is scanned | `17442:28238`, `21594:38284`, `21594:39908` |

---

## Gate (both methods)

PO **cannot book** until both:

1. **Complete your profile** (identity verification) — Step 1/2
2. **Create pet profile** — Step 2/2 (see `pet-profile.md`)

Entry: PO Home → **Book a sitter** → hub **Verify Profile & Create pet Profile**. Copy: *Before making a booking, you must verify your account and create your pet's profile.* After both steps are done, the hub is **Close** and Book a sitter goes to search (see `home.md`). Book a sitter always opens this hub until both steps are complete; after that, verification is never shown again.

Hub (`PO - Verification 01`):

- Step 1/2 **Complete your profile** → **Verify now**
- Step 2/2 **Create pet profile** → **Create now** (disabled until step 1 is done, from the enabled/disabled pairing on 01). **Product:** the owner **can** add a pet **through Profile** while identity is still pending (flow to be captured later). Booking still waits for both identity + at least one pet.

Info sheet on Step 1 (`02`): **Verify your profile** + body (lorem on canvas) → **Verify now**.

Then a method popup (`03`): **Verify your profile with UAE PASS** (UAE PASS button) and **Verify Manually**.

Hidden layer on that popup (not shown in the default frame): *Your email is not matching your UEA PASS email* — treat as a designed error, confirm with product.

---

## Path 1 — Verify with UAE PASS (already have an email/phone/social account)

Figma: `17115:87360`

1. Hub → info sheet → method popup → **UAE PASS**.
2. Native **UAE PASS APP** (biometrics / PIN / Face ID), same as sign-up.
3. **Profile Picture & bio** — photo required, bio optional, same picker as UAE PASS sign-up (Take photo / Gallery / Browse files). Continue off without photo.
4. Success popup **Let’s get started**.
5. Hub with Step 1 **Completed! Your Profile is verified successfully** (green check). Step 2 **Create pet profile** → **Create now** enabled.

Instant verify. No 24h wait. No ID photos. No admin review.

This does **not** apply to people who already signed up with UAE PASS — they skipped this step 1 entirely.

---

## Path 2 — Verify manually (Emirates ID scan)

Figma: `21594:42901`

Shared scan pipeline, then three endings.

### Scan pipeline

1. Hub → **Let’s Verify your profile by scanning your ID** → **Verify now**. Copy: *Verify your ID in seconds to keep our community safe and start using our services right away.*
2. **Get your Emirates ID card ready** — good / glare / blur examples. **Take a picture**.
3. Camera: **front** of Emirates ID, document in frame. Confirm or retake (*Are you sure you want to proceed with this picture?*).
4. Flip card: **back** of Emirates ID. Same confirm / retake.
5. Loading: **Scanning your ID’s information...** with sitter stories carousel.

Typos on canvas: “font side”, “Get you Emirates ID”, “Blury”.

### Ending A — Successful scan (`17442:28238`)

6. **Please check if all information are correctly applied.** Prefill from scan, user can edit:
   - First name, Last name, Nationality, Gender, Date of birth
7. **Profile Picture & bio** (photo required, bio optional).
8. **Thank you! Your information has been submitted.** *Our team will review your verification. Since this is a manual process, it may take up to 24 hours.* **Close**.
9. Hub while pending: Step 1 **We are currently verifying your profile**. Step 2 **Create pet profile** still shown. Owner **can** add a pet via **Profile** during this wait.
10. After admin approve: hub **Completed! Your Profile is verified successfully** + Step 2 **Create now**.

### Ending B — Missing some info (`21594:38284`)

Scan worked only in part. Screen **We are missing some info** / *We couldn’t scan all information from your ID. Please enter missing information.*

User completes empty fields (examples on canvas: First name, Last name, Nationality picker, Gender Male/Female, Date of birth via Apple date picker). Then:

- **Basic Information** — *We extracted these details from your ID to speed things up. Confirm they match your document, or make changes if needed.* Mixed scanned + typed fields.
- Same photo/bio → same **24h review** submit → same pending / completed hub.

### Ending C — Nothing is scanned (`21594:39908`)

Scan failed. **We couldn’t scan pictures you shared with us.** *Please make sure that the image you take is clear and not blurry.* **Try again** → back to camera. No manual-form skip drawn on this frame.

A duplicate section `23671:145343` repeats this story; treat as the same flow.

---

## Statuses (PO identity)

| Status | How they got it | Can book? |
|---|---|---|
| Registered, not verified | Email / phone / social sign-up | no (hub gate) |
| Verification pending | Manual ID submitted | no (until admin + pet profile) |
| Verified | UAE PASS at sign-up, or UAE PASS later, or admin approved manual ID | still need pet profile |
| Scan failed / missing fields | in-progress manual | no |

---

## Admin hooks

- **Manual ID review queue** (up to 24h). Approve → PO verified. Reject / request retake: **UNKNOWN** (not drawn). Owner is not shown a rejection-reason form on these screens.
- **Emirates ID expiry** (Profile Verification): owner must re-verify; booking re-shows the popup if they dismiss it.
- Payload: Emirates ID front + back images, extracted + user-edited name / nationality / gender / DOB, profile photo, bio.
- UAE PASS later-verify: no admin review; possible **email mismatch** with UAE PASS.
- Sitters: see `docs/product/flows/ps-verification.md`.

---

## Still unknown

- Admin reject / incomplete-ID outcome.
- Whether **email not matching UAE PASS** is live.
- Non-Emirates ID / non-UAE residents (canvas is Emirates ID only).
- Pet profile via Profile — same create wizard plus view/edit/add, vaccine update, redo if verify failed (`po-profile.md`).
