# Creating a pet profile (PO)

Status: captured from Figma 2026-08-18. Logic only — Figma copy is not product copy.

App Design: `fFkKBQPGIaM1Zjk9dz7LUW`  
Section: **Creating a pet profile** `23571:81318`  
Prototype (main path, not all branches): start `23571:81319`

Owner can also add a pet **through Profile** while identity is still pending (`po-verification.md`). This canvas starts from Home → Book a sitter hub with **identity already Completed**. Treat the wizard as the same create flow until product says otherwise.

---

## Gate

PO cannot book until **identity verified** + **at least one pet that is approved**.

### Now vs later (AI scanner)

Figma intro says scan = instant approve, manual = 24h. That is **long-term**.

**Now (testing phase, a couple of months):** the AI scanner is in testing. **Every** submitted pet still goes to **team review** (up to 24h). Hub **Your pet account is under review** is live. Booking stays blocked until the team approves.

**Later:** successful AI scan can **approve the pet instantly**; failed/unscannable stays on manual 24h.

This is intentional, not a bug. Admin must support the review queue **now**, and later a skip-queue path for good AI scans.

---

## Wizard (5 steps)

Progress bar is 5 circles throughout.

| Step | What |
|---|---|
| 1 | Pet passport pictures → scan → confirm fields |
| 2 | Vaccination record (mandatory **Rabies** + **DHPPi/DHPPiL**). Extra vaccines are a **side path**, not required |
| 3 | Additional info (size, health, feeding) |
| 4 | Pet photo + bio |
| 5 | Contacts (vet + emergency) |

---

## Step 1 — Pet passport

1. Hub **Create pet profile**.
2. **Let’s start with your pet’s passport** → Scan.
3. Prepare card: good / cut / glare / blur examples.
4. Upload slots. Picker: Take a photo / Gallery / (same pattern as ID). Native camera/gallery.
5. Photo actions: delete confirm (Delete / Keep).
6. Scanning loader (sitter stories carousel — same pattern as ID scan).
7. Outcomes:
   - **Scanned successfully** → confirm fields.
   - **Missing some info** → fill empty fields (canvas reuses ID-scan helper copy).
   - **Couldn’t scan** → Retake, or Contact us via WhatsApp / email.
8. Confirm / edit: **Pet type, Pet name, Gender, Breed, Date of birth, Microchip number**.

Canvas note: if **both** images are blurry or a random object → re-upload **both**. If only one failed → re-upload **that one**.

---

## Step 2 — Vaccination record

1. Prepare vaccination record (needs **Date given, Vaccination, Signature, Due date** visible — same good/glare/blur).
2. Two mandatory uploads: **Rabies**, **DHPPi/DHPPiL**. Each can show **Scanned successfully**.
3. Confirm: for each, **Vaccinated on** + **Vaccinated due**.
4. **Additional vaccinations** are optional. Prototype: after mandatory vacc success → reminder calendar → **Continue** goes to Additional info; **Upload other vaccines** opens Nobivac KC / Lepto / Deworming / Tick treatment (**Skip** back to Additional info).

Later (not create): **Vaccination expired** screen — redo the vaccine (**Try again**) or **Go back home**. Matches admin: expired mandatory vaccine → pet not bookable until redone.

---

## Step 3 — Additional info

Helps match sitters. Fields:

- Weight (kg) and Height (cm) — **ranges differ by pet type**
- Allergies Yes/No (+ free text if yes)
- Spayed/neutered Yes/No
- Medical condition Yes/No
- Feeding timing & instructions
- Additional info (optional)
- **Consent** (drawn; exact legal text **UNKNOWN**)

**Dog weight:** Toy 0–4 kg · small 5–10 · medium 11–24 · Large 25–44 · Giant 45+  
**Cat weight:** Mini 0–2.5 · Small 2.5–4 · Average 4.5–6 · Large 6.5–9 · Giant 10+  
**Cat height:** Under 23 cm · 23–30 · Over 30

---

## Step 4 — Pet photo & bio

Photo upload (same picker). **Bio optional** (counter 0/600). Whether photo is required like owner photo: **UNKNOWN** (Continue exists on empty-looking frames).

---

## Step 5 — Contacts

- Veterinarian name + phone
- Emergency contact name + phone  
(+971 prefix drawn)

Then **Your pet’s information has been submitted** → hub (identity Completed + **pet under review**) → Home. **Now:** still cannot book until team approves the pet.

---

## Admin hooks

- **Now:** all pet creates land in a **manual review queue** (up to 24h), even after a “successful” scan. Approve → pet bookable.
- **Later:** successful AI scan auto-approves; only failures go to the queue. Same admin surface should allow both.
- Payload: passport images, extracted + edited pet fields (incl. **microchip**), vaccine images + dates, optional extra vaccines, additional info, pet photo, contacts.
- **Vaccine expiry** (and later microchip expiry from admin spec) sends the pet back to not-bookable; owner sees redo, not a rejection reason.
- Scan fail → retake or Contact us (WhatsApp / email).

---

## Prototype (main path)

Start Home `23571:81319` → Book a sitter → hub → Create pet → passport intro → photos → camera → scan loader → confirm fields → passport success → vacc record → camera → loader → vacc success → reminder → Additional info → photo/bio → contacts → submitted → under-review hub → Home.

Side links exist (delete photo, extra vaccines, native pickers). Many error branches are **not** wired — canvas still wins for blur / missing / expired.

---

## Still unknown

- Same wizard from **Profile** — **yes** (`po-profile.md`).
- Photo required on step 4.
- Cat vs dog vaccine set (canvas is dog-labelled on expiry).
