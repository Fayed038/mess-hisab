# Mess Hisab

11-member mess expense tracker (rent, meals, bazar, misc expenses) — single-file HTML app backed by Firebase Firestore.

## Setup

1. Create a free Firebase project at https://console.firebase.google.com
2. Enable **Firestore Database** (start in production mode, pick a region e.g. asia-south1)
3. In Firestore Rules, use (simple, no login, mess is trusted small group):
   ```
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /mess/{doc} {
         allow read, write: if true;
       }
     }
   }
   ```
4. Project settings > General > Your apps > Web app (</>) > copy the `firebaseConfig` object
5. Paste it into `index.html`, inside the `firebaseConfig = {...}` block near the top of the `<script type="module">` section
6. Commit and push — if deployed via Vercel/Netlify/GitHub Pages, it auto-updates on every push to `main`

## Deploy (auto-update on push)

**Option A — Vercel (recommended, easiest)**
1. Push this repo to GitHub
2. Go to vercel.com > New Project > Import this repo > Deploy (no build settings needed, static HTML)
3. Every `git push` to main auto-redeploys

**Option B — GitHub Pages**
1. Push this repo to GitHub
2. Repo Settings > Pages > Source: Deploy from branch `main` / root
3. Every push auto-updates the live page in ~1 min

## Notes
- No login system — anyone with the link can edit. Fine for a trusted 9–11 person mess group.
- `rentAdmins` in-app setting still controls who can mark rent paid/unpaid.
- Firestore free tier (Spark plan) is far more than enough for this usage.
