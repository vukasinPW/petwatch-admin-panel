# Admin Reviews (Rate us / app feedback)

Status: in-app feedback table + detail drawn 2026-09-11. Store reviews table drawn 2026-09-11. Not booking reputation. App source: Rate us (`19962:158424`).

Admin-Panel: `rc6tFk9QGVqOFD3ht9Upt8`  
App Design: `fFkKBQPGIaM1Zjk9dz7LUW`

| Screen | Node | State |
|---|---|---|
| Feedback — table | `7699:81267` | Drawn 2026-09-11 |
| Feedback — detail | `7700:81697` | Drawn 2026-09-11 — Emma Wilson |
| Store reviews — table | `7700:109625` | Drawn 2026-09-11 |
| Store reviews — detail | `7704:82302` | Drawn 2026-09-11 — Sara Al Maktoum |
| Store reviews — statistics | — | Not this pass |

Two lists: **Feedback** (in-app Rate us) and **Store reviews** (App Store / Google Store). Neither is reviews of a sitter or owner after a booking. Booking reviews stay on booking / profile.

---

## Why it exists

Ops need one list of in-app Rate us feedback: who, score, when. Open a row to see chips + comment. Read-only. No moderate, no reply, no delete.

---

## Locked (product 2026-09-11)

- **Feedback table only.** One table. PO and PS together. Role is a column, not a second queue.
- **No edit. No delete.** Row action is **View** only.
- **No Add new. No card view.**
- Table email = the **account email**, not a second email collected on the form. Canvas “Enter your email” on Tell us more is leftover Input Filed copy.
- **In-app only** on the Feedback table. App Store / Google Store ratings are a **separate** list (`Store reviews - Table View`). Do not mix the two. Rate us still does not log a store tap as a Feedback row.
- **What we track here:** users’ **general app feedback** from Rate us (who, role, email, stars, date; chips + comment on detail). Not booking reviews. Not store reviews.

### Table columns

**Name** (username) · **Email** · **Role** · **Rate** · **Date** · **Actions** (View).

Role dummy: Pet Owner / Pet Sitter. Rate = the star score they left (1–5). Date = when they rated.

Improvement chips and optional comment are **not** table columns — they belong on detail.

---

## App flow

Profile **Rate us** → star sheet → in-app form → Submit → thanks. That Submit is a row.

Form (drawn): **What part of service can be improved?** chips — Communication · Sitter service · App Flows · Response Time · Prices · App design. **Tell us more** optional, 0/600.

Star-cut vs store: **parked** (product 2026-09-11 — do not ask). Dummy can show 1–5. Do not model an App Store row on this table — store ratings live on **Store reviews**.

---

## Detail (single feedback)

Full page. Read-only. Who (name, email, role) · rate · date · Improve (chips) · Comment. No Save. No delete. Dummy: Emma Wilson, 3, Communication + App design.

---

## Store reviews (App Store / Google Store)

Separate list from in-app Feedback. Public store ratings (Apple / Google), not Rate us Submit. Read-only. **No Add new. No card view.**

Drawn: `Store reviews - Table View` (`7700:109625`), in section Reviews (`7699:81266`) to the right of Feedback detail.

### Snapshot (product 2026-09-11)

Two `.general info card` Property 1=2 (no 4-card `General info` wrapper), like Notifications’ two-card row:

| Card | Big number | Secondary |
|---|---|---|
| Total reviews | all store reviews | App Store · Google Store (counts) |
| Overall review | combined average | App Store · Google Store (ratings) |

Dummy: 1,248 / 842 · 406; overall 4.6 / 4.8 · 4.3. Icons: `message-square` (Dark blue) · `star` (Success).

Segmented **All / App Store / Google Store** filters the table only.

### Table columns (first pass)

Checkbox · **Name** · **Store** · **Rate** · **Review** · **Date** · **Actions** (View).

Store dummy: App Store / Google Store (product wording on this screen). Export table stays. View → full-page detail.

### Detail (single store review)

Drawn 2026-09-11: `Store reviews - Sara Al Maktoum` (`7704:82302`). Full page. Read-only. Name · Store · Rate · Date · Review. No Save, no reply, no delete. Dummy: Sara Al Maktoum, App Store, 5.0, 8 Sep 2026.

---

## Still unknown

- Feedback snapshot cards (product will share).
- Store table: title / version / country, or Name · Store · Rate · Review · Date is enough.
- Overall 4.6 = weighted combined average, or drop the combined number and keep only the two store ratings.
- Reply / flag on a store review (Feedback is read-only).
