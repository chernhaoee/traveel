# Traveel

Shared group-trip app, first used for the Dec 19 – Jan 4 Japan trip: day-by-day plan, spending split (yen → ringgit, bank charge comparison), to-dos, shopping list, notes, ticket uploads, roles and an activity log.

- **Hosting:** GitHub Pages (this repo)
- **Login + data:** Firebase (Google sign-in + Cloud Firestore), free Spark plan is enough
- **Roles:** Admin (owner) · Planner (edit) · Traveler (view only), enforced by `firestore.rules`

## One-time setup (~10 min)

### 1. Firebase project
1. Go to <https://console.firebase.google.com> → **Add project** → name it e.g. `traveel` → you can turn Google Analytics off → **Create**.
2. **Build → Authentication → Get started → Sign-in method → Google → Enable** → pick your support email → **Save**.
3. **Authentication → Settings → Authorized domains → Add domain** → `chernhaoee.github.io`.
4. **Build → Firestore Database → Create database** → pick a location close to you (e.g. `asia-southeast1`) → **Start in production mode** → **Create**.
5. **Firestore → Rules** → replace everything with the contents of [`firestore.rules`](firestore.rules) → **Publish**.
6. **Project settings (gear) → General → Your apps → Web (`</>`)** → nickname `web` → **Register app** (no hosting needed). Copy the `firebaseConfig` values.

### 2. Connect the app
Put those values into [`firebase-config.js`](firebase-config.js) (edit it on GitHub, or send them to Claude to commit).

### 3. Turn on GitHub Pages
Repo **Settings → Pages → Build and deployment → Source: Deploy from a branch → Branch: `main` / `(root)` → Save**. After ~1 minute the app is live at:

**https://chernhaoee.github.io/traveel/**

### 4. First run
1. Open the link, **Sign in with Google**, tap **Make me the Admin** (only works for the first person, so do this yourself first).
2. Tap **Choose trip data file** and pick `traveel-trip-data.json` (kept out of this repo on purpose, so the trip details aren't public).
3. **Trip tab → Invite people** → make a **Planner** or **Traveler** link → send it on WhatsApp. They sign in with Google and join with that role.
4. Everyone taps **This is me** on their name under *People (for splitting)*.

On phones: open the link in Safari/Chrome → **Share → Add to Home Screen** to use it like an app. It keeps working offline for anything already loaded.

## Notes
- Firebase web config values are not secrets; access is controlled by Google sign-in and the security rules.
- Ticket uploads are stored in Firestore (images are shrunk to ~1600px; PDFs up to 700 KB), so no paid Firebase Storage is needed.
- Exchange rate: the app can fetch the day's JPY → MYR rate automatically (ECB rate via frankfurter.app); you can still type in the Google/Wise rate.

## License
All rights reserved. This repo is public for viewing only. See [LICENSE](LICENSE).
