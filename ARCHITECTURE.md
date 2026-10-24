# ARCHITECTURE — How Nivas Concierge is put together

*Plain-English guide to the machinery. Read this before changing code.*

## 1. The big picture
```
 Guest phone ──(scan QR)──► index.html on Netlify ──► Firebase Firestore (database)
                                                         ▲   │ live updates
 Reception PC ──(login)──► same index.html ─────────────┘   ▼
                                                    Reception sees request
```
- **One file** (`index.html`) contains the whole app: look (CSS), screens (HTML) and logic (JavaScript). No build step, no frameworks.
- **Netlify** just hosts that file publicly.
- **Firebase** is the shared notebook both sides read and write. "Live" = Firestore `onSnapshot` pushes changes to every open screen.
- **Same file, two faces:** with `?room=204` in the link it shows only the guest app. Without `?room=` it shows a demo picker plus the staff view (staff must log in).

## 2. Files
| File | What it is |
|---|---|
| `index.html` | The deployed app (identical copy of `concierge-firebase.html`) |
| `SETUP.md` | Step-by-step Firebase + Netlify setup for a non-coder |
| `docs/*.md` | These six documents |
| `room-XXX-qr.png` | QR cards, one per room |

## 3. Data (Firestore collections)
### `tickets` — every guest request
| Field | Meaning |
|---|---|
| `type` | Category: housekeeping, restaurant, minibar, spa, laundry, taxi, occasion, offer, activity, staff… |
| `guest`, `room` | Who and where |
| `items` | List of `{name, qty}` |
| `note` | Free text from guest or staff |
| `status` | `new` → `accepted` → `done` (also `rejected`, `pending` once added) |
| `at`, `acceptedAt`, `doneAt` | Time as display text (known weakness — see §7) |
| `createdAt` | Real timestamp number, used for sorting |
| `source` | `guest` or `staff` (new) |
| `reason` | Why rejected / pending (new) |

### `rooms` — one document per room number
`{ guest: "Name" | null, checkedInAt }`. Created automatically on first load.

### `feedback` (new) — one document per rating
`{ room, guest, stars (1–5), comment, createdAt }`

## 4. Who may do what (Firestore rules)
| Action | Guest (not logged in) | Staff (logged in) |
|---|---|---|
| Read tickets / rooms | ✅ (open — weakness) | ✅ |
| Create ticket | ✅ | ✅ |
| Update ticket (accept/done/reject) | ❌ | ✅ |
| Write rooms | ❌ | ✅ |
| Create feedback | ✅ (must have 1–5 stars) | ✅ |
| Read feedback | ❌ | ✅ |
| Delete anything | ❌ | ❌ |

Exact rules text lives in `SETUP.md`. After any rules change, press **Publish** in the Firebase console.

## 5. Inside the JavaScript
- **Data blocks** near the top: `HOTEL` (name), `ROOMS`, `HOUSE_INFO`, menus/`CATALOG`, `GUIDE`, `SERVICES`, and (new) `OFFERS`, `ACTIVITIES`. Changing a hotel = editing these.
- **State variables:** `tickets`, `cart`, `screen`, `ACTIVE_ROOM`, plus (new) `feedbackList`, `deskTab`, `reqFilter`.
- **Sync layer:** `initSync()` starts Firebase listeners; if config is missing it falls back to browser storage on one device (demo mode only).
- **Render functions** build HTML strings: `renderGuest`, `renderDesk`, `renderRooms`, `renderTiles`, `renderHeader`.
- **One click listener** reads `data-*` attributes on buttons (e.g. `data-act="accept"`). To add a button: add `data-act`, then handle it in that listener.
- **Actions:** `pushTicket`, `setStatus`, `checkIn`, `checkOut`, new `submitFeedback`, `addStaffRequest`.

## 6. Demo vs real
If Firebase fails to load, the app silently uses `localStorage` — good for offline demos, **not** for real hotels (guest and reception phones would not share data). The staff view shows a banner when running in local mode.

## 7. Known weaknesses (not hidden)
1. Times saved as text like "3:42 PM" — cannot be sorted or averaged reliably. Fix: store `createdAt` / `acceptedAt` / `doneAt` as numbers and format on screen (partly done: `createdAt` exists).
2. Guest can change `?room=`. Fix: per-room secret token.
3. Reads are open. Fix: tokens + tightened rules.
4. Old tickets remain after check-out; guest view filters by room + guest name so a new guest does not see them, but the data stays.
5. The hotel's Wi-Fi password lives in the page source. Acceptable for guests; do not put anything secret there.
6. "Log out" label on guest side does nothing.
7. Everything is hard-coded for "Kadamba Beach House".

## 8. Deploying a change
1. Edit `concierge-firebase.html`.
2. Copy it to a file named exactly `index.html`.
3. Netlify → site → **Deploys** → drag the file onto the drop zone.
4. Hard-refresh the browser (Ctrl+Shift+R) and test with a real `?room=` link.
