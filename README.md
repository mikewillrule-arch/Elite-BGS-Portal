<div align="center">

<img src="https://i.imgur.com/placeholder.png" alt="Elite BGS Analyzer" width="120"/>

# Elite BGS Analyzer
### Squadron Intelligence Dashboard for Elite Dangerous

[![Node.js](https://img.shields.io/badge/Node.js-v18%2B-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)](https://nodejs.org)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)](LICENSE)
[![EDDN](https://img.shields.io/badge/Data-EDDN%20Live-00d4ff?style=for-the-badge)](https://eddn.edcd.io)
[![AI Powered](https://img.shields.io/badge/AI-Gemini%20%7C%20Groq%20%7C%20Mistral-ff8800?style=for-the-badge)](https://aistudio.google.com)
[![Self Hosted](https://img.shields.io/badge/Self--Hosted-Your%20Data-00ff88?style=for-the-badge)](#installation)

**Real-time BGS tracking · AI-powered briefings · Tick detection · War tables · Rival monitoring**

[▶ Live Demo](https://nonskeletal-davin-nonzonated.ngrok-free.dev/) &nbsp;·&nbsp; [Installation](#installation) &nbsp;·&nbsp; [Free API Keys](#getting-your-free-api-keys) &nbsp;·&nbsp; [Ngrok Setup](#remote-access-with-ngrok)

</div>

---

> **Built for squadrons who take the BGS seriously.** Most tools give you raw data tables. This gives you command intelligence — live EDDN feed, AI executive briefings, automatic post-tick monitoring, and a full squadron command center, all in a single self-hosted web app.

---

## 🛡️ Is It Safe to Run?

<details>
<summary><strong>Click here — important reading before you install</strong></summary>

<br>

Fair question, and a smart instinct. Here is exactly what this program does on your machine.

**What kind of file is this?**

This is a **Node.js web application** — the same technology stack that powers Discord, Slack, GitHub, and Twitch. It is not a compiled `.exe` from unknown source. It is plain, human-readable JavaScript text files that Node.js runs line by line. Open `server.js` in Notepad right now and read it before running anything. Nothing is hidden, obfuscated, or compiled into a binary blob.

**Complete list of what it does to your PC:**

| Action | Details |
|---|---|
| Opens port 3000 on localhost | Local web server only. Not internet-facing unless you set up Ngrok yourself. |
| Connects to `eddn.edcd.io:9500` | The official Elite Dangerous Data Network — same source as Inara, EDDB, EliteBGS.app. Outbound only. |
| Makes HTTPS API calls | To Gemini, Groq, EliteBGS.app, Inara — services you configure. Outbound only. Same as a browser. |
| Writes to `data/` folder | Squadron config, user accounts, BGS history. Only inside the project folder. Nowhere else. |

**What it does NOT do:**

- ❌ Does not read your files, documents, or Elite Dangerous journal files
- ❌ Does not install anything system-wide or add startup entries
- ❌ Does not run in the background after you close the terminal
- ❌ Does not modify the Windows registry
- ❌ Does not make any outbound connections beyond the three listed above
- ❌ Does not collect or send your personal data anywhere

**Still not sure? Scan it first — completely reasonable.**

**VirusTotal** (no install needed):
1. Go to [virustotal.com](https://www.virustotal.com)
2. Zip the project folder and upload it — or upload `server.js` and `eddn-listener.js` individually
3. 70+ antivirus engines scan it in about 30 seconds

**Your local AV:**
Right-click the project folder → Scan with Windows Defender / Malwarebytes / whatever you use. JavaScript files are plain text — any AV can read them.

**Read the source yourself:**
Open `server.js` in VS Code or Notepad. `Ctrl+F` for `exec`, `spawn`, `writeFile` to see every system call the program makes. Everything is commented.

> If you've ever run a Minecraft server, a Discord bot, or any other self-hosted tool — this is the same category of thing. It runs when you start it and stops when you close the window.

</details>

---

## 🆚 Why Use This Over Other Tools?

Most BGS tools (Inara, EDDB, EliteBGS.app) give you **data**. This gives you **decisions**.

| Feature | Other Tools | Elite BGS Analyzer |
|---|:---:|:---:|
| Live EDDN data — no manual refresh | ❌ | ✅ Real-time ZeroMQ feed |
| AI executive briefings | ❌ | ✅ Gemini · Groq · Mistral |
| BGS tick auto-detection | ❌ | ✅ EDDN + tick.edcd.io |
| Post-tick change monitoring | ❌ | ✅ Auto-polls + AI diff report |
| War table with conflict tracking | ❌ | ✅ Built-in |
| Rival faction influence monitor | ❌ | ✅ Real-time |
| Squadron member accounts & ranks | ❌ | ✅ Login, ranks, messaging |
| Per-user color themes | ❌ | ✅ Saved to user profile |
| CMDR activity tracking | ❌ | ✅ Dev dashboard + commendations |
| Works on LAN or internet | ❌ | ✅ Ngrok tunnel support |
| Open source, self-hosted | ❌ | ✅ Your data, your server |

---

## ✨ Features

<details>
<summary><strong>📡 Live BGS Intelligence</strong></summary>

<br>

- **Real-time EDDN feed** — listens to the Elite Dangerous Data Network via ZeroMQ. Every FSD jump and location event from every player in the game flows through. Your faction's influence updates the moment a journal is submitted anywhere.
- **BGS Tick Detection** — dual-source detection: EDDN influence change threshold (watches all factions, not just yours) + live WebSocket push from `tick.edcd.io`. Both run in parallel with a 12-hour gate to prevent double-firing.
- **Post-Tick Monitoring** — on tick detection, the system snapshots all watched systems from EliteBGS API, then polls for changes every 20 minutes for 1 hour. When changes are detected, an AI brief is generated and pushed to all connected browser clients in real time.
- **Tick Countdown** — live `Xh MMm SSs` countdown to the next 15:50 UTC BGS tick in the header bar.

</details>

<details>
<summary><strong>🤖 AI-Powered Analysis</strong></summary>

<br>

- **Executive Briefings** — full squadron operations brief on demand. The AI has context for your faction, influence levels, active states, conflicts, and recent post-tick changes.
- **Strategy Suggestions** — AI-optimized BGS action plans based on current system states.
- **Journal Analysis** — paste Elite Dangerous journal events and get a BGS contribution breakdown per CMDR.
- **Automatic AI Fallback Chain** — Gemini → Groq (LLaMA 3.3 70B) → OpenRouter → Mistral. If your primary AI hits its daily quota, the next provider takes over silently. All have generous free tiers.

</details>

<details>
<summary><strong>⚔️ Squadron Command Center</strong></summary>

<br>

- **War Table** — all active conflicts your faction is involved in. Combat bond counts, war states, opposing factions.
- **Rival Faction Monitor** — set a rival faction and track their influence across all their systems in real time. Get AI trajectory analysis.
- **System Deep Dive** — full breakdown per system: all factions, influence history, active/pending states, last-seen timestamp.
- **Galactic Map Annotations** — mark key systems on your sector map with custom labels and colors.

</details>

<details>
<summary><strong>👥 Squadron Social Features</strong></summary>

<br>

- **User Accounts** — members register with CMDR name and password. Leadership has a separate admin key.
- **Rank System** — assign ranks to members (Recruit through Wing Commander).
- **Internal Messaging** — leadership announcements and direct inbox messages.
- **Activity Tracking** — CMDR journal submission counts, most active commanders, commendation leaderboard.
- **Per-User Color Themes** — Cyan, Amber, Red, Purple, White presets or fully custom hex values. Saved to each user's profile.

</details>

<details>
<summary><strong>🧙 First-Boot Setup Wizard</strong></summary>

<br>

On first launch, a full-screen setup wizard appears automatically and walks you through:

1. Squadron name (as it appears on Inara)
2. Initials badge and brand colors
3. Leadership password and dev/log password
4. API keys for Gemini, Groq, OpenRouter, Mistral, and Inara

Configuration saves to `data/squadron_config.json`. The `.env` file is written automatically. No manual file editing required.

</details>

<details>
<summary><strong>💻 CLI Companion (bgs-analyzer.js)</strong></summary>

<br>

A terminal-based BGS tool with slash commands for commanders who prefer the console:

| Command | Action |
|---|---|
| `/watch <system>` | Add a system to post-tick monitoring |
| `/unwatch <system>` | Remove a system |
| `/tick` | Show tick status and countdown |
| `/squadron` | Fetch squadron data from Inara |
| `/analyze` | Run AI analysis from the terminal |

Set `WATCH_SYSTEMS=Sol,Deciat` in `.env` for auto-monitoring on every launch.

</details>

---

## 📋 Requirements

- **Node.js** v18 or higher — [nodejs.org](https://nodejs.org)
- **npm** — included with Node.js
- **At least one AI API key** — all free tier, instructions below
- **Ngrok** *(optional)* — only if you want access outside your home network

---

## 🚀 Installation

### Step 1 — Download

```bash
git clone https://github.com/YOUR_USERNAME/elite-bgs-analyzer.git
cd elite-bgs-analyzer
```

Or download and extract the ZIP from the releases page.

### Step 2 — Install Dependencies

```bash
npm install
```

Installs Express, ZeroMQ, ws, dotenv, and ~30 other audited open-source packages. Takes about 30 seconds.

### Step 3 — Start the Server

**Windows:**
```
Double-click start.bat
```

**Mac / Linux:**
```bash
node server.js
```

### Step 4 — Complete the Setup Wizard

Open **`http://localhost:3000`** in your browser.

The setup wizard appears automatically on first launch. Fill in your squadron name, colors, passwords, and API keys — then click **COMPLETE SETUP**. The dashboard loads with your squadron's branding applied.

---

## 🔑 Getting Your Free API Keys

All AI providers below have a free tier sufficient for daily BGS analysis.

<details>
<summary><strong>Gemini — Primary AI (Free)</strong></summary>

1. Go to [aistudio.google.com](https://aistudio.google.com)
2. Sign in with a Google account
3. Click **Get API Key** → **Create API key**
4. Copy the key — it starts with `AIza...`

</details>

<details>
<summary><strong>Groq — Fallback 1 (Free)</strong></summary>

1. Go to [console.groq.com](https://console.groq.com)
2. Create a free account
3. Go to **API Keys** → **Create API Key**
4. Copy the key — it starts with `gsk_...`

</details>

<details>
<summary><strong>OpenRouter — Fallback 2 (Free tier)</strong></summary>

1. Go to [openrouter.ai/keys](https://openrouter.ai/keys)
2. Create a free account
3. Click **Create Key**
4. Copy the key — it starts with `sk-or-v1-...`

</details>

<details>
<summary><strong>Mistral — Fallback 3 (Free tier)</strong></summary>

1. Go to [console.mistral.ai/api-keys](https://console.mistral.ai/api-keys)
2. Create a free account
3. Click **Create new key** and copy it

</details>

<details>
<summary><strong>Inara — Optional, Squadron Data</strong></summary>

1. Go to [inara.cz/elite/settings-api](https://inara.cz/elite/settings-api/)
2. Log in with your Inara account
3. Register an application (name it anything — e.g. `BGS Dashboard`)
4. Copy the API key shown

</details>

---

## 🌐 Remote Access with Ngrok

By default the dashboard runs on `http://localhost:3000` — your machine only. To let squadron members connect from outside your network, use Ngrok.

**What is Ngrok?** It creates a secure tunnel from the internet to your local server. You get a public URL like `https://abc123.ngrok-free.app` that anyone can open in a browser.

### Free vs Paid

| | Free Plan | Paid (~$10/mo) |
|---|---|---|
| URL | Random, changes on restart | Permanent custom domain |
| Sessions | 1 at a time | Multiple |
| Bandwidth | Limited but sufficient | Higher |

For most squadrons the free plan is fine — just paste the new URL in Discord each session. For a permanent bookmarkable link, upgrade to Starter.

---

<details>
<summary><strong>📡 Ngrok Setup — Step by Step (Free Plan)</strong></summary>

<br>

**1. Create a free Ngrok account**

Go to [ngrok.com](https://ngrok.com) and sign up.

**2. Download Ngrok**

- **Windows** — download the `.zip` from [dashboard.ngrok.com/get-started/setup](https://dashboard.ngrok.com/get-started/setup), extract `ngrok.exe` to a folder like `C:\ngrok\`
- **Mac** — `brew install ngrok/ngrok/ngrok`
- **Linux** — `snap install ngrok`

**3. Authenticate (one time only)**

In your Ngrok dashboard, go to **Your Authtoken** and copy it:

```bash
ngrok config add-authtoken YOUR_AUTHTOKEN_HERE
```

**4. Start the dashboard**

```bash
node server.js
```

**5. In a second terminal, start the tunnel**

```bash
ngrok http 3000
```

Ngrok shows:
```
Forwarding    https://a1b2c3d4.ngrok-free.app -> http://localhost:3000
```

Share that URL with your squadron. Keep both windows open — closing either takes the dashboard offline.

</details>

<details>
<summary><strong>🔒 Permanent Ngrok Link — Static Domain (Paid Plan)</strong></summary>

<br>

After upgrading to Ngrok Starter at [ngrok.com/pricing](https://ngrok.com/pricing):

**1. Reserve your static domain**

In the Ngrok dashboard → **Cloud Edge** → **Domains** → **New Domain**

Pick a name like `my-squadron-bgs.ngrok.app` and click **Create**.

**2. Start Ngrok with your domain**

```bash
ngrok http --domain=my-squadron-bgs.ngrok.app 3000
```

Your dashboard is now permanently at `https://my-squadron-bgs.ngrok.app` every time you run that command.

**3. One-click Windows launcher**

Create `start-with-tunnel.bat` in your project folder:

```batch
@echo off
start "BGS Server" cmd /k "node server.js"
timeout /t 3
start "Ngrok Tunnel" cmd /k "ngrok http --domain=my-squadron-bgs.ngrok.app 3000"
echo Dashboard live at https://my-squadron-bgs.ngrok.app
pause
```

Double-click to start everything in one shot.

</details>

---

## 📁 Project Structure

```
elite-bgs-analyzer/
├── server.js              # Express server + all API routes
├── eddn-listener.js       # EDDN ZeroMQ listener + tick detection
├── bgs-analyzer.js        # CLI companion tool
├── inara.js               # Inara API helper
├── public/
│   └── index.html         # Single-page dashboard (HTML/CSS/JS)
├── data/                  # Runtime data — auto-generated, gitignored
│   ├── squadron_config.json
│   ├── users.json
│   ├── tick_history.json
│   └── ...
├── .env                   # Your API keys — NEVER commit this
├── .env.example           # Key template
├── SETUP.txt              # Detailed setup guide
├── start.bat              # Windows launcher
├── setup.bat              # Windows first-run helper
└── README.md
```

---

## 🔄 Updating

```bash
git pull
npm install
node server.js
```

Your `data/` folder and `.env` are gitignored — your config and user data survive every update.

---

## 🔐 Security Notes

- Your `.env` file contains API keys. **Never share it. Never commit it.** The `.gitignore` excludes it automatically.
- Passwords are set during setup. To reset, delete `data/squadron_config.json` and restart the server — the wizard runs again.
- This is fully self-hosted. Your data never leaves your machine except for the AI API calls you explicitly configure.

---

## 🛠️ Troubleshooting

<details>
<summary>Setup wizard appears every time</summary>

Check that `data/squadron_config.json` exists and contains `"setupComplete": true`. If you deleted the file, run through the wizard again.

</details>

<details>
<summary>AI analysis returns an error</summary>

- Verify your API keys in `.env` are correct
- Gemini free tier has a daily request limit — if hit, the system falls over to Groq automatically
- Run the server in a terminal to see live error output

</details>

<details>
<summary>EDDN not receiving data</summary>

- EDDN requires outbound access to `eddn.edcd.io:9500` (ZeroMQ). Check your firewall.
- Data only flows when players are actively playing and submitting journals. Off-peak hours can be quiet.

</details>

<details>
<summary>Theme save returns a JSON error</summary>

Restart the server. The `/api/users/theme` endpoint requires the running process to have loaded the latest `server.js`.

</details>

<details>
<summary>Ngrok URL changed</summary>

The free plan generates a new URL every time Ngrok restarts. Upgrade to a Starter plan for a permanent static domain, or paste the new URL in Discord each session.

</details>

---

## 🤝 Contributing

Pull requests welcome. When adding a feature, test with a clean first-boot — delete `data/squadron_config.json` and restart the server to trigger the setup wizard.

---

## 📄 License

MIT License — free to use, modify, and distribute. Credit appreciated but not required.

---

<div align="center">

*Built for Elite Dangerous squadron commanders who want real intelligence, not just data tables.*

[![Demo](https://img.shields.io/badge/▶%20Live%20Demo-Try%20It%20Now-00d4ff?style=for-the-badge)](https://nonskeletal-davin-nonzonated.ngrok-free.dev/)

</div>
