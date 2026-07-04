# Stub — clean restart

This is a simplified rebuild: same app (scan a receipt → free on-device OCR →
save to a local library → search past receipts), but with the service worker
removed and a local-testing step added, so you can catch problems before
ever pushing to GitHub.

## Step 1 — Test it locally first (do this before anything else)

From inside this folder:
```
python3 -m http.server 8000
```
Then open **http://localhost:8000** in Safari or Chrome on your Mac.

Try the whole flow right there:
- Tap "Scan a receipt"
- Tap "Take or upload photo" — on your Mac this opens a normal file picker,
  so pick any receipt photo you have, or even a screenshot of one
- Confirm it reads it and shows itemized results
- Back out and confirm it shows up in "My receipts"
- Try the search bar

If anything's broken, you'll see it immediately in this local test — no
waiting on a deploy. Press `Ctrl+C` in Terminal to stop the local server
when you're done testing.

## Step 2 — Only once it works locally, put it on GitHub

**Delete or ignore your old repos** — start clean:
1. github.com → **+** → **New repository** → name it something new and
   final, e.g. `stub-app` → leave it empty → **Create repository**.

2. From this folder:
   ```
   git init
   git add .
   git commit -m "Clean rebuild"
   git branch -M main
   git remote add origin https://github.com/YOUR-USERNAME/stub-app.git
   git push -u origin main
   ```
   (use your actual GitHub username — the one you confirmed was
   `apadilla7771-cloud` — and whatever repo name you just created)

## Step 3 — Turn on GitHub Pages

1. On the repo page: **Settings → Pages**
2. Source: **Deploy from a branch** → Branch: `main`, folder `/ (root)` → **Save**
3. Wait a minute, refresh, copy the URL it gives you

## Step 4 — Add to your home screen

- **iPhone:** open the URL in **Safari** → Share icon → **Add to Home Screen**
- **Android:** open the URL in **Chrome** → ⋮ → **Add to Home screen**

## If something breaks this time

Because there's no service worker anymore, there's no caching layer to
second-guess — if the live site is broken, it's broken for a real reason,
and a normal refresh will show you the current deployed state accurately.
That should make debugging much more straightforward going forward.
