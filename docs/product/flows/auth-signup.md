# Auth — sign up / login / forgot password

Status: Figma captured; rules confirmed 2026-08-18. Sign-up / log in closed.

App Design: `fFkKBQPGIaM1Zjk9dz7LUW`

| Variant | Section | Node |
|---|---|---|
| Email | Sign in/up flow using email address | `21900:74577` |
| Phone | Sign in/up flow using phone number | `21900:74578` |
| Social (Google, Apple) | Sign Up Flow continuing with a social links | `21900:74579` |
| Guest | Continue as guest | `21900:74576` |
| UAE PASS | UAE PASS | `21900:74580` |
| Log in | Log in | `17115:86746` |
| Forgot password | Forgot password | `17115:86130` |

UAE PASS, Log in, and Forgot password captured below. If a twin path is not drawn (phone vs email), apply the same logic.

---

## Confirmed rules (from product, not only canvas)

- **Continue on the identifier is always sign-up.** Log in is a separate screen, entered from **Already have an account? Log in** (or the guest gate). Log in captured below.
- **Identifier already registered:** *An account with this email already exists. Please log in.* Phone twin (not drawn): *An account with this phone number already exists. Please log in.* Stay on sign-up; do not auto-open Log in.
- **One account = one role** (for now). Not both PO and PS on the same account.
- **Guest is not an account.** Can browse Home and some other tabs. Cannot take account actions (book, etc.). Gated by login/signup popup.
- **OTP** expires after **2 minutes**. No max-attempt lockout. Resend cooldown 30s. Expired: *The verification code has expired. Please request a new one.* (Resend, not Continue). Mismatch: *The code you entered is not matching.*
- **Social:** name/email prefill from Apple/Google is still **UNKNOWN** (engineering). **PetWatch always stores the real email**, never Apple Hide My Email (`@privaterelay.appleid.com`). Social and UAE PASS users **set a password later from Profile**; after that the menu becomes Reset password (`po-profile.md`).
- **Phone:** any country is allowed at sign-up. Default UI is UAE +971. **Log in and Forgot password work the same as email** (not drawn).
- **Name at email / phone / social is just a name.** Government ID is **not** checked there. Identity is asked later in verification — **except UAE PASS**, which verifies identity during sign-up.
- **Role is assigned only on Sign up 04.** Continue stays off until one card is selected.
- **Let’s get started** (success popup) → **Home** for both PO and PS. Unverified users hit verification from Home CTAs.
- Last onboarding slide also has “If you are pet owner / pet sitter” cards. Those are **not** the role picker; they do not set the account role.
- **UAE PASS sign-up:** when the flow completes, the profile is **Registered and Verified** (identity done; no separate ID step).

Figma helper on Sign up 04 (*You will be able to change it later*) is **not** product. One account stays one role. Profile **Switch account** adds/switches a **second account** on the device (`po-profile.md`) — it does not merge PO+PS on one user.

---

## Shared entry (all registered paths)

Same prefix before the identifier:

1. **Splash** — logo only (`Splash screen`).
2. **Onboarding carousel** (3 slides) — cannot skip from Figma; page dots; no Skip control drawn.
   - Slide 1: service catalog (dog/cat walking, boarding, sitting, feed & playtime) + “Live chat updates from your sitter”.
   - Slide 2: same catalog + “Real-time map tracking” over a Dubai map (Burj Khalifa pin). Copy: “Scroll for more”.
   - Slide 3 / **Data Consent Form 01**: chat + map recap, two explainer cards (“If you are pet owner” / “If you are pet sitter”) — marketing only, **do not set role**. Primary **Get Started**. Footer: *By tapping “Get Started”, you agree to our Terms & Conditions and Privacy Policy*.
3. **Identifier screen** — title **Welcome to PetWatch**; subtitle **Enter an email to get started** or **Enter a phone number to get started**.

Identifier actions (always visible):

- Email field *or* phone field (`+971` default, flag, national number). Toggle: **Use phone number** / **Use email**.
- Primary **Continue** — sign-up only; disabled until the field looks complete.
- **or continue with:** **UAE PASS** · **Apple** · **Google**
- **Continue as guest**
- Footer: **Already have an account? Log in** → separate Log in flow.

---

## Path A — Sign up with email

Figma: `21900:74577`

