# NutriLens AI — Legal docs (GitHub Pages)

Static HTML pages for the **Privacy Policy** and **Terms & Conditions**, styled to match the brand and ready to deploy to GitHub Pages — same setup pattern as `mokshgiri/shieldvpn`.

## Final URLs (after the one-time setup below)

| Page | URL |
|---|---|
| Index | `https://mokshgiri.github.io/nutrilens-ai/` |
| Privacy Policy | `https://mokshgiri.github.io/nutrilens-ai/privacy-policy.html` |
| Terms & Conditions | `https://mokshgiri.github.io/nutrilens-ai/terms-conditions.html` |

These are the URLs to paste into Firebase Realtime Database under `/showConfigs/privacyPolicyUrl` and `/showConfigs/termsUrl` — the in-app **Settings → Privacy / Terms** rows already read from those keys via `RemoteConfigUtil`, so no app rebuild is needed once Firebase is updated.

## One-time setup

### 1. Create a new GitHub repo
Go to https://github.com/new

- **Repository name:** `nutrilens-ai`
- **Visibility:** Public (required for free GitHub Pages)
- **Initialize with README:** No

Click **Create repository**.

### 2. Push these files to that repo

From the **`legal/`** folder of this Android project:

```bash
cd legal
git init
git add index.html privacy-policy.html terms-conditions.html README.md
git commit -m "Initial NutriLens AI legal docs"
git branch -M main
git remote add origin https://github.com/mokshgiri/nutrilens-ai.git
git push -u origin main
```

### 3. Enable GitHub Pages

On the new repo's GitHub page:

1. Click **Settings** (top tab)
2. Scroll to **Pages** in the left sidebar
3. Under **Build and deployment → Source**, choose **Deploy from a branch**
4. Branch: **`main`** · Folder: **`/ (root)`**
5. Click **Save**

Wait 1–2 minutes for the first deploy, then verify the three URLs above load.

### 4. Plug the URLs into Firebase

In the Firebase Console for the NutriLens AI project:

1. Open **Realtime Database** → `/showConfigs`
2. Set / update:
   - `privacyPolicyUrl` → `https://mokshgiri.github.io/nutrilens-ai/privacy-policy.html`
   - `termsUrl` → `https://mokshgiri.github.io/nutrilens-ai/terms-conditions.html`

The app picks the new URLs up the next time it launches and the remote-config fetch succeeds. No new APK build required.

### 5. Use the URLs on Play Store too

Play Console → **App content → Privacy policy** → paste the privacy URL.

---

## Editing the docs later

Edit the HTML in this folder, push to the repo, and GitHub Pages auto-redeploys in ~30 seconds. Bump the **"Last updated"** date at the top of the page whenever you ship a meaningful change.

---

## What's in here

- **`index.html`** — landing page with links to both docs (gradient logo, dark theme, brand green)
- **`privacy-policy.html`** — privacy policy reflecting the app's actual data flow:
  - Local-only Room storage of profile, meals, weight, water, chat
  - OpenAI for vision + chat + plan generation (with the API "no training" note)
  - Firebase Realtime Database for read-only remote config
  - Google AdMob with Advertising ID opt-out instructions
  - No third-party analytics or tracking SDKs
- **`terms-conditions.html`** — terms with explicit AI accuracy disclaimer, full medical disclaimer, acceptable use, third-party services, IP, liability cap, governing law (India)
- **Style** — matches the `mokshgiri/shieldvpn` legal pages: dark `#080C14` background, brand-green headings (`#22C55E`), teal subheadings (`#0EA5A4`), green-bordered highlight callouts

## Important

These docs reflect the app's data flow as of the date at the top of each page. If you add a new third-party service (analytics, crash reporting, social login, server-side sync, etc.), **update the privacy policy** before shipping that build.
