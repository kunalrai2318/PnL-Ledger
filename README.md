# P&L Ledger — Synced Web App

A calendar-based trading journal: log daily P&L, trade count, a journal note,
and a chart screenshot. Shows win rate, profit factor, expectancy, and a
drawdown chart. Now syncs privately across every device via your own free
Firebase account — log in once on your phone and iPad and everything stays
in sync automatically.

## One-time setup: create your free Firebase backend (~15–20 min)

### 1. Create a Firebase project
1. Go to https://console.firebase.google.com and sign in with any Google account
2. Click **Add project**, name it anything (e.g. "pnl-ledger"), continue through the prompts (you can disable Google Analytics, it's not needed)
3. Wait for it to finish creating

### 2. Turn on Email/Password login
1. In the left sidebar, click **Build → Authentication**
2. Click **Get started**
3. Click **Email/Password**, toggle it **Enabled**, click **Save**

### 3. Turn on Firestore (the database)
1. In the left sidebar, click **Build → Firestore Database**
2. Click **Create database**
3. Choose any nearby location, then select **Start in production mode**, click **Create**
4. Once it's created, click the **Rules** tab and replace the contents with:
   ```
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /users/{userId}/{document=**} {
         allow read, write: if request.auth != null && request.auth.uid == userId;
       }
     }
   }
   ```
5. Click **Publish**

   This rule means: only a logged-in user can read or write their *own* data — nobody else's, and nothing works without logging in.

### 4. Register a Web App and get your config
1. Click the **gear icon** next to "Project Overview" (top left) → **Project settings**
2. Scroll to "Your apps", click the **</>** (web) icon
3. Give it a nickname (e.g. "ledger-web"), click **Register app** (skip the hosting step)
4. You'll see a code block with a `firebaseConfig` object like:
   ```js
   const firebaseConfig = {
     apiKey: "AIza...",
     authDomain: "pnl-ledger-xxxxx.firebaseapp.com",
     projectId: "pnl-ledger-xxxxx",
     storageBucket: "pnl-ledger-xxxxx.appspot.com",
     messagingSenderId: "...",
     appId: "..."
   };
   ```
5. Copy those 6 values

### 5. Paste your config into the app
1. Open `index.html` in a text editor (or edit it directly on GitHub with the pencil icon)
2. Find this block near the top of the `<script>` section:
   ```js
   const FIREBASE_CONFIG = {
     apiKey: "PASTE_ME",
     authDomain: "PASTE_ME",
     projectId: "PASTE_ME",
     storageBucket: "PASTE_ME",
     messagingSenderId: "PASTE_ME",
     appId: "PASTE_ME"
   };
   ```
3. Replace each `"PASTE_ME"` with your actual values from step 4
4. Save / commit the change

## 2. Upload to GitHub (if not already hosted)
See your repo → **Add file → Upload files** → select `index.html`, `manifest.json`,
`service-worker.js`, the icon files, and this README → **Commit changes**.
GitHub Pages will redeploy automatically in about a minute.

## 3. Create your account and log in on both devices
1. Open your GitHub Pages URL in Safari
2. Tap **"Create an account"**, enter an email + password (this can be anything — it's just your private login, doesn't need to be a real inbox you check)
3. On your other device, open the same URL and **log in** with the same email + password
4. Anything you log on one device appears on the other within a second or two, as long as both are online

If you already installed the app to your home screen before this update,
force-close it and reopen so it picks up the new version.

## Notes
- Your data lives in your own private Firestore database — Anthropic/Claude
  never sees it, and Firebase's free tier (Spark plan) covers personal use
  at no cost.
- The app works offline too: entries save locally first and sync up
  automatically once you're back online.
- Chart screenshots are compressed before upload to keep sync fast; very
  large or numerous photos will use more of Firebase's free storage quota
  over time, though normal use is nowhere close to the limit.
- Forgot your password? Firebase's free tier doesn't include a password
  reset flow out of the box in this app — if that happens, just create a
  new account. Ask me if you'd like a "forgot password" flow added.
