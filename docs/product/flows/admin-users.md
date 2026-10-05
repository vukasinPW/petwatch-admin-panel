# Admin Users

Status: list fields + remove gate locked 2026-09-11. Table + card drawn. Login drawn 2026-09-19 (email + password). FigJam `9:372` (System & Support → Admin Users).

Admin-Panel: `rc6tFk9QGVqOFD3ht9Upt8`  
FigJam: list `9:375` · detail `9:379` · new `9:383` · edit `9:387`

| Screen | Node | State |
|---|---|---|
| Login | `7901:111557` | Drawn 2026-09-19 — email, password, remember me, forgot password, Log in. Error twins `7901:111701` `7901:111889` |
| Reset password | `7908:138584` | Drawn 2026-09-19 — email recovery, then new password + Requirements |
| Profile — recovery sent | `7923:112473` | Drawn 2026-09-19 — signed-in Reset password, same recovery email |
| List — table | `7678:81265` | Drawn 2026-09-11 |
| List — card | `7694:81357` | Drawn 2026-09-11 — User card: name, role, last login |
| Detail | — | Later — activity log + remove (not on the list) |
| New | `7684:81020` | Drawn 2026-09-11 — Email, Name, Role. No created date on the form |
| Edit | — | Later |

Not the Pet Owner / Pet Sitter directory. These are **people who can open the admin panel**.

---

## Why it exists

Super admin needs to see who has panel access, what role they hold, who created them, and whether they still use the account.

---

## Locked (product 2026-09-11)

- **No invite.** There is no pending / Invited state. An account exists only after a **super admin creates it**.
- **Role** on the list is a placeholder: **Admin**. Real role set later — do not invent extra roles on the dummy.
- **Activity** on the list = **last login** (they opened the panel), not “last used a screen.” **Detail** also has an **activity log** (same idea as PO / sitter).
- Audit on the list: **created date** + **created by**, and **updated date** + **updated by** (last time a super admin changed the account — including role). No special case for the first super admin.
- **Remove** is allowed (super admin can take another admin off the panel). **Not from the table** — table Actions are **View** only. Remove lives on **detail**. Deactivate vs delete as separate actions: **UNKNOWN** until that screen.
- **Panel login is email + password.** No magic link on this screen. No create-account — an admin exists only after super admin creates them (`Add new`). Remember me + **Forgot password?** are on the login.
- **Forgot password is email recovery, not OTP.** Forgot password? → enter email → **Send recovery** → **Recovery email sent** → (email link) new password with `Requirements` → success popup **Password reset successfully**. **Continue** opens the admin panel (signed in). Empty Send recovery / Reset password are Disable. Requirements copy is the component (8–12 characters, capital, special, number) — not the app’s five-rule list. **Already signed in:** Profile **Reset password** sends that same recovery email to the account email and shows **Recovery email sent** on the drawer. They still set the new password from the email link.

---

## List

Same shell as other admin lists: table + card (`Table control`). No card-only product. **No invite CTA** — Add new is create.

### Table columns

Checkbox · **Name** (avatar + name) · **Role** · **Created** · **Created by** · **Updated** · **Updated by** · **Last login** · **Actions** (View).

**Updated** / **Updated by** = last change to the account (role change). If never changed after create, dummy can match Created / Created by.

No Status column (no Invited). No remove / delete / deactivate on the row.

### Cards

Same `User card` as Pet Owner list. Photo + **name**. Rows: **Role** · **Last login**. **View** only (no Edit, no status badge). Created / created by / updated stay on the table.

---

## Create (Add new)

Drawn 2026-09-11: `Admin Users - Add new` (`7684:81020`). Super admin creates the account. **No invite.** Created date / created by / last login are **not** on this form — the system sets them on Create.

| Field | Control | Dummy |
|---|---|---|
| Email | `Input Filed` Placeholder | Email |
| Name | `Input Filed` Placeholder | Full name |
| Role | `Input Filed` select (chevron) | Admin |

Actions: Cancel Tertiary · **Create** Primary Brand. No password field.

---

## Login

Drawn 2026-09-19: `Login` (`7901:111557`). Split layout — form left, image placeholder right (drop the photo on `Image placeholder`).

| Field | Control |
|---|---|
| Email | `Input Filed` Placeholder |
| Password | `Password` / `Input Filed` + show/hide |
| Remember me | `Checkbox` 24, off |
| Forgot password? | `Link` → Reset password |
| Log in | Primary Brand |

No sign-up. No social / UAE PASS.

---

## Reset password

Drawn 2026-09-19. Same split shell as Login. Buffer-style email recovery (no 4-digit code).

| Screen | Node | State |
|---|---|---|
| Reset password | `7908:138584` | Email empty, **Send recovery** Disable, **Back to log in** |
| Reset password — filled | `7908:138602` | Email filled, Send recovery on |
| Recovery email sent | `7908:138620` | Success check, **Back to log in** Secondary |
| New password | `7908:138638` | `Password` + `Requirements` Not confirmed, **Reset password** Disable |
| New password — valid | `7908:138656` | Requirements Confirmed, Reset password on |
| Success | `7914:111598` | Dim 70% + 659 `Pop up` on the filled new-password screen. **Password reset successfully**. **Continue** Primary Brand → admin panel |
| Signed-in — recovery sent | `7923:112473` | Profile drawer still open. **Reset password** sends the recovery email (no email field — account is known). Bottom card: **Recovery email sent** + same body as `7908:138620` (this profile’s email). No new-password form here. |

**Signed-in Reset password** (profile drawer) is the same email-recovery path, not a second form. No OTP. No in-panel password fields.

---

## Still unknown

- Real role set (super admin vs Admin vs others) — dummy is Admin.
- On detail: deactivate vs delete (or both), same 30-day restore as PO/PS or not.
- How the new admin gets a first password (Create has no password field) — this recovery flow can be that path, not confirmed.
