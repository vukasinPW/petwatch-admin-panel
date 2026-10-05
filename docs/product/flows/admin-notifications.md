# Admin Notifications

Status: home snapshot + period locked 2026-09-01. Support send layout locked 2026-09-04 (Cloudflare). Support IA: sent list is home; create is a separate screen with Create new / Templates tabs. Sent detail locked 2026-09-04; recipients table locked 2026-09-11. Extra audience filters later (Summer). Sent-list columns still dummy.

Admin-Panel: `rc6tFk9QGVqOFD3ht9Upt8`  
FigJam cluster: `9:208` (Notifikacije + Push)

| Screen | Node | State |
|---|---|---|
| Home (platform) | `7582:70321` | Drawn |
| Period dropdown | `7582:100193` | Drawn |
| Detail (platform) | — | Later |
| Support list (sent) | `7616:81299` | Drawn — columns dummy |
| Support sent detail | `7646:74265` | Received / Opened by channel + copy + specs + recipients table |
| Support create (Cloudflare) | `7606:73604` · `7616:81241` | Locked layout |
| Support templates tab | `7616:81319` | Drawn — View / Use / ⋯ |
| Create template (full page) | `7638:71893` | Same send setups + Template title |
| Templates overflow | `7638:99470` | ⋯ → Make a copy · Delete |
| Make a copy | `7638:99639` | Dim 70% + 760: Template title · Cancel · Continue |
| Edit template | `8138:92523` | Dim 70% + 760 popup. Same fields as Create template, filled. Cancel · Save changes |
| Delete template | `7638:99808` | Dim 70% + 659 `Pop up` Error |
| After-send confirm | `7616:81356` | Drawn |
| Icons | FigJam `9:266` | Catalog lives under **Content → Notification icon** ([admin-catalog.md](admin-catalog.md)). Support create still has icon **out**. |

App prefs and inbox stay in [po-profile.md](po-profile.md). Per-person log stays on owner/sitter **Notification tracking**. Reassign still does **not** notify the owner ([booking-live-session.md](booking-live-session.md)).

---

## Why it exists

Ops needs one place for **every notification the platform sends**: volume, whether people open them, and the list of sends. Not Messages (PO↔PS threads). Support blasts have their own sent list + create + templates.

---

## Channels (locked)

Three. Not SMS (OTP only). Not chat cards in Messages.

| Channel | What it is |
|---|---|
| **In-app** | Row in the app Notifications list (still visible when they pause) |
| **Push** | Phone OS banner |
| **Email** | Including Necessary (always on in prefs) |

---

## Home

One page. Period at the top drives **cards + through-time + table**.

### Period

Same family as the list **Filter Date** panel, not a second invention. Control on the snapshot heading (Tertiary button + calendar), default **This month**.

| Option | Notes |
|---|---|
| This week | |
| Last week | |
| This month | Default |
| Last month | |
| Between … and … | Custom range |

### Snapshot (2 cards)

`General info` has no 2-card wrapper — two `.general info card` **Property 1=3** (hero + 3 secondaries), FILL in a 1128 row, gap 24.

| Card | Big number | Secondaries | Chip | Icon |
|---|---|---|---|---|
| Notifications sent | all three channels | In-app · Push · Email | Dark blue | `bell` |
| Open rate | overall % | In-app · Push · Email | Success | `percent` |

Hero may keep the card’s built-in vs-previous-period %. Do **not** add failed/bounce until we have that data. Unique recipients and click-through stay off the snapshot.

### Through time

On this page, under the cards. Sends over the selected period, series = in-app · push · email (total line optional). No second period button on the chart.

### Sections (table)

Segmented: **All** · **Marketing** · **General** · **Personal**. Filters the table only — snapshot stays the whole period.

### Table

Grain = **one send** (person + type + channel + opened), same object as Notification tracking, global. Columns: recipient · notification · category · channel · opened · date · view.

**Add new** on this hub still opens Support **create**. Support’s own home is the sent list. Export stays.

---

## Support Notifications

Sent list + create + templates. Extra audience filters (Summer) are out of this phase — the four Active Admin filters stay. A template stores the same setups as a send, plus **Template title**.

### Sent list (home)

Node `7616:81299`. Breadcrumbs: Home / Notifications / Support Notifications. **Add new** → create. Row **View** → sent detail.

Table columns are **dummy** until we lock them: Date · Title · Send to · Recipients · Channels · View.

### Sent detail

Node `7646:74265`. Breadcrumbs: Home / Notifications / Support Notifications / **Service update**. Title is the send Title. No tabs. No edit (already sent).

Two `.general info card` **Property 1=3** (hero + 3 secondaries), FILL in a 1128 row, gap 24. No vs-previous trend.

