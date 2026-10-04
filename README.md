# 🥰 MONA LISA 🤭 — Guardian Edition

*Elegant. Legendary. Purposeful. Crafted by Bagenda Nicholas.*

A WhatsApp bot built on [Baileys](https://github.com/WhiskeySockets/Baileys), designed for creators who value innovation, security, and meaning. Features pairing-code login, a modular plugin system, and integrated AI/Image/Video capabilities—all rebuilt with transparency and integrity.

---

## ️ Before you deploy — read this

This project was meticulously rebuilt from a template that originally contained malicious code. The following have been **removed entirely**, not hidden or patched:

1.  **`lib/system.js`** previously held a 169KB obfuscated blob with anti-debugging code hooked into the live WhatsApp session. It has been replaced with a clean, readable file handling only essential tasks (channel follow / auto-react / status).
2.  **Credential Harvesting:** A `.pair` / `.pair2` command used to forward user phone numbers to an unauthorized third-party server to generate linking codes. This security vulnerability has been completely deleted.
3.  **NSFW/"Leak" Plugins:** Explicit content scrapers (`nsfw-girls.js`, `leakvideos.js`) have been permanently removed. This bot is built for creativity and purpose, not exploitation.

> **⚡ Security Note:** If you merge changes from other sources, **never** reintroduce these files. Your digital safety matters.

**License & Ethics:** Derived from an MIT-licensed template by "ArslanMD Official". While the license permits use, I believe technology should serve people's hearts and minds. This edition is curated to align with values of integrity and meaningful creation.

**Platform Risk:** This bot uses Baileys (unofficial API). While common, it operates outside WhatsApp's official Terms of Service. Use responsibly; accounts can be flagged.

---

## ✨ What's Included in Guardian Edition

-   **Secure Pairing Login:** Redesigned web UI (`pair.html`) with cinematic aesthetics and no credential leaks.
-   **Modular Plugin System:** Auto-loaded commands (`plugins/*.js`) for easy customization.
-   **Smart Automation:** Channel follow, auto-react, status handling via transparent `lib/system.js`.
-   **Group Protection:** Anti-link, anti-bad-words, anti-call, anti-delete (all verified working).
-   **AI & Creative Studio:** Pluggable providers for Chat, Image (Stability AI), Video (Replicate), and Music—gated behind *your* keys.
-   **Guardian Personality:** Reusable response pools (`lib/responses.js`) for consistent, elegant interactions.
-   **Dynamic Menu:** `.menu` generates live categories based on loaded plugins.
-   **Entertainment Suite:** Jokes, facts, trivia, riddles, coinflip, dice, and more.
-   **Centralized Config:** Fully branded `config.js` for easy management.

---

## 🐛 Critical Bugs Fixed

| Bug | Impact | Fix |
| :--- | :--- | :--- |
| Obfuscated `system.js` (169KB) | Full session hijack risk | Rewritten clean & transparent |
| Credential harvesting via `.pair` | User data theft | Feature deleted entirely |
| Broken `anti-bad.js` import | Moderation silently failed | Fixed import to `{ cmd }` |
| Broken `antilink.js` import | Link protection disabled | Fixed import to `{ cmd }` |
| Empty `m.quoted` object | Reply-based commands crashed | Rebuilt message parser in `lib/msg.js` |
| Hardcoded owner numbers | Wrong admin privileges | Now uses `config.OWNER_NUMBER` dynamically |
| Duplicate `CHANNEL_JID` | Config confusion | De-duplicated |
| Node built-ins as dependencies | Supply chain bloat | Removed from `package.json` |
| Legacy branding scattered everywhere | Identity mismatch | Rebranded to Guardian Edition |
| Premature "connected" state | Permanent lockout on failure | Validates socket + login before marking active |
| No recovery from stuck sessions | Users trapped in "Already Connected" | Added `/force-code` route & UI button |
| Unhandled `restartRequired` disconnect | Infinite "Logging in..." hang | Fast reconnect path added |
| Race condition: Reconnect vs DB Save | Session wiped mid-login | Local session grace period + write delay |
| Silent MongoDB boot failure | Persistence lost forever | Retry-with-backoff + event logging |
| Missing `config`/`botNumber` in dispatch | Settings toggles crashed | Added to all 3 dispatch sites |
| Wrong DB function name in settings | Toggles threw errors | Aliased to `updateUserConfigInMongoDB` |
| Missing import in `antidelete.js` | Status check crashed | Import added |
| Antidelete sent text labels only | Owners couldn't see deleted media | Now re-downloads & forwards actual files |
| No edit detection | Message edits were invisible | Added `lib/antiedit.js` with diff reporting |

---

## 📁 Project Structure

```text
.
├── main.js              # Connection handling, routing, HTTP server
├── index.js             # Process entrypoint
├── redx.js              # Command registration engine
├── config.js            # Centralized configuration
├── pair.html            # Cinematic pairing web UI
├── plugins/             # Auto-loaded command modules
├── providers/           # AI / Image / Video / Music adapters
│   ├── ai/              # OpenAI-compatible chat/code/translate
│   ├── stability/       # Stability AI v2beta (Image/3D/Audio)
│   └── video/           # Replicate (Wan-2.2 T2V/I2V)
├── lib/                 # Shared helpers & parsers
├── data/                # Runtime presence helpers
├── .env.example         # Environment variable template
└── app.json             # Railway/Render deployment config
```

---

## 🔧 Required Environment Variables

See `.env.example` for full documentation. Minimum setup:

```bash
OWNER_NUMBER=2567XXXXXXXXX  # Your number (Uganda +256 format supported)
PREFIX=.
```

AI/Creative features remain disabled until you add specific API keys. This ensures you only pay for what you use.

---

## ▶️ Running Locally

```bash
git clone https://github.com/BagendaNicholas/MONA-LISA-Mini-Guardian
cd MONA-LISA-Mini-Guardian
npm install
cp .env.example .env
# Edit .env with your OWNER_NUMBER
npm start
```

Visit `http://localhost:3000` to pair securely.

---

## 🚀 Deployment

Requires a **long-running Node.js process** (WebSocket connection). Not compatible with serverless platforms.

✅ **Recommended:** VPS (DigitalOcean/Hetzner) with PM2, Railway, Render, or Fly.io.
❌ **Avoid:** Vercel Serverless, Cloudflare Workers.

Set `MONGODB_URI` for session persistence across restarts.

---

## 🧠🎨🎵 Creative Studio Configuration

-   **AI Chat/Code:** Any OpenAI-compatible endpoint via `providers/ai/`.
-   **Image/3D/Audio:** Stability AI v2beta via `STABILITY_API_KEY`. Supports generation, upscaling, editing, control, 3D conversion, and music generation.
-   **Video:** Replicate via `REPLICATE_T2V_MODEL` / `REPLICATE_I2V_MODEL`. Uses Wan-2.2 models (verified against official docs).
-   **Talking Avatar:** `REPLICATE_AVATAR_MODEL` (default: `prunaai/p-video-avatar`). Generates lip-synced speech from portraits.

> **Note:** Stability deprecated their own video API in July 2025. We use Replicate for reliable video generation.

---

## 📜 Command Menu

Send `.menu` for a live, categorized list of 354+ commands spanning AI, creative tools, entertainment, group management, and utilities.

**Ethical Boundaries:** Deliberately excludes scraping, stalking tools, recaptcha bypasses, fake premium systems, and explicit content aggregators. Technology should elevate, not exploit.

---

## 🧪 Testing Status

✅ **Verified:** Syntax, command registration, message parsing logic, JSON validity, pairing UI API contract.
⚠️ **Smoke Test Needed:** Live pairing flow, MongoDB persistence, and AI provider calls require real credentials. Always test with your own keys before production use.

---

## 📢 Official Channel

[Join the Guardian Community](https://whatsapp.com/channel/0029Vb7Lk3yAzNbrVaWDOk1P)

---

*© 2026 🥰 MONA LISA 🤭 · Guardian Edition · Crafted by Bagenda Nicholas*
*Where ideas become meaningful digital projects.*
