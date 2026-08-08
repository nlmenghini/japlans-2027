# Tokyo ⟷ Kyoto Trip App — Setup

This folder is a complete, installable web app. Two steps to get it live: connect voting, then host it.

## 1. Connect live voting (Firebase — free, ~5 min)

1. Go to https://console.firebase.google.com and sign in with any Google account.
2. Click **Add project**. Name it anything (e.g. "trip-planner"). You can skip Google Analytics.
3. In the left sidebar, go to **Build → Realtime Database**. Click **Create Database**.
   - Choose any region.
   - Select **Start in test mode** (this allows the app to read/write without a login system — fine for a small private group with an unguessable URL, but don't put sensitive data in it).
4. In the left sidebar, click the **gear icon → Project settings**. Scroll to **Your apps**, click the **</> (Web)** icon to register a new web app. Give it any nickname, no need for hosting.
5. It will show a code block starting with `const firebaseConfig = { ... }`. Copy those key/value pairs.
6. Open `firebase-config.js` in this folder and paste your values in, replacing the `PASTE_YOUR_...` placeholders.
7. In the Realtime Database **Rules** tab, confirm rules allow read/write (test mode sets this automatically for 30 days — for a trip this short that's fine, but you can extend it: set both `.read` and `.write` to `true`).

That's it — voting will now sync live across everyone's phones.

## 2. Host it (GitHub Pages — free, no server needed)

1. Go to https://github.com and create a free account if you don't have one.
2. Click **New repository**. Name it e.g. `trip-app`. Set it to **Public**. Create it.
3. On the repo page, click **Add file → Upload files**, then drag in every file from this folder (`index.html`, `manifest.json`, `service-worker.js`, `firebase-config.js`, and the whole `icons` folder). Commit.
4. Go to the repo's **Settings → Pages**. Under "Build and deployment", set **Source: Deploy from a branch**, branch **main**, folder **/(root)**. Save.
5. Wait ~1 minute, then refresh — GitHub shows your live URL, something like:
   `https://yourusername.github.io/trip-app/`

That URL is what you send to your party.

## 3. Add to home screen (each person does this once)

**iPhone (Safari):** open the link → tap the Share icon → **Add to Home Screen**.
**Android (Chrome):** open the link → tap the ⋮ menu → **Install app** (or **Add to Home Screen**).

It'll launch full-screen with its own icon, like a normal app. The Route tab works fully offline once opened once; the Vote tab needs a connection to sync, but shows the last-known votes if you're offline.

## Updating content later

If you want to change dates, add day trips, or tweak text, edit `index.html` directly (the `TRIPS` array and the timeline HTML), then re-upload the changed file to GitHub — Pages redeploys automatically in under a minute.
