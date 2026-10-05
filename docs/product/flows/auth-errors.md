# Auth & verification — error copy

Canonical inline errors for sign-up, log in, OTP, forgot password, and profile photo.
Figma: `25683:20278` (App Design). Do not invent other copy.

Continue stays **off** on these states unless noted.

---

## Sign up / Log in (`21929:139123`)

Identifier and Log in share the same field errors.

| When | Copy | Screen |
|---|---|---|
| Email not a valid address | The email format is not valid. | Sign-up identifier |
| Phone not a valid number | The phone number format is not valid. | Sign-up identifier (phone) |
| Email already has an account (sign-up Continue) | An account with this email already exists. Please log in. | Sign-up identifier |
| Phone already has an account (sign-up Continue) | An account with this phone number already exists. Please log in. | Sign-up identifier (not drawn; same logic) |
| Email + password do not match (log in) | The email or password you entered is incorrect. | Log in (phone + password = same idea, not drawn) |
| Identifier has no account (log in) | Looks like you don’t have an account. Please sign up. | Log in |

Log in does **not** reveal whether the identifier or the password was wrong.

---

## OTP (`21638:223560`) — email and phone verify, including forgot-password

| When | Copy | CTA |
|---|---|---|
| Code expired (2 min product rule) | The verification code has expired. Please request a new one. | **Resend code** (not Continue) |
| Code does not match | The code you entered is not matching. | Continue off |

No max-attempt lockout on canvas (matches product: no attempt cap).

---

## Forgot password (`21929:139403`, `21638:223370`)

Same email-format error as sign-up.

| When | Copy |
|---|---|
| Email format invalid | The email format is not valid. |
| Email has no account | Looks like you don’t have an account. Please sign up. |

Forgot-password is email on canvas; phone is the same logic (SMS).

---

## Profile photo (`21937:154349`) — sign-up UAE PASS, PO/PS verification

Shown on **Profile Picture & bio**. Continue off.

| When | Copy |
|---|---|
| Wrong file type | The format of the picture is not valid. Please upload PNG or JPEG |
| File too large | The size of the picture is too large. |

Two more frames in the section repeat format-invalid with an image already chosen (re-upload failed).

Allowed types: **PNG or JPEG** only.

---

## Already captured elsewhere (not this board)

| When | Copy | Where |
|---|---|---|
| IBAN format | The IBAN number format is not valid. | PS bank details |
| IBAN vs name on ID (admin) | Your IBAN is not matching with the name on your documents | PS Home after review |
| Identity rejected (admin) | Your account is not verified / Please contact us for more information. | PS Home |
| Email ≠ UAE PASS email | Your email is not matching your UEA PASS email | Hidden layer on PO verify popup — confirm live |

---

## Logic this locks

- Sign-up Continue on an existing email → stay on sign-up, tell them to **log in** (does not auto-switch).
- Log in on an unknown email → stay on log in, tell them to **sign up**.
- OTP expiry is a distinct state from mismatch; expired uses **Resend**, not Continue.
- Photo is required and validated (type + size) before Continue.
