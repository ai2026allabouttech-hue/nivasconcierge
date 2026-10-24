# Getting this live — a walkthrough for a non-coder

This is written assuming you've never touched Firebase before. It's about
15 minutes, and everything in Steps 1–2 is free.

---

## Step 1 — Create your Firebase project (5 min)

1. Go to https://console.firebase.google.com and sign in with any Google account.
2. Click **Add project**. Name it anything (e.g. "kadamba-concierge"). You can
   turn off Google Analytics when asked — you don't need it.
3. Once the project opens, click the **`</>`** (web) icon on the project's home
   screen to register a web app. Give it any nickname and click **Register app**.
4. Firebase will show you a block of code containing a `firebaseConfig` object
   that looks like this:

   ```js
   const firebaseConfig = {
     apiKey: "AIza...",
     authDomain: "kadamba-concierge.firebaseapp.com",
     projectId: "kadamba-concierge",
     storageBucket: "kadamba-concierge.appspot.com",
     messagingSenderId: "123456789",
     appId: "1:123456789:web:abc123"
   };
   ```

   **Copy these six values.**

5. Open `concierge.html` in any text editor, find this block near the top of
   the `<script>` section (search for `PASTE_YOUR`), and replace each
   placeholder with your real value:

   ```js
   var firebaseConfig = {
     apiKey: "PASTE_YOUR_API_KEY_HERE",
     authDomain: "PASTE_YOUR_PROJECT.firebaseapp.com",
     projectId: "PASTE_YOUR_PROJECT_ID",
     storageBucket: "PASTE_YOUR_PROJECT.appspot.com",
     messagingSenderId: "PASTE_YOUR_SENDER_ID",
     appId: "PASTE_YOUR_APP_ID"
   };
   ```

6. Save the file.

## Step 2 — Turn on the database (2 min)

1. In the Firebase console's left sidebar, click **Build → Firestore Database**.
2. Click **Create database**. Choose any nearby location. Start in
   **test mode** for now (you'll tighten this below).
3. Once it's created, click the **Rules** tab and replace everything with:

   ```
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /rooms/{roomId} {
         allow read: if true;
         allow write: if request.auth != null;
       }
       match /tickets/{ticketId} {
         allow read: if true;
         allow create: if true;
         allow update: if request.auth != null;
         allow delete: if false;
       }
       match /feedback/{fid} {
         allow create: if request.resource.data.stars is number
                       && request.resource.data.stars >= 1
                       && request.resource.data.stars <= 5;
         allow read: if request.auth != null;
         allow update, delete: if false;
       }
     }
   }
   ```

   **Updating an existing project?** The new `feedback` block is the only
   addition. Paste the full text above over your old rules and press
   **Publish**, otherwise guests' star ratings will be refused.

   Click **Publish**.

   **What this actually means:** anyone can read live data (so a guest can
   see their own request update without logging in), and anyone can send a
   new request (so guests never need an account). But only a *signed-in*
   user can check a guest in/out, or touch an existing request (Accept,
   Mark as completed) — that's reception, and reception only. This is
   real protection, not just a UI toggle: even someone who inspects the
   page's code can't perform those actions without signing in, because
   Firestore itself enforces it.

## Step 2.5 — Create a reception login (2 min)

This is what makes Step 2's rules actually work — without it, reception
will be stuck at the sign-in screen with nothing to sign in with.

1. In the Firebase console's left sidebar, click **Build → Authentication**.
2. Click **Get started**, then choose **Email/Password** from the list of
   sign-in providers, and turn it **On**. Save.
3. Go to the **Users** tab and click **Add user**. Enter an email and
   password for your reception staff to use (this can be anything — it
   doesn't need to be a real, working email address, it's just a login).
4. That's the login your reception desk uses to sign in — give it to
   whoever's on shift. Add more users here for more staff logins later.

   **Note:** the app itself never asks a guest to sign in — this screen
   only ever appears on the "Reception desk" side.

## Step 3 — Put it online (5 min)

You need somewhere to host the HTML file so it has a real, public web
address. Two easy, free options:

**Option A — Netlify (easiest, no account needed to start)**
1. Go to https://app.netlify.com/drop
2. Drag `concierge.html` straight onto the page.
3. It gives you a live URL immediately (like `random-name.netlify.app`).
   That's it — that's your hotel's app.

**Option B — Firebase Hosting (since you already have a Firebase project)**
1. This one needs a terminal — if that's unfamiliar, use Option A instead.
2. `npm install -g firebase-tools`, then `firebase login`, then
   `firebase init hosting` inside a folder containing `concierge.html`
   (rename it to `index.html` first), then `firebase deploy`.

## Step 4 — Print your room QR codes

Once you have a real URL (say `https://kadamba-concierge.netlify.app`),
each room's QR code should point to that URL **plus its own room number**:

```
https://kadamba-concierge.netlify.app/?room=101
https://kadamba-concierge.netlify.app/?room=204
https://kadamba-concierge.netlify.app/?room=310
```

Generate each one as a QR code (any free QR generator online works), print
it, and place it in that room. Add any new room to the `ROOMS` list near the
top of the file's `<script>` section first, the same way `101`, `204`, and
`310` are listed.

---

## What you get once this is done

- A guest scans the QR in Room 204 → the app already knows it's Room 204
- They send a request → it appears on reception's screen, anywhere, within
  a second or two — no longer limited to people signed into your own
  account
- Check a guest in or out from the Rooms panel → every device reflects it
  live
- Only staff who've signed in can accept a request, mark it complete, or
  check a guest in or out — enforced by the database itself, not just
  hidden in the interface

## What's still worth knowing

- Reads are still open to anyone with the link (so a guest never needs to
  sign in to see their own request update) — only the *actions* that
  matter (accepting, completing, checking guests in/out) require a
  reception login. That's a deliberate, reasonable line for a pilot.
- Every reception staff member shares logins you create manually in the
  Firebase console (Step 2.5). If you outgrow that — many staff, several
  properties, individual accountability per staff member — that's a
  natural next step, and a fairly small one from here. Ask me when you're
  there.
- Firebase's free tier is generous (roughly 50,000 reads and 20,000 writes
  a day) — comfortably enough for a single property's pilot. It only
  starts costing money past that, and you'd see it coming in the Firebase
  console's usage tab well before it did.
