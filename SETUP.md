# Hosting Gritwise Legal Docs on gritwise.co
**One-time setup — ~20 minutes**

The goal: publish `privacy.html` and `terms.html` to Cloudflare Pages so they
are live at `https://gritwise.co/privacy` and `https://gritwise.co/terms`.

---

## Step 1 — Create the GitHub repository

1. Go to [github.com/new](https://github.com/new)
2. Owner: **Fabs-world**
3. Repository name: `gritwise-legal`
4. Set to **Public** (Cloudflare Pages free tier requires public repos, or you
   can connect a private repo if you're on a paid GitHub plan)
5. Leave everything else as default — do NOT initialize with a README
6. Click **Create repository**

---

## Step 2 — Push the legal files to GitHub

Open Terminal (on your Mac) and run these commands one at a time.
Replace the path if your project folder is in a different location.

```bash
# Navigate to the legal folder
cd ~/Documents/Claude/Overlanding_planning_app/Overlanding_trip_planning_app/legal

# Initialize a git repo
git init

# Add all files
git add .

# Make the first commit
git commit -m "Add privacy policy, terms of service, and redirects"

# Point to your new GitHub repo
git remote add origin https://github.com/Fabs-world/gritwise-legal.git

# Push
git branch -M main
git push -u origin main
```

After this, refresh your GitHub page — you should see `privacy.html`,
`terms.html`, and `_redirects` listed in the repo.

---

## Step 3 — Connect to Cloudflare Pages

1. Log in to your Cloudflare dashboard at [dash.cloudflare.com](https://dash.cloudflare.com)
2. In the left sidebar, click **Workers & Pages**
3. Click **Create** → **Pages** → **Connect to Git**
4. Authorize Cloudflare to access your GitHub account if prompted
5. Select the **Fabs-world/gritwise-legal** repository
6. Click **Begin setup**

On the build settings screen:
- **Project name:** `gritwise-legal`
- **Production branch:** `main`
- **Build command:** *(leave blank — this is a static site, no build needed)*
- **Build output directory:** *(leave blank)*

Click **Save and Deploy**. Cloudflare will deploy the site in about 30 seconds.

---

## Step 4 — Connect your gritwise.co domain

Once deployed, Cloudflare will give you a temporary URL like
`gritwise-legal.pages.dev`. Now connect your real domain:

1. In the Pages project dashboard, go to **Custom domains**
2. Click **Set up a custom domain**
3. Enter: `gritwise.co`
4. Click **Continue**

Because your domain is already registered through Cloudflare, the DNS records
will be added automatically. Click **Activate domain**.

It may take a minute or two to propagate. When it's done, your URLs will be:

- `https://gritwise.co/privacy` ✅
- `https://gritwise.co/terms` ✅

---

## Step 5 — Verify

Open a browser and visit both URLs to confirm they load correctly.
Then you're done — IF-17 is complete.

---

## Updating the documents later

If you ever need to update the privacy policy or terms (e.g., before adding
user accounts or cloud sync), edit the HTML files in this folder and run:

```bash
cd ~/Documents/Claude/Overlanding_planning_app/Overlanding_trip_planning_app/legal
git add .
git commit -m "Update privacy policy"
git push
```

Cloudflare Pages will automatically redeploy within about 60 seconds.