1. Identifier — enter email → Continue enables. Invalid format: *The email format is not valid.* Already registered: *An account with this email already exists. Please log in.*
2. **Select your role** — Pet Owner / Pet Sitter. Role is set on card select. Continue disabled until one is selected.
3. **Let’s get your basic info** — First name, Last name. Copy mentions government ID; **product rule: name only, ID later in verification.** Continue disabled until both fields have values.
4. **Create your password** — single field, show/hide. Requirements (all must pass before Continue enables):
   - At least 8 characters
   - One lowercase character
   - One uppercase character
   - One special character
   - One number
5. **Verify your Email** — 4-digit code. Copy: *Enter the security code we sent to {email}*. **Resend code in 30 seconds**. Code **expires in 2 minutes**. No attempt cap. Continue disabled until 4 digits. Wrong-code / expired copy incoming (mismatch UI is drawn on the phone path).
6. Success popup: **Welcome to PetWatch** / **Successfully created your account** / **Let’s get started**.

Landing after this popup is **Home** for both PO and PS. Unverified users then hit verification from Home.

---

## Path B — Sign up with phone

Figma: `21900:74578`

Same splash → onboarding → identifier. User switches via **Use phone number**.

1. Phone field, default **UAE (+971)**. Any country allowed. Country picker: search (“Enter country name”), flag + country + dial code.
2. Continue enables when a number is entered. Invalid format: *The phone number format is not valid.* Already registered: *An account with this phone number already exists. Please log in.*
3. Role → name → password — **same as email**.
4. **Verify your phone number** — 4-digit SMS. Expires in 2 minutes. No attempt cap. Resend in 30s.
   - Empty / typing / 4 digits valid → Continue on.
   - **Wrong code (drawn):** *The code you entered is not matching.* Continue stays off (`Sign up 23`).
5. Same success popup. Landing is **Home** for PO and PS.

---

## Path C — Sign up with Apple / Google

Figma: `21900:74579`

1. Identifier → tap Apple (drawn) or Google (native Google sheet not separately drawn).
2. **Native system sheet** (Apple example): Cancel / Continue with password, Face ID, phone number, or email; *Hide My Email*; *Skip*.
3. **No password step. No email/SMS OTP step.** Password can be created later in Profile.
4. Role → name → success popup **Let’s get started** → **Home**. Same for PO and PS.

Prefill name/email from the provider: **UNKNOWN** (engineering). **Hide My Email is not used** — PetWatch always keeps the real email.

---

## Path D — Continue as guest

Figma: `21900:74576`

1. Identifier → **Continue as guest**.
2. **Select your role** — required; role set on card select. Drawn with Pet Owner selected.
3. **PO Home** as guest — not a user record. Browse Home and some other tabs. Cannot book or other account actions.
4. Gate: tapping a sitter (and other blocked actions) → **Log in or Sign up to start using PetWatch** · **Login** · **Sign up**, close (X).

Converting guest browse → full account: nothing to merge (no account). They start sign-up / log in from the gate.

---

## Path E — Sign up with UAE PASS

Figma: `21900:74580` (section split into **PO** `21900:67890` and **PS** `21900:73477`)

**Product rule:** when this flow completes, the user is **Registered and Verified**. Identity is done here; they do not go through a later ID / UAE PASS verification step.

No name step (name comes from UAE PASS). No password. No email/SMS OTP.

### Shared prefix (PO and PS)

1. Splash → onboarding → T&C Get Started → identifier (same as other paths).
2. Tap **UAE PASS** → **native UAE PASS app**: Login with biometrics, PIN, or Face Recognition. (OS overlay; PetWatch does not own this UI.)
3. **Select your role** — same Sign up 04 screen. PO and PS cards. Continue off until selected.

### Pet Owner only (after role)

4. **Profile Picture & bio**
   - Photo required (Continue off with empty avatar). Bio optional.
   - Photo picker: Take a photo / Choose from Gallery / Browse files.
   - Filled state: photo shown, bio empty, Continue on.
5. Success popup: **Welcome to PetWatch** / **Successfully created your account** / **Let’s get started**.

### Pet Sitter only (after role)

4. **Bank details** — required to complete sign-up. Copy: *We need your Bank details to complete your sign-up. Don’t worry — your information is protected and will never be misused.*
   - Fields: **IBAN**, **Account holder name**, **Bank name**.
   - Empty → Continue off.
   - Invalid IBAN → *The IBAN number format is not valid.* Continue off (`Sign up 32`).
   - Valid IBAN + filled name/bank → Continue on (`Sign up 33`).
   - **What is IBAN number?** sheet: definition + where to find it (banking app, statement, bank website generator, contact bank). Close with X (`Sign up 34`).
