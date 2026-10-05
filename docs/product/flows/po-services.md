# PO Services tab

Status: captured 2026-08-18. Logic only.

App Design: `fFkKBQPGIaM1Zjk9dz7LUW`

| Topic | Node |
|---|---|
| Dog services | `21468:161680` |
| Cat services | `21468:163132` |

---

## Why it exists (product)

**Explore** before commit — especially **guests** and people who are not sure they will use the app. See what PetWatch offers and **prices** (same **platform-fixed** catalog as booking / sitter setup).

List: species (Dogs / Cats) → family (Walking, Boarding, Sitting / Home visit) → SKUs with From X AED, Learn more. Detail: options, Details. Add-on pages exist (feeding, extra walk, water, medicine, grooming, litter) as **info only**.

**Add-ons cannot be booked alone** — only attached to a main service in the booking wizard.

---

## Book CTA (now)

**Book now** on a specific SKU will be **removed for now** (too many branches: one pet vs many, which booking path). Deep-link “book this SKU” is future.

Whatever Book remains on the tab is a generic start of **service-first booking** (`booking-po-general.md`), not a pre-selected SKU.

---

## Guest / gated

- **Guest:** full catalog + **prices**, no account. Book → Log in / Sign up (same guest popup as Home).
- **Logged in, not verified:** same browse. Book → **verify + pet** gates (same as Home).

---

## Admin

This tab is the public view of the **same catalog** sitters opt into. **SKUs and prices are edited only in admin.** Sitters only opt in; they do not set prices.
