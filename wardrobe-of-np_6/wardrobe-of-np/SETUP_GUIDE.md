# Wardrobe of NP — Setup Guide
## Google Drive + Netlify Deployment

Total time: ~20 minutes. No coding needed.

---

## STEP 1 — Deploy to Netlify (5 min)

1. Go to **[netlify.com](https://netlify.com)** and sign up (free)
2. From your dashboard, click **"Add new site" → "Deploy manually"**
3. Drag the entire **`wardrobe-of-np`** folder onto the upload area
4. Netlify gives you a URL like `https://random-name-123.netlify.app`
5. Optional: click **"Site settings" → "Change site name"** to get something like `wardrobe-of-np.netlify.app`

**Write down your Netlify URL — you'll need it in Step 2.**

---

## STEP 2 — Create Google Cloud Project (10 min)

### 2a. Create a project
1. Go to **[console.cloud.google.com](https://console.cloud.google.com)**
2. Sign in with your Google account
3. Click the project dropdown at the top → **"New Project"**
4. Name it `Wardrobe of NP` → click **Create**

### 2b. Enable the Google Drive API
1. In the left menu go to **APIs & Services → Library**
2. Search for **"Google Drive API"**
3. Click it → click **Enable**

### 2c. Configure the OAuth consent screen
1. Go to **APIs & Services → OAuth consent screen**
2. Choose **External** → click **Create**
3. Fill in:
   - App name: `Wardrobe of NP`
   - User support email: your email
   - Developer contact email: your email
4. Click **Save and Continue** through all steps (you can skip optional fields)
5. On the **Test users** step, click **"+ Add Users"** and add your own Gmail address
6. Click **Save**

### 2d. Create OAuth credentials
1. Go to **APIs & Services → Credentials**
2. Click **"+ Create Credentials" → "OAuth 2.0 Client ID"**
3. Application type: **Web application**
4. Name: `Wardrobe of NP Web`
5. Under **Authorised JavaScript origins**, click **Add URI** and add:
   - `https://your-site-name.netlify.app` ← your Netlify URL from Step 1
   - `http://localhost` (optional, for local testing)
6. Click **Create**
7. A popup shows your **Client ID** — it looks like:
   `123456789-abcdefghijklmnop.apps.googleusercontent.com`
   **Copy this — you need it for Step 3.**

### 2e. Create an API Key
1. Go to **APIs & Services → Credentials**
2. Click **"+ Create Credentials" → "API Key"**
3. Copy the API key (looks like `AIzaSyABC123...`)
4. Click **"Restrict key"** → under API restrictions choose **"Restrict key"** → select **Google Drive API** → Save

---

## STEP 3 — Add your credentials to the app (2 min)

1. Open **`index.html`** in a text editor (Notepad, TextEdit, VS Code etc.)
2. Find these lines near the top of the `<script>` section:
   ```
   CLIENT_ID: 'YOUR_GOOGLE_CLIENT_ID.apps.googleusercontent.com',
   API_KEY:   'YOUR_GOOGLE_API_KEY',
   ```
3. Replace `YOUR_GOOGLE_CLIENT_ID.apps.googleusercontent.com` with your Client ID from Step 2d
4. Replace `YOUR_GOOGLE_API_KEY` with your API Key from Step 2e
5. Save the file

---

## STEP 4 — Redeploy to Netlify (1 min)

1. Go back to your Netlify site dashboard
2. Click **"Deploys" → "Deploy manually"**
3. Drag the updated `wardrobe-of-np` folder again
4. Wait ~30 seconds for it to deploy

---

## STEP 5 — Test it

1. Open your Netlify URL in any browser
2. You should see the sign-in screen with "Sign in with Google"
3. Click it — sign in with your Google account
4. The app loads and auto-saves to Google Drive
5. Open the same URL on your phone — sign in again — your data appears!

---

## How data is stored

- All your data (occasions, looks, closet items) is stored as a single JSON file called `wardrobe-of-np-data.json` in a **private, hidden "app data" folder** in your Google Drive
- This folder is only accessible by the Wardrobe of NP app — no other app or person can see it
- Images you upload are stored as base64 data inside the same file
- Auto-saves every 1.5 seconds after any change
- A "Saved to Drive ✓" indicator appears at the bottom-right of the screen

---

## Troubleshooting

**"Sign-in failed"** — Make sure your Netlify URL is added to Authorised JavaScript origins in Google Cloud (Step 2d), and that you've added yourself as a test user (Step 2c).

**"Access blocked: This app's request is invalid"** — The Client ID doesn't match the domain. Double-check the URL in Authorised JavaScript origins matches your exact Netlify URL.

**Data not loading** — Try signing out and signing back in. Check the browser console for errors.

**Images making the file very large** — This is normal. Each uploaded image is stored as base64 text (~1.3x the image file size). Keep individual images under 2MB for best performance.

---

## Your Netlify URL
Write it here after Step 1: ___________________________
