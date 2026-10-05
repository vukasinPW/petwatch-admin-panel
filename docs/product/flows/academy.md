# Sitter Academy

Status: **logic captured** from product 2026-08-18. In-app screens / web UI not captured yet.

Academy is **not an in-app course**. It happens **on the web**. The app is **connected**: when the sitter confirms/completes Academy on the web, the app unlocks the next step.

Long term: more of this may live in the app. **Now:** web Academy + app status sync.

---

## Gate to join

From the app, **Join academy** unlocks only when:

1. Team has **verified** the profile (manual identity up to 24h, or UAE PASS instant), **and**
2. **IBAN is approved** by **Mamo Pay** (fast, ~1–2 minutes). Admin does not set this status.

See `ps-verification.md` and `home.md`. There is no 24h “Academy application” queue.

**Join academy** in the app sends them to the **web** Academy. Exact open method (Safari / in-app browser / deep link) is **UNKNOWN**.

---

## After they confirm Academy (web)

1. App shows **Congratulations! You finish academy successfully!**
2. They must **set up the operating profile** in the app (services, add-ons, availability, environment, address) — `ps-profile-setup.md`.
3. Only then they are **live / visible to pet owners** and can receive bookings.

Until Academy is confirmed **and** this setup is done, they are **not** visible. Availability toggle stays gated.

Bank + photo already happened at verification. This setup is not identity.

Lifecycle already used in admin: **Registered → Verified → In academy → Graduated → Approved**. Mapping (product confirmed):

| After | Status |
|---|---|
| Verified + IBAN ok, not yet confirmed Academy | Verified (can join) |
| On the web Academy, not confirmed | In academy |
| Confirmed Academy, setting up operating profile | **Graduated** |
| Setup complete, visible to owners | **Approved** |

---

## Admin hooks

- Academy lives on **web**. Admin likely needs: started / confirmed (or equivalent), and the sync into app status.
- Completing Academy unlocks **profile setup** (`ps-profile-setup.md`); finishing that makes them **visible to POs**.
- Availability / “visible for new services” is after Academy complete.

---

## Still unknown

- Web Academy URL / CMS / who marks confirm.
- In-app Join academy → how the web opens.
- The post-Academy profile setup screens — captured in `ps-profile-setup.md`.
