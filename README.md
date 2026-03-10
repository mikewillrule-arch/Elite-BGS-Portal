Demo Link : https://nonskeletal-davin-nonzonated.ngrok-free.dev/

What This Program Actually Is — For the Cautious Commander

  Fair question, and smart instinct. Here's exactly what you're running and why it's safe.

  ---
  What kind of file is this?

  This is a Node.js web application — the same technology that runs Discord, Slack, GitHub, and thousands of other tools you already use every day. It is not an .exe compiled from unknown source code. It is
  plain, human-readable JavaScript text files that Node.js interprets line by line at runtime.

  You can open server.js, eddn-listener.js, or any other file in Notepad right now and read every single line of what it does before running it. Nothing is hidden, obfuscated, or compiled into a binary blob.
  It is source code all the way down.

  ---
  What does it actually do on your PC?

  Here is the complete list of everything this program does to your computer:

  1. Opens one port on localhost (port 3000) — this is a local web server, identical in concept to running a web page on your own machine. It is not exposed to the internet unless you specifically set up Ngrok
   yourself.
  2. Connects outbound to EDDN (eddn.edcd.io:9500) — this is the official Elite Dangerous Data Network, the same data source used by Inara, EDDB, and EliteBGS.app. It receives live BGS data from the game.
  3. Makes HTTPS API calls to services you configured — Gemini, Groq, EliteBGS.app, Inara — to fetch faction data and run AI analysis. These are outbound calls only, same as your browser calling a website.
  4. Writes files to its own data/ folder — stores squadron config, user accounts, and BGS history inside the project folder. It does not touch anywhere else on your system.
  5. That's it. No registry edits. No startup entries. No background processes after you close it. No access to your Elite Dangerous installation, your journal files, or anything outside its own folder.

  ---
  What it does NOT do

  - Does not read your files, documents, or Elite journal files
  - Does not install anything system-wide
  - Does not run in the background after you close the terminal window
  - Does not modify your registry
  - Does not make any outbound connections other than the three listed above
  - Does not have any mechanism to receive incoming connections from the internet (unless you manually set up Ngrok)
  - Does not collect or transmit your personal data anywhere

  ---
  Why does it need to run locally at all?

  Because it's a web server. The dashboard your browser opens at http://localhost:3000 has to be served by something. That something is node server.js. It's the same reason you have to run a Minecraft server
  on a machine to host a Minecraft server — there's no magic cloud doing it for free. The upside is that your data stays on your machine, under your control, forever.

  ---
  The dependencies (node_modules)

  When you run npm install, it downloads about 30 small packages from the official npm registry — things like express (the most popular Node.js web framework on the planet, used by millions of projects) and
  zeromq (a networking library). These are all open source, publicly audited packages. You can check every one of them at npmjs.com.

  ---
  Still not sure? Scan it first.

  Totally reasonable. Here's how:

  VirusTotal (easiest — no install needed):
  1. Go to https://www.virustotal.com
  2. Click Choose file
  3. Zip up the project folder and upload it, or upload individual files like server.js and eddn-listener.js
  4. 70+ antivirus engines will scan it in about 30 seconds
  5. Read the results

  Your local antivirus:
  - Right-click the project folder → Scan with [Windows Defender / Malwarebytes / whatever you use]
  - JavaScript files are text — your AV will have no trouble reading them

  Read the source yourself:
  - Open server.js in Notepad or VS Code
  - Ctrl+F for words like exec, spawn, writeFile to see exactly what system calls it makes
  - Everything is labeled with comments explaining what each section does



  This is a text-based web application written in one of the most common, most scrutinized programming languages on earth. It has no installer, no compiled binary, no persistence mechanism, and no access to
  anything outside its own folder. It runs when you tell it to run and stops when you close the window.

  If you've ever run a Minecraft server, a Discord bot, or any other local tool your squadron uses — this is the same category of thing.


# Elite BGS Analyzer — Squadron Intelligence Dashboard

<img width="1891" height="932" alt="image" src="https://github.com/user-attachments/assets/0587e759-6f3c-4f2f-b46c-5b89e6000101" />


A real-time Background Simulation (BGS) tracking and intelligence dashboard for Elite Dangerous squadron commanders. Built for squadrons who take the BGS seriously — live EDDN data, AI-powered briefings, tick detection, war tracking, rival monitoring, and a full squadron command interface, all in a single self-hosted web app.

---

## Why Use This Over Other Tools?

Most BGS tools (EDDB, Inara, EliteBGS.app) give you raw data tables. This gives you **command intelligence**.

