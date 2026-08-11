# Mess Hisab

A web app I built to manage shared expenses for my 11-member mess (rent, meals, bazar rotation, and misc expenses) — replacing our old messy WhatsApp/Excel tracking with a single shared dashboard everyone can use from their phone.

## Why I built this

Our mess had 9-11 people splitting rent, meal costs, and grocery duty every month, and keeping track of who paid what, whose turn it was to do bazar, and how many meals everyone ate was getting messy across WhatsApp texts and spreadsheets. I built this to centralize everything in one place, with a clean UI in Bangla/English, live shared data, and an audit log so nothing gets disputed.

## Features

- **Rent tracking** — per-member rent amount, paid/unpaid status, and admin permissions for who can mark rent as paid
- **Meal entry** — daily meal check-in per member (breakfast/dinner), with a separate collapsible guest-meal add-on
- **Bazar rotation** — auto-generated shopping duty cycle across members, with manual override
- **Expense tracking** — miscellaneous mess expenses logged and split
- **Monthly reports** — per-member cost breakdown for the month
- **Audit log** — every change (rent status, meal entry, member edits) is logged with who/what/when
- **Bangla / English toggle** — full UI translation
- **Real-time shared data** — everyone sees the same live data instantly, backed by Firebase Firestore

## Tech stack

- Single-file HTML/CSS/JS (no build step, no framework — easy to host anywhere)
- Firebase Firestore for shared real-time data storage
- Deployed on Vercel with auto-deploy on every push to `main`

## Setup (for running your own instance)

1. Create a free Firebase project at https://console.firebase.google.com
2. Enable **Firestore Database** (start in production mode, pick a region e.g. `asia-south1`)
3. In Firestore Rules, use:
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
4. Project settings > General > Your apps > Web app (`</>`) > copy the `firebaseConfig` object
5. Paste it into `index.html`, inside the `firebaseConfig = {...}` block near the top of the `<script type="module">` section
6. Commit and push — every push to `main` auto-redeploys on Vercel

## Deploy

**Vercel (recommended)**
1. Push this repo to GitHub
2. vercel.com > New Project > Import this repo > Deploy (no build settings needed, it's static HTML)
3. Every `git push` to `main` auto-redeploys

## Notes

- No login system — anyone with the link can use it, which works fine for a small trusted mess group.
- Rent-admin permissions inside the app control who's allowed to mark rent as paid/unpaid.
- Firestore's free tier is more than enough for this scale of usage.

---

Built and maintained by [Fayed](https://github.com/Fayed038).
