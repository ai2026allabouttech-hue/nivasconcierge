# MEMORY — Running log of decisions and progress

*Update this file at the end of every work session. It is the project's brain: anything not written here will be forgotten.*

## Decisions (and why)
| Decision | Reason |
|---|---|
| Single `index.html`, no build tools | Founder is a non-coder; deploy = drag one file |
| Firebase Firestore + Email/Password auth | Free tier, live updates, no server to manage |
| One Firebase project per hotel | Data isolation, simple handover |
| Guests anonymous; only reception logs in | Guests will not create accounts |
| Netlify Drop hosting; file must be named `index.html` | Simplest hosting; wrong name gave "page not found" |
| Bottle green + brass design, not the reference app's blue/purple | Our own identity |
| Show "Rooms occupied", not "Revenue" | No billing exists; no invented numbers |
| PMS integration and billing deferred | Per-client paid add-ons |

## Facts
- Live URL: https://nivasconcierge.netlify.app (guest links use `?room=<number>`)
- Firebase project id: `nivas-concierge`
- Demo hotel rooms: 101, 204, 310 and others listed in `ROOMS` in the code
- Founder: Minu, Bengaluru, first-time vibe-coder
- Reference products: Athithi Concierge (guest app), a staff dashboard with Overview / Requests / Add Request (screenshots)

## Bugs we hit and how they were fixed (so we do not repeat them)
| Problem | Fix |
|---|---|
| Service buttons did nothing | Added generic catalogue screens |
| Dark mode: invisible bars | Separate `--deep` / `--on-deep` colours |
| Accept / Done stopped working | Firestore IDs are strings; stop converting to numbers |
| Only one room in reception | Seed each room document separately |
| Netlify "page can't be found" | Deploy file named exactly `index.html` |
| Staff login hidden on wide screens | `.gate-hidden` class that always hides |
| Guests could see reception | Hide staff UI when `?room=` is present |
| QR card title overflowed | Smaller font, no letter-spacing |

## Session log
- **Phase 1–5:** built app, fixed bugs, made pitch deck, added Firebase sync and login, deployed, made QR codes.
- **Phase 6 (this round):** wrote the six docs; building Offers, Activities, Feedback, tabbed staff dashboard, reject/pending, staff add-request form. 
  **Result:** all P0 items built and tested in a headless browser (guest phone size + desktop + phone-width staff view, no console errors). Added: Offers banner + screen, Activities with day/tag filters, Feedback stars, staff tabs (Overview / Requests / Rooms / Feedback), status filters, Reject and Pending with a reason the guest sees, staff "Add request" form, new `feedback` Firestore collection with its own rule.
  **Not yet verified live:** the Firebase path (rules for `feedback`, real-time sync of new statuses). Tested only in demo/local mode. Needs a real check after redeploy + publishing rules.
  **Sample content:** offers and activities are placeholders, not a real hotel's.

## Open questions for the founder
1. Which hotel is the first pilot, and how many rooms?
2. Real offers and activity list for the pilot hotel (current ones are sample content).
3. Final product name?
4. Who at the hotel creates / owns staff logins?