| Card | Big number | Secondaries | Chip | Icon |
|---|---|---|---|---|
| Received | unique users who got it | In-app · Push · Email | Dark blue | `bell` |
| Opened | unique users who opened | In-app · Push · Email | Success | `eye` |

Channel counts can overlap (same person, three channels). Dummy: Received 16,174 all three; Opened 10,028 — 8,412 / 6,201 / 4,890.

Then two `Card`s:

| Card | Rows |
|---|---|
| Notification | Title · Message · Date |
| Specifications | Send to · Channels · Users Status · Pet Status · Pet Type · City / Emirates |

Same dummy blast as create: All Users, all three channels, filters All, Title Service update, Message “We have an update about your PetWatch account.”, Date 3 Sep 2026, 14:20.

### Recipients table

On sent detail, under the cards. Grain = **one person** (not one channel). No View / no other CTA. Checkbox column stays (table chrome).

| Column | Cell | Notes |
|---|---|---|
| Title | Name | Recipient |
| Receiving date | Text | When they got this send |
| Open date | Text | First open on any channel; `—` if never |
| In-app · Push · Email | one column each | Only these three, because this blast used all three |

Channel cell, three states:

| State | Cell |
|---|---|
| Not sent | `Icon/-` dash |
| Sent, not opened | `Table status` **Not opened** (Pending color, no chevron) |
| Opened | **Opened** + success check |

Open date can be filled while some channel columns stay dash or Not opened (opened on one channel, not the others). Not opened was added on local `Table status` (`6431:1337`).

### Create (Cloudflare)

Node `7606:73604`. Layout locked. One page, not FigJam’s three-step. Pause, icon, and deep link stay out.

Tabs: **Create new** | **Templates**.

Breadcrumbs: Home / Notifications / Support Notifications / New.

| Block | Control | Options |
|---|---|---|
| Send to | Radio | All Users · Pet Sitters · Pet Owners |
| Channels | Checkbox | In-app · Push · Email (all on) |
| Users Status | Select | All (dummy) |
| Pet Status | Select | All · Registered · Approved — stays on Sitters too (sitters with that pet) |
| Pet Type | Select | All · Dog · Cat |
| City / Emirates | Select | All · 7 emirates |
| Users to notify | Read-only | Live count + first 5 sample emails |
| Title | Input | |
| Message | Text area | |
| Actions | | **Create template** Tertiary · Cancel Tertiary · **Send Notification** Primary Brand |

**Create template** is a **full page** (`7638:71893`), not the old 760 name/title/message popup. Same stacked setups as create, plus **Template title** first. Cancel · **Save template**. No Send. No Save as a draft.

**After send** still opens a confirm first (`7616:81356`): “Would you like to create a template from the sent message?” · checkbox **Don’t ask this again** (24px) · Cancel · Create template. Create template then opens the same full page, prefilled from the blast. Don’t ask this again skips this confirm on later sends.

### Templates tab

Node `7616:81319`. Same chrome, Templates selected. Search / Filter / Sort · **+ Create template** · table · pagination.

Table (dummy): checkbox · Updated · Name · Message · Preferences · View · Use · ⋯.

**Use** prefills Create new with the stored setups (audience, channels, filters, Title, Message).

**⋯** (`7638:99470`): **Make a copy** · **Delete**.

**Make a copy** (`7638:99639`): 760 overlay, **Template title** (dummy prefill Service update) · Cancel · Continue (Brand). Copy keeps the rest of the setups.

**Edit template** (`8138:92523`): popup on the templates list, dim 70% + 760. Every field from Create template, already filled (dummy Service update): template title, send to, channels, filters, users to notify, title, message. Cancel · **Save changes**. Not a full page.

**Delete** (`7638:99808`): regular 659 `Pop up` — “Are you sure you want to delete this template?” · Cancel · Delete (Error).

Starter template set is not locked — dummy is the existing **Service update** copy.

Entry: Notifications home **Add new**, or Support list **Add new**.

---

## Taken from the app

- Push categories: Marketing, General, Personal. Email adds **Necessary** (always on). Pause does not hide the in-app list.
- Inbox: unread, swipe-delete, mark as read.
- System events already fire (booking accept/cancel/pickup/done, review reminder, vaccine / microchip expiry = push + email).

---

## Still unknown

- Failed / bounce data — not on the snapshot until yes.
- Whether Support blasts also appear as rows on Notifications home, or only on the Support sent list.
- Starter template set — dummy is Service update until we pick.
- Sent-list columns — dummy until later.
- Whether Necessary is a fifth segmented item or only an Email attribute.
- What **View** on a template opens (edit vs read-only).
- Duplicate Template title on Make a copy — allowed or blocked.
