# PetWatch product knowledge

Canonical app truth for Cursor. Distilled from App Design Figma + confirmed rules.
Do not invent behavior that is not in these files. `UNKNOWN` means ask, do not guess.

Capture **logic** (gates, statuses, who can do what). Figma copy is not 1:1 with the live app and may be missing — do not invent strings, and do not block on wording.

When a new flow is shared, **ask blocking product questions in that same turn** (gates, who the request goes to, combo rules, what Figma left open). Do not wait until after the doc.

App Design file: `fFkKBQPGIaM1Zjk9dz7LUW`

| Flow | Status | File | Figma |
|---|---|---|---|
| Sign up / login / forgot password | Captured | [flows/auth-signup.md](flows/auth-signup.md) | `21900:74576`–`21900:74580`, `17115:86746`, `17115:86130` |
| Auth & verification errors | Captured | [flows/auth-errors.md](flows/auth-errors.md) | `25683:20278` |
| PO profile verification | Captured | [flows/po-verification.md](flows/po-verification.md) | `17115:87360`, `21594:42901` |
| PS profile verification | Captured | [flows/ps-verification.md](flows/ps-verification.md) | `17858:106356`, `21594:139902` |
| Home (PO + PS) | Captured | [flows/home.md](flows/home.md) | `21638:239602`, `21638:240055`, `21671:141597`, `21849:168201`; protos `21638:168342`, `21638:170258` |
| Pet profile | Captured | [flows/pet-profile.md](flows/pet-profile.md) | `23571:81318`; proto `23571:81319` |
| Sitter onboarding / Academy | Logic captured (web) | [flows/academy.md](flows/academy.md) | — (web; app Join academy on Home) |
| PS profile setup (after Academy) | Captured | [flows/ps-profile-setup.md](flows/ps-profile-setup.md) | `24071:219686`; proto `24071:221517` |
| PO Profile | Captured | [flows/po-profile.md](flows/po-profile.md) | `20393:177018` and related Profile sections |
| PS Profile | Captured | [flows/ps-profile.md](flows/ps-profile.md) | `20409:20158`, `19962:185251`, `19962:185631`, `19962:186157`, `19962:185974`, `19962:186383` |
| Admin: delete sitter | Captured (gate) | [flows/ps-profile.md](flows/ps-profile.md) — Admin hooks | FigJam `Flow — Delete sitter`; blocked overlay `7228:79523` |
| Booking (PO General) | Captured | [flows/booking-po-general.md](flows/booking-po-general.md) | `20389:121706` and related General sections |
| Booking live session (PS) | Captured | [flows/booking-live-session.md](flows/booking-live-session.md) | `21019:191825`–`24539:193650` |
| PO Services tab | Captured | [flows/po-services.md](flows/po-services.md) | `21468:161680`, `21468:163132` |
| PS Finance tab | Captured | [flows/ps-finance.md](flows/ps-finance.md) | `25700:218013` |
| Admin Finance | Overview + Payouts list; sitters-in-month; sitter payout popup (bookings + sessions + ratio, no list, no IBAN) 2026-09-01 | [flows/admin-finance.md](flows/admin-finance.md) | Overview `7432:73211` · Payouts `7512:63015` · Month `7538:66309` · Refunds `7489:74886` · Detail `7562:94663` · FigJam `98:499`, `6:200`, `6:229`, `103:504` · legal [refund](https://petwatchapp.com/legal/refund-policy/) · [cancel](https://petwatchapp.com/legal/cancellation-policy/) |
| Admin Promo codes | List + create/edit (designer lock) + Active detail + Statistics | [flows/admin-promo.md](flows/admin-promo.md) | List `7512:64021` · Add `7558:66322` · Edit `7558:67975` · Detail `7561:66695` · Statistics `7615:97879` · FigJam `9:344` |
| Admin Notifications | Home + Support list / create (Cloudflare) / templates (full-page create + copy/delete) + sent detail (recipients table) | [flows/admin-notifications.md](flows/admin-notifications.md) | Home `7582:70321` · Period `7582:100193` · Support list `7616:81299` · Sent detail `7646:74265` · Create `7606:73604` · Templates `7616:81319` · Create template `7638:71893` · Overflow `7638:99470` · Copy `7638:99639` · Delete `7638:99808` · After-send confirm `7616:81356` · FigJam `9:258` `9:275` |
| Admin Content / Catalog | 8 children locked; lists + universal Open popup 2026-09-04 | [flows/admin-catalog.md](flows/admin-catalog.md) | Services `7626:89673` · Open `7655:75163` · FigJam Catalog `9:287` · FAQ/Content/icons `9:208` |
| Admin Users | List + add-new form 2026-09-11 (email, name, role; no invite); login + reset password 2026-09-19; signed-in profile recovery 2026-09-19 | [flows/admin-users.md](flows/admin-users.md) | Login `7901:111557` · Reset `7908:138584` · Profile recovery `7923:112473` · Table `7678:81265` · Card `7694:81357` · Add new `7684:81020` · FigJam `9:375` `9:383` |
| Admin Reviews (Rate us / app + store) | In-app feedback table + detail; store reviews table + detail 2026-09-11 (not booking reviews) | [flows/admin-reviews.md](flows/admin-reviews.md) | App Rate us `19962:158424` · Feedback `7699:81267` · Detail `7700:81697` · Store reviews `7700:109625` · Store detail `7704:82302` |
| Sessions | Same as live booking (no separate flow) | [flows/booking-live-session.md](flows/booking-live-session.md) | `21019:191825`–`24539:193650` |
| PO finance | None — no PO finance in the app | — | — |
| Messages | Captured | [flows/messages.md](flows/messages.md) | `21638:187382`, `21638:185427`, `21638:185744`, `21638:186278`, `21638:186711`, `21638:187534` |

When designing admin, read the matching flow file and flag any app rule, status, or exception that has no admin surface. Keep Figma vs product copy labels consistent across capture files.

## How to update this (product)

You do **not** paste knowledge into chat. You **change the files**.

Same Cursor project, any chat. When a flow or rule changes, say what changed (Figma link and/or the decision) and the agent patches the matching `flows/*.md` + this INDEX **in that turn**.

One-liners that work:
- `New flow — [Figma]. Capture it.`
- `Update pet-profile: vaccine expiry now also emails the owner.`
- `We reversed X — lock it in docs.`

If we already captured during the session, you don’t need a second “please remember” at the end.

Admin visual work (new table, new layout) is not a product-doc update unless an **app rule** changed.
