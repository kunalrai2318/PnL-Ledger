# P&L Ledger — Installable Web App

A calendar-based trading journal: log daily P&L and trade count, see win rate,
profit factor, expectancy, and a drawdown chart, set monthly goals, and jot
journal notes per day. All data is stored locally on your device (nothing is
sent to a server).

## Files
- `index.html` — the app
- `manifest.json` — makes it installable
- `service-worker.js` — enables offline use
- `icon-192.png`, `icon-512.png`, `apple-touch-icon.png` — app icons

## 1. Host it somewhere (required — iOS needs https to install a PWA)

Pick whichever is easiest for you:

**Netlify Drop (fastest, no account needed)**
1. Go to https://app.netlify.com/drop on your computer
2. Drag this whole folder onto the page
3. You'll get a live `https://…netlify.app` URL instantly

**GitHub Pages (free, permanent)**
1. Create a new GitHub repo, upload these files
2. Repo Settings → Pages → set source to the main branch
3. Your app will be live at `https://yourusername.github.io/reponame/`

**Vercel**
1. https://vercel.com/new → drag and drop the folder or connect a repo

## 2. Install on your iPad
1. Open the hosted URL in **Safari** (must be Safari, not Chrome — Chrome on iOS can't install PWAs)
2. Tap the **Share** icon (square with an arrow) in the toolbar
3. Scroll down and tap **"Add to Home Screen"**
4. Tap **Add**

You'll now have a P&L Ledger icon on your home screen that opens full-screen,
with no browser bar, and works offline after the first load.

## Notes
- Data is stored in the browser's local storage, scoped to that installed app.
  It stays on this iPad; it won't sync to your phone or a Mac automatically.
- If you ever want to reset all data, you'd need to delete and reinstall the
  app (there's no in-app "reset" button yet — ask me to add one if useful).
