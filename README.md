# Home Workout Tracker

A mobile-first weekly home workout tracker. Tick off sets, track time, see streaks and history. Progress syncs live through Firebase Firestore, so two people can follow the same tracker from different phones.

## Files

| File | What it is |
|---|---|
| `index.html` | The whole app (plan, UI, sync) |
| `firebase-config.js` | Your Firebase keys + the private space id |
| `firestore.rules` | Database security rules to paste into Firebase |
| `manifest.json`, `icon-*.png`, `apple-touch-icon.png` | Home-screen app icon |
| `.nojekyll` | Tells GitHub Pages to serve files as they are |

## Setup

### 1. Firebase (database)

1. Go to https://console.firebase.google.com and click **Create a project**. Name it `home-workout`. Turn Google Analytics off.
2. Left menu: **Build → Firestore Database → Create database**.
   - Location: `asia-south1 (Mumbai)`
   - Start in **production mode**
3. Open the **Rules** tab, replace everything with the contents of `firestore.rules`, click **Publish**.
4. Click the gear icon → **Project settings** → scroll to **Your apps** → click the web icon `</>`.
   - Nickname: `workout`. Don't tick Firebase Hosting. Click **Register app**.
5. Copy the values from the `firebaseConfig` object shown and paste them into `firebase-config.js`, replacing the `PASTE_...` values. Leave `SPACE_ID` as it is.

The Firebase web `apiKey` is meant to be public. The rules plus the long `SPACE_ID` are what keep the data private.

### 2. GitHub Pages (website)

```bash
cd home-workout
git init
git add .
git commit -m "Home workout tracker"
git branch -M main
git remote add origin https://github.com/<your-username>/workout.git
git push -u origin main
```

Then on GitHub: repo **Settings → Pages → Build and deployment → Source: Deploy from a branch → Branch: main, / (root) → Save**.

After about a minute the site is live at:

```
https://<your-username>.github.io/workout/
```

### 3. Check it works

Open the link. The chip at the top right should say **Live sync** (green dot). If it says **This device only**, `firebase-config.js` still has placeholder values.

### 4. Add to home screen

- **iPhone (Safari):** Share button → **Add to Home Screen**
- **Android (Chrome):** ⋮ menu → **Add to Home screen** / **Install app**

## Free tier

Firestore's free plan allows 50,000 reads and 20,000 writes per day. One person's daily workout uses a few hundred at most.
