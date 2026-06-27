# Arogya — Arogyavan

A premium mind–body–soul wellness PWA, rooted in Indian dietary and spiritual tradition. Pick a goal (Urja / Shanti / Pachan / Santulan), follow a daily 80/10/10 path, and watch a living lotus bloom as you log meals, movement, mind and soul.

## Files
| File | Purpose |
|---|---|
| `index.html` | The entire app (single file, vanilla JS) |
| `manifest.json` | PWA manifest — name, colours, icons |
| `sw.js` | Service worker — offline app shell |
| `icon.svg` / `icon-192.png` / `icon-512.png` / `icon-maskable.png` | App icons |

## Deploy to GitHub Pages (fastest)
1. Create a new repo, e.g. `arogyavan`.
2. Upload all files in this folder to the repo root.
3. Repo **Settings → Pages → Source: `main` / root → Save**.
4. Live at `https://<username>.github.io/arogyavan/` in ~1 minute.

## Deploy to Vercel
1. Push the folder to GitHub.
2. On vercel.com → **Add New → Project → import the repo**.
3. Framework preset **Other**, root directory `/`, no build command. Deploy.

## Turn on login + email (Supabase)
The app runs without this (a **Continue without an account** button appears). To enable real accounts:
1. Create a project at supabase.com.
2. In `index.html`, find the **Supabase** block near the top of the script and fill:
   ```js
   const SUPABASE_URL="https://xxxx.supabase.co";
   const SUPABASE_ANON_KEY="your-anon-public-key";
   ```
3. Supabase → **Authentication → Providers → Email** (enable). For confirmation/magic-link emails, set **Authentication → Email → SMTP** (e.g. a Gmail App Password).
4. Add your deployed URL under **Authentication → URL Configuration → Site URL / Redirects**.

Email/password sign-up, sign-in, and magic-link are all wired. Sign-out lives in the **Me** tab.

## Turn on the AI (Haiku recipes + Sonnet photo scan)
The app uses an Anthropic proxy so your API key never ships to the browser.
1. Deploy a Supabase **Edge Function** that forwards requests to `https://api.anthropic.com/v1/messages` with your `ANTHROPIC_API_KEY` from server-side env.
2. In `index.html`, set:
   ```js
   const PROXY_URL="https://<project>.functions.supabase.co/anthropic";
   ```
Until then, recipes and photo scans use a graceful offline demo.

## Add your dishes
Replace or extend the `DISHES` array in `index.html`. Author dishes with the **Dish Builder** tool and paste its export, or send a `name | meals | ingredients` list. Atomic flags drive all diet eligibility (see `RULES.md`).

## App icons
`icon-*.png` are placeholders. Replace with your final logo at 192×192, 512×512, and a 512×512 **maskable** version (keep art inside the centre 80% safe zone).

## Android (Play Store) later
Wrap the deployed PWA as a TWA with Bubblewrap or PWABuilder once it's live and installable.

---
*DailyLabs · built one surgical patch at a time.*
