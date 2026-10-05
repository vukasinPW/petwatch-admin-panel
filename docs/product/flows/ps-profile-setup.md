# PS profile setup (after Academy)

Status: captured from Figma 2026-08-18. Logic only.

App Design: `fFkKBQPGIaM1Zjk9dz7LUW`  
Section: **Setting up your profile** `24071:219686`  
Prototype start: `24071:221517`

This is **not** identity verification and **not** Academy. After the sitter **finishes Academy (web)**, they must complete this setup to become **visible to pet owners** and able to receive services/bookings.

Bank + photo already happened at verification. This is the **operating profile**: services, availability, environment, address.

---

## Entry

Home still looks like pre-Academy until they finish this. Overlay: **Congratulations! You finish academy successfully!** → **Continue** → wizard.

Until this wizard is done they are **not live** (not visible, not receiving requests). Availability toggle on Home remains gated until Academy + this setup (`home.md`).

---

## Wizard (5 steps)

| Step | What |
|---|---|
| 1 | Species (dog / cat / both) + **main services** |
| 2 | **Additional services** (add-ons owners pick after a main service) |
| 3 | **Availability** (days + hours) |
| 4 | **Environment** (photos, smoking, other pets, facilities) |
| 5 | **Address** |

Then success: **Your Profile Is All Set Up! You're Now Live!** → Home with **Your bookings** + **Earnings** (empty).

---

## Step 1 — Main services

First: **Dog services / Cat services / Dog & cat services**.

Then catalog (Select all allowed):

**Dogs:** Walking (30 min / 60 min) · Boarding (Day care / Night care / Daily) · Sitting (Day care / Night care / Daily)

**Cats:** Home visit (30 min / 60 min) — no Walking · Boarding · Sitting (same structure, different example prices)

Canvas shows **prices** next to each SKU. **Product:** prices are **fixed by the team**, identical for **all sitters**. Sitters select which services they offer; they do not set rates. Admin owns the catalog.

If they chose **both** species, they go through dog list then cat list (prototype).

---

## Step 2 — Additional services

Add-ons; owners attach them after choosing a main service.

**Dog add-ons drawn:** Feeding at your place · additional 30 min walk · Bottled water · Medicine administration · Basic Grooming

**Cat add-ons drawn:** Feeding at your place · Litter box cleaning · Bottled water · Medicine administration · Basic Grooming

Select all per species. Continue → Availability.

---

## Step 3 — Availability

- Days: Mon–Sun (multi-select)
- Hours per day (example 09:00–17:00)
- **Use same hours for all days** toggle
- Add extra intervals (plus) — e.g. a second range 00:00–22:00 on canvas

This is the **weekly working window**. Separate from the Home pause-availability control (that only hides them for **new** services after they are live).

---

## Step 4 — Environment

- Environment picture(s)
- Smoking allowed? Yes/No
- Pets at home? Yes/No → if yes: Dog / Cat / Other (free text, e.g. Parrot) + **Add another pet**
- Facilities (multi-select): Indoor play area · Pet-friendly amenities · Open spaces · Proximity to parks · Fenced yard · Separate areas for different pets

---

## Step 5 — Address

Search or **Use current location** (iOS location permission). Then:

- Type: **House/villa** or **Apartment**
- House/villa (or apt) number
- Area/community
- Street optional
- Additional instructions optional

---

## After live

They are **visible to pet owners** and can receive booking requests. Home switches to bookings + earnings.

---

## Admin hooks

- Status after this wizard = **Approved** (visible / live). **Graduated** = Academy confirmed, still in this wizard (`academy.md`).
- Need to see: services + add-ons offered, weekly availability, environment, address, live flag.
- **Prices and SKUs are edited only in admin.** Sitters only opt in. Same catalog for every sitter.

---

## Prototype

Main path is wired: Academy success → species → dog/cat services → add-ons → availability (days/hours/same-hours/extra slot) → environment (pets/facilities) → address type/details → **Now Live** → Home bookings.

Not every environment/address micro-state is linked; canvas still wins for those.

---

## Still unknown

- How many environment photos are required.