| Feature | Other Tools | Elite BGS Analyzer |
|---|---|---|
| Live EDDN data (no refresh needed) |  |  Real-time ZeroMQ feed |
| AI executive briefings |  |  Gemini / Groq / Mistral AI |
| BGS tick auto-detection |  |  EDDN + tick.edcd.io |
| Post-tick change monitoring |  |  Auto-polls + AI diff report |
| War table with conflict tracking |  |  Built-in |
| Rival faction monitor |  |  Real-time influence tracker |
| Squadron member accounts |  |  Login, ranks, messaging |
| Per-user color themes |  |  Saved to user profile |
| CMDR activity tracking |  |  Dev dashboard + commendations |
| Works on your LAN or internet |  |  Ngrok tunnel included |
| Open source, self-hosted |  |  Your data, your server |

If your squadron has a dedicated BGS officer or wants to coordinate operations across multiple commanders, this is the tool.

---

## Features

### Live BGS Intelligence
- **Real-time EDDN feed** — listens to the Elite Dangerous Data Network via ZeroMQ. Every FSD jump and location event from every player in the game flows through. Your squadron's faction influence updates the moment someone submits a journal entry.
- **BGS Tick Detection** — detects the daily BGS tick using two parallel methods: EDDN influence change detection (threshold-based, watches all factions) and a live WebSocket feed from `tick.edcd.io`. Once the tick fires, post-tick monitoring begins automatically.
- **Post-Tick Monitoring** — after the tick, the system takes a baseline snapshot of all your watched systems and polls for changes every 20 minutes for 1 hour. When changes are detected, an AI executive brief is automatically generated and pushed to all connected clients.
- **Tick Countdown** — live countdown to the next 15:50 UTC BGS tick displayed in the header, format `Xh MMm SSs`.

### AI-Powered Analysis
- **Executive Briefings** — ask the AI for a full squadron operations brief. The AI knows your faction, current influence levels, active states, conflicts, and recent changes.
- **Strategy Suggestions** — request optimized BGS action plans based on current system states.
- **Journal Analysis** — paste in your Elite Dangerous journal events and get a BGS contribution breakdown.
- **AI Fallback Chain** — Gemini → Groq (LLaMA 3.3 70B) → OpenRouter → Mistral. If your primary AI hits its daily quota, the system falls over to the next provider automatically. All providers have generous free tiers.

### Squadron Command Center
- **War Table** — track all active conflicts your faction is in. See combat bond counts, war states, and opposing factions.
- **Rival Faction Monitor** — set a rival faction and track their influence across all their systems in real time. Get AI analysis of their trajectory.
- **System Deep Dive** — click any system for a full breakdown: all factions, influence history, active/pending states, last seen timestamp.
- **Galactic Map Annotations** — mark key systems on your sector map with custom labels and colors.

### Squadron Social Features
- **User Accounts** — squadron members register with a CMDR name and password. Leadership has an admin key, members have their own login.
- **Rank System** — assign ranks to members (Recruit → Wing Commander, etc.).
- **Internal Messaging** — Leadership can send announcements and direct messages to registered members.
- **Activity Tracking** — see which CMDRs have submitted the most journal data, who's been most active, and commendation counts.
- **Per-User Color Themes** — each user can pick their own color scheme (Cyan, Amber, Red, Purple, White) or build a fully custom hex theme. Saved to their profile.

### First-Boot Setup Wizard
- On first launch, a setup wizard walks the new squadron commander through:
  - Setting their squadron name (as it appears on Inara)
  - Choosing brand colors and initials badge
  - Setting the leadership password and dev/log password
  - Entering API keys for Gemini, Groq, OpenRouter, Mistral, and Inara
- All configuration is saved to `data/squadron_config.json`. The `.env` file is written automatically. No manual file editing required.

### CLI Companion (`bgs-analyzer.js`)
- A terminal-based BGS analysis tool with slash commands:
  - `/watch <system>` — add a system to post-tick monitoring
  - `/unwatch <system>` — remove a system
  - `/tick` — show tick status and countdown
  - `/squadron` — fetch squadron data from Inara
  - `/analyze` — run AI analysis from the terminal
- Set `WATCH_SYSTEMS=Sol,Deciat` in `.env` for auto-monitoring on launch.

---

## Requirements