5. Same **Profile Picture & bio** as PO (photo required, bio optional, same picker).
6. Same success popup.

Drawn: PO never sees bank details in this section. PS always does, before photo.

---

## Path F — Log in

Figma: `17115:86746` (`Log in 01` `21900:74584`, `Log in 02` `21900:74790`)

Entered from identifier footer **Already have an account? Log in**, or guest popup **Login**.

Screen title **Log in**:

- **Email** + **Password** (show/hide). **Phone + password is the same path, not drawn.**
- **Forgot password?** → Path G (email drawn; phone = same logic, SMS OTP).
- Primary **Continue** — off until both fields have values (`Log in 01` empty).
- **Don’t have an account? Sign up** → back to sign-up identifier.
- **or** UAE PASS / Apple / Google (same three as sign-up). No Continue as guest on this screen.

Wrong credentials: *The email or password you entered is incorrect.* (phone twin: same idea). Unknown identifier: *Looks like you don’t have an account. Please sign up.* After successful Continue → **Home** (then verification gates if unverified).

---

## Path G — Forgot password

Figma: `17115:86130`

Email drawn; **phone is the same logic** (SMS OTP, not drawn).

1. From Log in → **Forgot password?**
2. **Forgot Password** — *Enter your email address that you use with your account to get the verification code.* Invalid format: *The email format is not valid.* No account: *Looks like you don’t have an account. Please sign up.* Empty → Continue off (`01`). Filled + valid → Continue on (`02`).
3. **Verify your Email** — 4-digit code. Same OTP errors as sign-up (expired → Resend; mismatch → Continue off). Phone twin: verify phone via SMS.
4. **Create your password** — same 5 rules as sign-up (`06` empty, `07` partial, `08` all green → Continue on).

No success popup after reset is drawn. Product inclination: user is **signed in** after Continue (not confirmed 100%). Treat as signed-in → Home until told otherwise.

---

## What is the same vs different

| Step | Email | Phone | Apple/Google | Guest | UAE PASS |
|---|---|---|---|---|---|
| Onboarding + T&C via Get Started | yes | yes | yes | skipped | yes |
| Identifier | email | phone | social button | Continue as guest | UAE PASS button |
| Role | yes | yes | yes | local only | yes |
| Name typed | yes, not ID-checked | yes, not ID-checked | yes, not ID-checked | no | no (from UAE PASS) |
| Password | yes | yes | later in Profile | no | no |
| OTP | email, 4 digits, 2 min | SMS, 4 digits, 2 min | no | no | no (native UAE PASS) |
| Bank details | no | no | no | no | **PS only** |
| Photo + bio | no | no | no | no | yes (photo required) |
| After complete | Registered, not verified → Home | Registered, not verified → Home | Registered, not verified → Home | no account, Home | **Registered + Verified** → Home |
| Success popup | yes | yes | yes | no — Home | yes |

---

## Designed edge cases (on canvas)

- Continue disabled until the current step is valid.
- Phone country search + list (any country).
- Password checklist (5 rules), live.
- OTP resend cooldown 30s; expiry 2 min (product).
- OTP mismatch (phone path drawn): “The code you entered is not matching.”
- Guest gated by login/signup popup.
- UAE PASS: invalid IBAN format; IBAN explainer sheet; photo required; bio optional.
- UAE PASS completion = Registered **and** Verified.
- Log in: Continue off until email + password filled.
- Forgot password: email → OTP → new password (same 5 rules).

## Still incoming (do not invent copy)

- Apple/Google **name** prefill (engineering). Email on the account is always the **real** one, not Apple Hide My Email.
- Forgot-password after Continue is **probably signed in** (not 100%).

Error copy: `docs/product/flows/auth-errors.md`. Twin paths not drawn (phone vs email) use the same logic.

---

## Admin hooks (fill when we design admin)

Candidates: user record (guest is **not** one), auth method including **UAE PASS**, role (single), email/phone vs **identity verified at signup (UAE PASS)**, PS IBAN at signup, photo/bio, already-registered → login.

---

## Figma copy traps (do not treat as product decisions)

Typos on canvas: “Select you role”, “Let’ get your basic info”, “United Arabic Emirates”, “Navtive apple/google”.
Name screen still says names must match government ID — product rule is name-only at sign-up; ID later.
Role screen still says role can be changed later — product rule for now is one account, one role.
