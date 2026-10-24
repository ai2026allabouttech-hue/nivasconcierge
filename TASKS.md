# TASKS — The backlog

Legend: ⬜ to do · 🔨 in progress · ✅ done. **P0** = do now, **P1** = before the first paying hotel, **P2** = later.

## Done earlier
- ✅ Guest app: 7 services, house info, Goa guide, contacts
- ✅ Reception: live list, Accept, Complete
- ✅ Rooms screen (check-in / check-out)
- ✅ Firebase live sync + staff login + locked rules
- ✅ Netlify deploy, QR cards, pitch deck (8 slides)

## P0 — built this round (live check after redeploy still pending)
| # | Task | Done when |
|---|---|---|
| ✅ P0-1 | Guest **Offers** (banner + screen, Claim → request) | Claim appears on reception as category "Offer" |
| ✅ P0-2 | Guest **Activities** (day + tag filters, Reserve → request) | Reserve appears on reception as "Activity" |
| ✅ P0-3 | Guest **Feedback** (stars + comment → `feedback` collection) | Rating visible in staff Feedback tab |
| ✅ P0-4 | Staff **tabbed dashboard**: Overview, Requests, Rooms, Feedback | All four tabs render with live data |
| ✅ P0-5 | **Requests table** with filters New / Pending / In progress / Solved / Rejected | Counts match the list |
| ✅ P0-6 | **Reject** and **Pending** with reason; guest sees status | Reason shown on guest card |
| ✅ P0-7 | Staff **Add request / reservation** form | Ticket tagged `source: staff` |
| ✅ P0-8 | Update Firestore rules for `feedback` in SETUP.md | **Founder must paste + Publish the new rules** |
| ✅ P0-9 | Test on phone and desktop sizes (light mode checked; dark mode not yet screenshot-tested) | Screenshots checked |

## P1 — before first paying hotel
| # | Task | Why |
|---|---|---|
| P1-1 | Per-room **secret token** in QR link (`?room=204&k=xxxx`) and rules that check it | Stops guests peeking at other rooms |
| P1-2 | Store all times as numbers; show formatted | Allows response-time stats |
| P1-3 | Tighten reads (guests read only their own room's tickets) | Privacy |
| P1-4 | Move hotel data (name, rooms, menus, offers, activities) into one `HOTEL_CONFIG` block or Firestore doc | Faster onboarding of hotel #2 |
| P1-5 | Staff roles (receptionist vs manager) | Managers see Feedback and stats only |
| P1-6 | Sound / browser notification on new request | Staff notice requests without staring |
| P1-7 | Check-out clears the room's old requests from guest view and archives them | Clean slate for next guest |
| P1-8 | Fix guest "Log out" label | Currently does nothing |
| P1-9 | Trademark check on "Nivas" | Before printing materials |
| P1-10 | One-page onboarding checklist for a new hotel | Under one day setup |

## P2 — later
- Prices on menu items + room-folio export (CSV)
- PMS integration (paid add-on)
- Hindi / Kannada / other languages
- Response-time report (needs P1-2)
- WhatsApp or SMS alert to the duty manager
- Custom domain per hotel
- Image upload for offers and activities

## Hotel setup checklist (use for each new client)
1. Create Firebase project; enable Firestore and Email/Password login.
2. Add reception users.
3. Paste rules from SETUP.md and Publish.
4. Copy `index.html`; edit hotel name, room list, menus, offers, activities, Wi-Fi.
5. Paste Firebase config.
6. Deploy to Netlify.
7. Generate and print room QR cards.
8. Test with one real phone and the reception PC.