- **Node.js** v18 or higher — [nodejs.org](https://nodejs.org)
- **npm** — included with Node.js
- **At least one AI API key** — all free tier, links below
- **Ngrok** (optional) — only needed if you want remote access outside your home network

---

## Installation

### Step 1 — Download

Clone the repository or download and extract the ZIP:

```bash
git clone https://github.com/YOUR_USERNAME/elite-bgs-analyzer.git
cd elite-bgs-analyzer
```

### Step 2 — Install Dependencies

```bash
npm install
```

This installs Express, ZeroMQ, ws, dotenv, and all other required packages. It takes about 30 seconds.

### Step 3 — Start the Server

**Windows:**
```
Double-click start.bat
```

**Mac / Linux:**
```bash
node server.js
```

### Step 4 — First-Boot Setup Wizard

Open your browser to `http://localhost:3000`

The setup wizard will appear automatically on first launch. It will ask you for:

1. **Squadron Name** — your squadron's name as it appears on Inara (e.g. `The Pilots Federation`)
2. **Initials** — 2–3 letter badge shown in the header (e.g. `PF`)
3. **Brand Colors** — primary, accent, and highlight hex colors for your dashboard
4. **Leadership Password** — this is the admin key used to unlock leadership features. Minimum 6 characters. Write it down.
5. **Dev/Log Password** — used to access the raw activity log and dev dashboard. Minimum 6 characters.
6. **API Keys** — enter at least one AI key (Gemini is recommended as the primary). All others are fallbacks and optional but recommended.

Click **COMPLETE SETUP** and the dashboard will load with your squadron's branding.

---

## Getting Your Free API Keys

All AI providers below have a free tier that is sufficient for daily BGS analysis.

### Gemini (Primary AI) — Free
1. Go to [aistudio.google.com](https://aistudio.google.com)
2. Sign in with a Google account
3. Click **Get API Key** → **Create API key**
4. Copy the key — it starts with `AIza...`

### Groq (Fallback 1) — Free
1. Go to [console.groq.com](https://console.groq.com)
2. Create a free account
3. Go to **API Keys** → **Create API Key**
4. Copy the key — it starts with `gsk_...`

### OpenRouter (Fallback 2) — Free tier available
1. Go to [openrouter.ai/keys](https://openrouter.ai/keys)
2. Create a free account
3. Click **Create Key**
4. Copy the key — it starts with `sk-or-v1-...`

### Mistral (Fallback 3) — Free tier available
1. Go to [console.mistral.ai/api-keys](https://console.mistral.ai/api-keys)
2. Create a free account
3. Click **Create new key**
4. Copy the key

### Inara (Optional — Squadron Data)
1. Go to [inara.cz/elite/settings-api](https://inara.cz/elite/settings-api/)
2. Log in with your Inara account
3. Register your application (name it anything, e.g. `BGS Dashboard`)
4. Copy the API key shown

---

## Remote Access with Ngrok

By default the dashboard runs on `http://localhost:3000` — only accessible on your local machine. If you want squadron members to connect from outside your home network, you need Ngrok.

### What is Ngrok?

Ngrok creates a secure tunnel from the internet to your local server. You get a public URL (like `https://abc123.ngrok-free.app`) that anyone can open in their browser and access your running dashboard.

### Free vs Paid Ngrok

| | Free Plan | Paid Plan (~$10/mo) |
|---|---|---|
| URL | Random, changes every restart | Permanent custom domain |
| Sessions | 1 at a time | Multiple |
| Bandwidth | Limited but sufficient | Higher limits |
| Auth | Requires one-time agent setup | Same |

**For most squadrons, the free plan is fine.** Your URL changes when you restart Ngrok, but you can just paste the new URL in your Discord each time. If you want a permanent link your members can bookmark, upgrade to the Starter plan and follow the custom domain steps below.

---

### Setting Up Ngrok — Step by Step

#### 1. Create a Free Ngrok Account

Go to [ngrok.com](https://ngrok.com) and sign up. It's free and only takes a minute.

#### 2. Download Ngrok

- **Windows**: Download the `.zip` from your Ngrok dashboard → [dashboard.ngrok.com/get-started/setup](https://dashboard.ngrok.com/get-started/setup)
  - Extract `ngrok.exe` to a folder you'll remember (e.g. `C:\ngrok\`)
- **Mac**: `brew install ngrok/ngrok/ngrok`
- **Linux**: `snap install ngrok` or download the binary

#### 3. Authenticate Ngrok

In your Ngrok dashboard, go to **Your Authtoken** and copy it. Then run:

```bash
ngrok config add-authtoken YOUR_AUTHTOKEN_HERE
```

You only need to do this once per machine.

#### 4. Start Your Dashboard

First, make sure your dashboard server is running:

```bash
node server.js
```
(or double-click `start.bat` on Windows)

#### 5. Start the Ngrok Tunnel

In a **separate** terminal window:

```bash
ngrok http 3000
```

Ngrok will display something like:

```
Forwarding    https://a1b2c3d4.ngrok-free.app -> http://localhost:3000
```

That `https://a1b2c3d4.ngrok-free.app` URL is your public dashboard link. Share it with your squadron in Discord.

> **Note:** Keep both windows open. If you close either one, the dashboard goes offline.

---

### Setting Up a Permanent Ngrok Link (Paid)

If you want a URL that never changes — something your members can bookmark permanently — follow these steps after upgrading to the Ngrok Starter plan.

#### 1. Upgrade Your Ngrok Plan

Go to [ngrok.com/pricing](https://ngrok.com/pricing) and upgrade to **Starter** ($10/month). This unlocks custom domains and static addresses.

#### 2. Reserve a Static Domain

1. In your Ngrok dashboard, go to **Cloud Edge** → **Domains**
2. Click **New Domain**
3. Choose a name like `my-squadron-bgs.ngrok.app`
4. Click **Create**

Your domain is now reserved — it will always point to your tunnel when it's running.

#### 3. Start Ngrok with Your Static Domain

Instead of `ngrok http 3000`, use:

```bash
ngrok http --domain=my-squadron-bgs.ngrok.app 3000
```

Your dashboard is now permanently accessible at `https://my-squadron-bgs.ngrok.app` — every time you start Ngrok with that command, the same URL is live.

#### 4. Make It Easy to Start (Windows)

Create a file called `start-with-tunnel.bat` in your project folder:

```batch
@echo off
start "BGS Server" cmd /k "node server.js"
timeout /t 3
start "Ngrok Tunnel" cmd /k "ngrok http --domain=my-squadron-bgs.ngrok.app 3000"
echo Dashboard starting at https://my-squadron-bgs.ngrok.app
pause
```

Double-click it to start both the server and the tunnel in one click.

---

## Project Structure

```
elite-bgs-analyzer/
├── server.js              # Main Express server + all API routes
├── eddn-listener.js       # EDDN ZeroMQ listener + tick detection
├── bgs-analyzer.js        # CLI companion tool
├── inara.js               # Inara API helper
├── public/
│   └── index.html         # Full single-page dashboard (HTML/CSS/JS)
├── data/                  # Auto-generated runtime data (gitignored)
│   ├── squadron_config.json
│   ├── users.json
│   ├── tick_history.json
│   └── ...
├── .env                   # Your API keys (gitignored, NEVER share)
├── .env.example           # Template — copy to .env to start manually
├── SETUP.txt              # Detailed setup guide
├── package.json
└── README.md
```

---

## Updating

When a new version is released, pull the latest code and restart:

```bash
git pull
npm install
node server.js
```

Your `data/` folder and `.env` are gitignored so your configuration and user data are never overwritten by an update.

---

## Security Notes

- Your `.env` file contains your API keys. **Never share it, never commit it to GitHub.**
- The `.gitignore` in this repo excludes `.env` and all `data/` files by default.
- Leadership and Dev passwords are set during the setup wizard. Change them if you ever suspect they've been compromised — re-run setup by deleting `data/squadron_config.json` and restarting the server.
- This is a **self-hosted** tool. You control all the data. Nothing is sent to any third party except the AI API calls you configure.

---

## Troubleshooting

**Dashboard shows setup wizard every time**
- Make sure `data/squadron_config.json` exists and `"setupComplete": true` is set.
- If you deleted the file, just go through the wizard again.

**AI analysis returns an error**
- Check that your API keys are correct in `.env`
- Gemini free tier has a daily limit (~50 requests). If you hit it, the system will fall over to Groq automatically.
- Run the server from a terminal to see error output.

**EDDN not receiving data**
- EDDN requires an outbound connection to `eddn.edcd.io:9500` (ZeroMQ). Check your firewall.
- Data only flows when players are actively submitting journals. It can be quiet during off-peak hours.


**Theme save returns an error**
- Make sure the server is fully restarted after any updates.
- The `/api/users/theme` endpoint requires the server to be running the latest `server.js`.

---

## Contributing

Pull requests welcome. If you add a feature, please test it with a clean first-boot (delete `data/squadron_config.json` first).

---

## License

MIT License — free to use, modify, and distribute. Credit appreciated but not required.

---

*Built for Elite Dangerous squadron commanders who want real intelligence, not just data tables.*

