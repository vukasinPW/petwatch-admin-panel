# Admin Content / Catalog

Status: children locked 2026-09-04. Pet Services list drawn (table). Same shell for every child. Shared `Sidebar` on every catalog screen; selected child matches the page.

Admin-Panel: `rc6tFk9QGVqOFD3ht9Upt8`  
FigJam: Catalog `9:287` · Content `9:208` (FAQ, FAQ categories, Dashboard Content, Notification icons)

| Screen | Node | State |
|---|---|---|
| Services — list | `7626:89673` | Drawn (card grid) |
| Additional services | `7626:90065` | Same shell |
| Pet (types) | `7626:89575` | Same shell |
| Vaccines | `7626:89771` | Same shell |
| FAQ | `7626:89378` | Same shell |
| FAQ categories | `7626:89477` | Same shell |
| Content (one section) | `7626:89869` | Same shell |
| Notification icon | `7626:89967` | Same shell |
| Open (universal) | `7655:75163` | Drawn 2026-09-04 — image + text + Delete / Edit |

**Only these eight.** No videos, no T&C/policy CMS, no weight bands, no facilities list. Not a pet’s own profile or vaccination **record** — those stay on Pet Profiles.

---

## Why it exists

Ops edits the **platform lists** the app (and Help/FAQ) read. Sitters only opt in to Services / Additional. Owners browse the same SKUs. Vaccines gate pet approval. FAQ + one Content section + notification icons are the CMS side of the same parent.

---

## IA (locked 2026-09-04)

**Content** is one sidebar parent. Children are separate destinations. Breadcrumb: Home / Content / {child}.

| Child | What it is | App reads it |
|---|---|---|
| **Services** | Main SKU families + prices | Services tab, booking, sitter opt-in |
| **Additional services** | Add-ons (not bookable alone) | Booking add-on, sitter opt-in, Services info |
| **Pet** | Species types (Dog / Cat) + which services exist | Create pet, Services Dogs/Cats, sitter species |
| **Vaccines** | Vaccine list + mandatory vs optional | Create pet; expiry → not bookable |
| **FAQ** | Questions / answers | Help Center FAQ (canvas still says website — whether this CMS **is** that site: open) |
| **FAQ categories** | Buckets FAQs sit in | Same Help FAQ |
| **Content** | **One** section only (FigJam Dashboard Content) | That one surface — not a second CMS |
| **Notification icon** | Icon set for sends | In-app notification glyph. Support **create** still has icon **out** ([admin-notifications.md](admin-notifications.md)); this is the catalog when it turns on |

Every child uses the **same card-grid list**. **Open** is one popup for all eight — image + text + Delete / Edit. Dummy from Services (`Dog walking`).

---

## Open (universal)

Opens from any catalog card **Open**. Not a full page. Dim 70% + 760.

| Block | Component | Dummy (Services) |
|---|---|---|
| Title | `Pop up heading` | Dog walking |
| Image | `Upload image` Uploaded | Same photo as the card |
| Text | `Text area` | Lorem already on FAQ cards |
| Actions | Delete `Primary` `Error` · Edit `Primary` `Brand` | — |

No extra fields (species, SKU, price stay on the card). Edit / Delete destinations not drawn.

---

## Services — list

One **row per family**, not per SKU. View → detail + SKUs.

| Family | Species | SKUs | From (dummy) |
|---|---|---|---|
| Walking | Dogs | 30 min · 60 min | 55 AED |
| Home visit | Cats | 30 min · 60 min | 100 AED |
| Boarding | Dogs, Cats | Day care · Night care · Daily | 120 AED |
| Sitting | Dogs, Cats | Day care · Night care · Daily | 150 AED |

Prices **platform-fixed**. Walking = dogs only. Home visit = cats only.

---

## Admin hooks still open

- FAQ CMS vs Help “opens website FAQ” — same store or not.
- Notification icon: catalog only for now, or Support create picks from it.
- Add new on Services = new **family** or new **SKU**.
- Vaccine mandatory flag (changes pet-approval gate).
