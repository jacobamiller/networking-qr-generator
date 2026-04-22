# Networking QR Code Generator

A mobile-first web app that generates vCard QR codes for networking events. When someone scans your QR code, your contact info is added to their address book with a note about where and when you met.

## How It Works

1. **Set up your profile** (once) -- your name, email, phone, company, and title.
2. **Enter event details** -- date, event name, and any notes.
3. **Generate a QR code** -- hand your phone to someone and let them scan it.
4. **Their phone saves your contact** with a note like: "Met Jane Smith at TechCrunch Disrupt on April 30, 2026. We discussed AI tooling for startups."

All data is stored locally in your browser (localStorage). Nothing is sent to any server.

## Local Development

No build step required. Open the file directly in a browser:

```bash
# Option 1: Open the file directly
open index.html

# Option 2: Use any local server (optional, for a more production-like experience)
npx serve .
# or
python3 -m http.server 8000
```

## Deploy to GitHub Pages

### 1. Create a GitHub repository

Go to [github.com/new](https://github.com/new) and create a new **private** repository named `networking-qr-generator` (or any name you prefer).

### 2. Push the code

```bash
cd /path/to/this/folder
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/networking-qr-generator.git
git push -u origin main
```

### 3. Enable GitHub Pages

1. Go to your repository on GitHub.
2. Navigate to **Settings > Pages**.
3. Under **Source**, select **Deploy from a branch**.
4. Set branch to `main` and folder to `/ (root)`.
5. Click **Save**.

### 4. Access your app

After a minute or two, your app will be live at:

```
https://YOUR_USERNAME.github.io/networking-qr-generator/
```

## Tech Stack

- Plain HTML, CSS, and JavaScript (no build step, no framework)
- [qrcode.js](https://github.com/davidshimjs/qrcodejs) via cdnjs CDN for QR code generation
- vCard 3.0 strings generated directly (no library needed)
- localStorage for all data persistence

## Features

- Mobile-first responsive design
- One-tap QR code generation
- vCard encoding that works with iOS and Android native contacts apps
- Event history with reload and delete
- QR code persists across page reloads
- Stale QR code warning (12+ hours old)
- Profile data saved once, reused for every event
