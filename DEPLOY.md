# Mata Viva Platform — Deployment Guide

This is a single-file web app. No build step, no Node.js, no framework.
Follow the two steps below and your co-founders will have a live shared URL
in about 15 minutes.

---

## STEP 1 — Set up Supabase (free, ~5 min)

Supabase is the free backend that keeps all three founders in sync.
Without it the app still works, but each person sees their own local data.

1. Go to https://supabase.com and click **Start your project** (free tier, no credit card).
2. Create a new project. Name it anything (e.g. `mataviva`). Choose the **South America (São Paulo)** region. Set a database password and save it somewhere.
3. Wait ~2 minutes for the project to spin up.
4. In the left sidebar go to **Table Editor → New table**.
   - Name: `mataviva_state`
   - Uncheck "Enable Row Level Security" for now (you can add it later)
   - Add these columns:
     | Name  | Type   | Default | Primary key |
     |-------|--------|---------|-------------|
     | id    | int8   | —       | ✅ Yes      |
     | key   | text   | —       | No          |
     | value | text   | —       | No          |
   - Click **Save**.
5. In the Table Editor, click **Insert row** and add:
   - id: `1`
   - key: `state`
   - value: `{}`
   - Click **Save**.
6. In the left sidebar go to **Settings → API**.
   - Copy the **Project URL** (looks like `https://xxxxxxxxxxxx.supabase.co`)
   - Copy the **anon / public** key (long string under "Project API keys")

7. Open `index.html` in any text editor and replace these two lines near the top:
   ```
   const SUPABASE_URL = 'YOUR_SUPABASE_URL';
   const SUPABASE_KEY = 'YOUR_SUPABASE_ANON_KEY';
   ```
   with your actual values, e.g.:
   ```
   const SUPABASE_URL = 'https://abcdefgh.supabase.co';
   const SUPABASE_KEY = 'eyJhbGciOiJIUzI1NiIs...';
   ```

---

## STEP 2 — Deploy to GitHub Pages (free, ~10 min)

1. Go to https://github.com and sign in (or create a free account).
2. Click **New repository**.
   - Name: `mataviva-platform` (or anything you like)
   - Set to **Public** (required for free GitHub Pages)
   - Click **Create repository**
3. On the next screen click **uploading an existing file**.
4. Drag and drop `index.html` into the upload area. Click **Commit changes**.
5. Go to **Settings → Pages** (left sidebar).
6. Under **Source**, select **Deploy from a branch**.
7. Under **Branch**, select `main` and `/ (root)`. Click **Save**.
8. Wait ~60 seconds, then refresh the page. You'll see:

   > Your site is live at `https://YOUR-USERNAME.github.io/mataviva-platform/`

9. Share that URL with your co-founders. That's it.

---

## Sharing with co-founders

Send them the GitHub Pages URL. They open it in any browser — no install,
no account needed. They select their founder identity from the dropdown
in the top right and start editing. All changes sync via Supabase within
a second or two.

---

## Optional: make the repo private

GitHub Pages requires a public repo on the free plan. If you want the
code private, upgrade to GitHub Pro ($4/mo) or use **Netlify** instead:

1. Go to https://netlify.com → **Add new site → Deploy manually**
2. Drag the `index.html` file into the deploy zone
3. Netlify gives you a URL instantly (e.g. `https://random-name.netlify.app`)
4. You can rename it under **Site settings → Site name**

Netlify's free tier supports private deployments with no repo required.

---

## Updating the platform later

**GitHub Pages:** go to your repo, click `index.html`, click the pencil
icon to edit, make changes, commit. The site updates in ~30 seconds.

**Netlify:** drag the updated `index.html` into the Netlify deploy zone again.

---

## Troubleshooting

| Problem | Fix |
|---------|-----|
| "synced" shows but data doesn't persist | Check SUPABASE_URL and SUPABASE_KEY in index.html |
| Co-founder sees different data | Make sure all three are using the same deployed URL, not a local file |
| Yellow setup banner still showing | You haven't replaced the placeholder values in index.html yet |
| Supabase PATCH returns 404 | Check that row id=1 exists in the mataviva_state table |
