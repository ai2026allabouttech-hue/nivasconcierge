# DESIGN — Look and feel

## Principles
1. **Calm luxury, fast to use.** A tired guest at night should finish a request in 2 taps.
2. **Phone first** for guests; **wide screen first** for reception.
3. **Request vs. answer look different.** Guest actions use one colour family; staff actions another (this was an explicit founder request).
4. **Never copy another brand.** Our identity is bottle green + brass.

## Colours (variables in the CSS)
| Name | Use |
|---|---|
| `--paper` | Card / page surface |
| `--stone` | App background |
| `--ink`, `--ink-soft` | Main and secondary text |
| `--line` | Thin borders |
| `--brass` | Accent, highlights, offers |
| `--moss` | Success, "done" |
| `--bubble` | Guest chat-bubble tint |
| `--alert` | Needs attention, "rejected" |
| `--teal`, `--slate` | Section colour-coding (House & Wi-Fi, Guide, Contacts) |
| `--deep` / `--on-deep` | Dark green bars and the text on them (fixed in both light and dark mode) |

Dark mode is automatic (`prefers-color-scheme`).

## Status colours
| Status | Label | Colour |
|---|---|---|
| new | New | brass |
| pending | Pending | slate |
| accepted | In progress | teal |
| done | Solved | moss |
| rejected | Rejected | alert |

## Type
- Headings: **Cormorant Garamond** (serif, elegant).
- Body and buttons: **Karla** (sans, readable).
- Minimum body size 14 px on phone. Tap targets at least 44 px tall.

## Guest app layout
- Top bar: hotel name, room, guest name.
- Home: greeting → **Offer banner** (brass) → service tiles → request history feed.
- Each service opens a simple list → cart → "Send request".
- **Offers**: card per offer with title, short text, validity, "Claim" button.
- **Activities**: day filter chips (Today / Tomorrow), tag chips (Kids, Pool, Wellness, Culture), cards with time and "Reserve".
- **Feedback**: 5 big stars, optional comment, "Send".

## Staff dashboard layout (wide screens)
Left: **Rooms** panel (existing). Right: tabbed area.
1. **Overview** — four stat cards (New requests, In progress, Completed, Rooms occupied) → "Requests by category" donut → recent requests.
2. **Requests** — status filter chips with counts (All, New, Pending, In progress, Solved, Rejected) → table: ID, Room/Guest, Category, Details, Time, Status, Actions → **+ Add request** button.
3. **Rooms** — occupancy summary (the existing room list is also shown on the left).
4. **Feedback** — average rating, count, list of comments.

On phones (<860 px) the staff view stacks vertically and tabs scroll sideways.

## Accessibility
- Every colour pair has at least 4.5:1 contrast in both modes.
- Status is never colour-only; the word is always shown.
- Buttons are real `<button>` elements so keyboard users can reach them.

## Don'ts
- No emoji as the only label for a function.
- No more than two font families.
- No animation longer than 300 ms.
