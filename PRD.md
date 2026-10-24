# PRD — Nivas Concierge (Product Requirements)

*Plain-English version. "PRD" = a document that says **what** we are building and **why**, before anyone worries about **how**.*

## 1. One-line pitch
A QR code in every hotel room opens a simple guest web page (no app download). The guest taps what they need — housekeeping, food, spa, taxi — and the request appears **instantly** on the reception screen, where staff accept it and mark it done.

## 2. The problem
- Guests call reception for every small thing; lines are busy, requests get forgotten.
- Reception tracks requests on paper, WhatsApp or memory — no record of who asked what, when, and whether it was done.
- Hotels cannot easily promote their own spa, restaurant or activities to guests already inside the building.
- Managers get no feedback until a bad online review appears.

## 3. Who uses it
| Person | What they want | Where they use it |
|---|---|---|
| **Guest** | Ask for something in 2 taps, see that it was received, find local places | Phone browser via room QR (`?room=204`) |
| **Receptionist** | See new requests live, accept, finish, log phone-in requests | Reception PC/tablet (needs staff login) |
| **Manager / MD** | See volume, speed, ratings; trust the data | Same dashboard, Overview + Feedback tabs |
| **Us (the startup)** | Set up a new hotel in under a day | One file copy + one Firebase project per hotel |

## 4. Features — status today
Legend: ✅ built and live · 🟡 partly built · ⬜ not built

### Guest app
| Feature | Status |
|---|---|
| Room-specific QR links (`?room=204`) | ✅ |
| Housekeeping, Restaurant, Mini bar, Spa, Laundry, Taxi, Special occasion | ✅ (all create a request) |
| House & Wi-Fi info, Goa guide (with real map links), Contacts | ✅ |
| See own request status (New → Accepted → Done) | ✅ |
| Offers (banner + screen, "claim" creates request) | ⬜ → building now (TASKS P0) |
| Activities (schedule, kids filter, reserve) | ⬜ → building now |
| Feedback (stars + comment) | ⬜ → building now |
| Prices / bill on the guest screen | ⬜ (deferred, see §7) |
| Multi-language | ⬜ |

### Reception / staff
| Feature | Status |
|---|---|
| Staff login (Firebase email + password) | ✅ |
| Live request list, Accept, Mark completed | ✅ |
| Rooms screen: check guest in / out, see occupied | ✅ |
| Tabbed dashboard: Overview, Requests table with filters | ⬜ → building now |
| Reject / Pending status with reason | ⬜ → building now |
| Staff "Add request / reservation" form (phone-in) | ⬜ → building now |
| Feedback tab | ⬜ → building now |
| Staff user roles (manager vs receptionist) | ⬜ |

## 5. Success measures (what "working" means)
1. A guest request shows on reception in **under 3 seconds**.
2. A receptionist can accept and complete a request in **2 taps**.
3. A new hotel goes live in **under one day**, by a non-coder following SETUP.md.
4. Reception **stops using WhatsApp** for guest requests (check after 2 weeks of a pilot).
5. At least **30% of guests** who use the app leave a rating.

## 6. What we will NOT build (for now)
- **Revenue figures.** No billing exists, so any revenue number on the dashboard would be invented. We show *rooms occupied* instead.
- **Hotel software (PMS) integration.** Sold later as a paid add-on per hotel.
- **Online payments.** Charges are added to the room bill by the hotel.
- **A native phone app.** The browser page is the product.

## 7. Business decisions already made
- One Firebase project **per hotel** (data isolation, simple billing).
- One copy of the app file per hotel for name, rooms, menus and colours.
- Billing model when added: housekeeping free; other services charged to the room folio.
- Hosting: Netlify. Live demo: https://nivasconcierge.netlify.app

## 8. Risks (honest list)
| Risk | Why it matters | Plan |
|---|---|---|
| A guest can edit `?room=` in the link and see another room | Privacy | Short-term: random room token in QR. See TASKS P1 |
| Anyone with the project config can read tickets | Guest names exposed | Move reads behind a per-room token. TASKS P1 |
| Hotels already use WhatsApp | Adoption | Pilot with one hotel, measure success #4 |
| Product name "Nivas" is a placeholder | Branding / trademark | Check trademark before first paid client |
