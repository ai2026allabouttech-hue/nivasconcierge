# RULES — How we build (for you and for any AI helping you)

*Paste this file at the start of any AI coding session so it follows the same house rules.*

## A. Working style
1. **Explain in simple English.** The founder is not a coder. After each change, say what each changed line does and what could go wrong.
2. **One change at a time.** Finish, test, then move on.
3. **Never break what works.** Guest ordering and the reception Accept / Done flow must keep working after every edit.
4. **Ask before anything that cannot be undone** (deleting data, changing Firebase rules, renaming the site).
5. **Be honest about gaps.** If something is a demo, say so. No invented numbers.

## B. Code rules
1. Keep the **single-file** structure (`index.html`). No build tools, no new frameworks.
2. Use the existing **colour variables** (`--moss`, `--brass`, `--paper`...). Never type a raw colour code inside a component.
3. Every colour must work in **dark mode** too.
4. Buttons use `data-act="..."`; handle them in the one click listener.
5. Firestore IDs are **strings**. Compare with `String(a) === String(b)`; never `Number()` them.
6. Guest screens must **never** show reception controls. Use `ROOM_FROM_URL` / `.guest-only`.
7. Anything saved to Firebase needs a **local fallback** so demo mode still works.
8. Use `textContent` or the existing escape helper for guest-typed text. Never paste guest text straight into HTML.
9. No secrets in code except the Firebase web config (which is designed to be public). **Never** paste passwords or service-account keys.
10. Do not store money amounts we cannot back with real billing.

## C. Before every release (checklist)
- [ ] JavaScript syntax check passes.
- [ ] Open `?room=204` on a phone-size window: all tiles open, a request is sent.
- [ ] Log in at the staff URL: the new request appears within seconds.
- [ ] Accept, then Complete: the guest screen updates.
- [ ] Reject with a reason works (guest sees it).
- [ ] Dark mode looks right.
- [ ] Guest link shows **no** staff controls.
- [ ] Firestore rules published if they changed.
- [ ] `index.html` is an exact copy of `concierge-firebase.html`.
- [ ] MEMORY.md updated.

## D. Data and privacy rules
- Collect only: guest name, room, requests, optional rating comment.
- No phone numbers, ID documents or payment details in the app.
- Each hotel's data lives only in that hotel's Firebase project.
- Staff accounts are created by us in Firebase Authentication; no public sign-up.

## E. Naming
- Product (placeholder): **Nivas Concierge**. Demo hotel: **Kadamba Beach House**.
- Status words shown to people: **New, Pending, In progress, Solved, Rejected**. Stored values: `new, pending, accepted, done, rejected`.

## F. Things AI helpers must NOT do
- Do not rewrite the whole app when asked for a small fix.
- Do not change the design language (bottle green + brass) to match another product.
- Do not add fake data (revenue, ratings, reviews) to the real dashboard.
- Do not loosen Firestore rules to "make it work" — explain the error instead.
