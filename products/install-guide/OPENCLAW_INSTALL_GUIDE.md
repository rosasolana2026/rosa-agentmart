# How to Give Your AI a Real Job
## A Step-by-Step Guide to Installing OpenClaw on Your MacBook — Full Access, Screen Control, Everything

*By Rosalinda Solana*
*Version 1.0 — February 2026*

---

## Before You Start

This guide shows you exactly how to install OpenClaw on your MacBook, give it full machine access, connect it to WhatsApp/Telegram/Discord, and pair it with a real AI brain (Claude). By the end, your AI will be able to write files, run commands, browse the web, see your screen, and talk back to you on your phone.

**Time required:** About 30–45 minutes
**Cost to run:** ~$5–20/month (Anthropic API, no subscription)
**What you need:**
- A MacBook (Apple Silicon M1/M2/M3/M4 recommended)
- Admin password access
- An Anthropic account (claude.ai — free to create)
- A phone number (for WhatsApp or Telegram pairing)

---

## Step 1: Install Homebrew (macOS Package Manager)

Homebrew is the tool that installs everything else. Open **Terminal** (press `Cmd+Space`, type "Terminal", press Enter).

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

When prompted, type your Mac password and press Enter. It will install for several minutes.

After it finishes, add Homebrew to your PATH:

```bash
# For Apple Silicon (M1/M2/M3/M4):
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zshrc && source ~/.zshrc

# For older Intel Macs:
echo 'eval "$(/usr/local/bin/brew shellenv)"' >> ~/.zshrc && source ~/.zshrc
```

Verify it works:
```bash
brew --version
```
You should see something like `Homebrew 4.x.x`. ✓

---

## Step 2: Install Node.js

OpenClaw runs on Node.js. Install it via Homebrew:

```bash
brew install node
```

Verify:
```bash
node --version   # Should show v20 or higher
npm --version    # Should show 10 or higher
```

---

## Step 3: Install OpenClaw

```bash
npm install -g openclaw
```

This installs the `openclaw` command globally. Verify:

```bash
openclaw --version
```

---

## Step 4: Get Your Anthropic API Key

1. Go to **https://console.anthropic.com** in your browser
2. Sign up or log in
3. Click your name (top right) → **API Keys**
4. Click **+ Create Key**, name it "OpenClaw", copy the key (starts with `sk-ant-...`)
5. Add $10 credit at **Settings → Billing** (this lasts weeks to months of normal use)

Store your key safely — you'll use it in the next step.

---

## Step 5: Configure OpenClaw

Run the interactive setup:

```bash
openclaw setup
```

When asked for your AI provider, select **Anthropic (Claude)**. Paste your API key.

Or set it directly:

```bash
openclaw config set anthropic.apiKey "sk-ant-YOUR_KEY_HERE"
openclaw config set model "anthropic/claude-sonnet-4-6"
```

---

## Step 6: Start the Gateway

The Gateway is OpenClaw's background daemon — it keeps your AI running.

```bash
openclaw gateway start
```

Check it's running:
```bash
openclaw gateway status
```

You should see: `● Gateway: running`. ✓

**Make it start on login automatically:**
```bash
openclaw gateway start --autostart
```

---

## Step 7: Give Full Machine Access

This is what makes your AI actually useful. Without these permissions, it's just a chatbot.

### 7a. Grant Accessibility Access (for screen control)

OpenClaw needs macOS Accessibility permission to read your screen and control apps.

1. Open **System Settings** → **Privacy & Security** → **Accessibility**
2. Click the `+` button
3. Navigate to `/opt/homebrew/bin/` and add `openclaw` (or add Terminal if prompted)
4. Toggle it ON

### 7b. Grant Screen Recording Access

1. Open **System Settings** → **Privacy & Security** → **Screen Recording**
2. Add `openclaw` or your terminal app
3. Toggle it ON

### 7c. Grant Full Disk Access (optional but recommended)

Allows your AI to read/write files across your entire system:

1. Open **System Settings** → **Privacy & Security** → **Full Disk Access**
2. Add your terminal app (Terminal.app or iTerm2)
3. Toggle it ON

### 7d. Verify permissions are working

```bash
openclaw permissions check
```

---

## Step 8: Install Peekaboo (Screen Vision)

Peekaboo lets your AI see your screen and interact with macOS UI.

```bash
brew install peekaboo
```

Test it:
```bash
peekaboo screenshot --output /tmp/test.jpg && echo "Screen access works ✓"
```

---

## Step 9: Set Up Your Workspace

Your AI needs a home base — a folder it writes to, thinks from, and organizes itself in.

```bash
mkdir -p ~/.openclaw/workspace
openclaw config set workspace "~/.openclaw/workspace"
```

Create your identity files (OpenClaw reads these automatically):

```bash
cat > ~/.openclaw/workspace/USER.md << 'EOF'
# USER.md
- Name: [Your Name]
- What to call you: [First Name]
- Timezone: America/New_York
- Notes: You have full machine access. Ask before public posts or emails.
EOF
```

---

## Step 10: Test Your AI

```bash
openclaw chat "Hello — what can you see about my machine?"
```

Your AI should respond, introduce itself, and describe its capabilities. ✓

---

## Part 2: Connecting Your Phone

### Connect Telegram (Recommended — Free, Fast)

Telegram is the easiest and most reliable channel.

1. Install Telegram on your phone: **https://telegram.org**
2. Create a bot:
   - Open Telegram, search for `@BotFather`
   - Send `/newbot`
   - Name it anything (e.g., "My AI Assistant")
   - Copy the token it gives you (looks like `1234567890:ABCdefGhi...`)
3. Get your Chat ID:
   - Search for `@userinfobot` in Telegram
   - Send it any message — it replies with your Chat ID (a number)
4. Configure OpenClaw:

```bash
openclaw config set telegram.botToken "YOUR_BOT_TOKEN"
openclaw config set telegram.chatId "YOUR_CHAT_ID"
openclaw gateway restart
```

5. Open your Telegram bot and send: **"hello"**
   Your AI should reply instantly. ✓

---

### Connect Discord

Great if you're already in Discord all day.

1. Go to **https://discord.com/developers/applications**
2. Click **New Application** → name it "My AI"
3. Go to **Bot** tab → **Add Bot** → copy the Token
4. Go to **OAuth2** → **URL Generator**:
   - Scopes: `bot`
   - Permissions: `Send Messages`, `Read Messages/View Channels`
5. Copy the generated URL, open it in browser, add bot to your server
6. Get your channel ID: In Discord, right-click a channel → **Copy Channel ID** (enable Developer Mode first: User Settings → Advanced → Developer Mode)

```bash
openclaw config set discord.token "YOUR_BOT_TOKEN"
openclaw config set discord.channelId "YOUR_CHANNEL_ID"
openclaw gateway restart
```

Send a message in the Discord channel. Your AI responds. ✓

---

### Connect WhatsApp

WhatsApp requires a QR code scan — takes 2 minutes.

```bash
openclaw whatsapp login
```

A QR code appears in your terminal. Open WhatsApp on your phone:
- **iPhone:** Settings → Linked Devices → Link a Device → scan
- **Android:** Menu (⋮) → Linked Devices → Link a Device → scan

After scanning, your AI is reachable on WhatsApp. Text yourself on WhatsApp from any number. ✓

---

## Part 3: Giving Your AI a Personality

Drop these files into `~/.openclaw/workspace/`:

- `SOUL.md` — who your AI is, its values and operating principles
- `USER.md` — who you are (so it can personalize)
- `AGENTS.md` — define sub-agents if you want a multi-agent system
- `RULES.md` — hard rules (no spending without approval, etc.)

OpenClaw reads these automatically on every message.

**Pro tip:** Order the files however feels right. Your AI ingests all of them. The more specific you are, the more useful it becomes.

---

## Troubleshooting

| Problem | Fix |
|---|---|
| `openclaw: command not found` | Run `source ~/.zshrc` or restart Terminal |
| Gateway won't start | Check `openclaw gateway status` — look for port conflicts on 3333 |
| Telegram not responding | Double-check bot token + chat ID with `openclaw config get` |
| Screen access denied | Re-check System Settings → Privacy — toggle off/on, restart Terminal |
| API key error | Verify key at console.anthropic.com, ensure billing is active |

---

## What's Next?

You now have a fully operational AI running 24/7 on your MacBook. Here's what to do next:

1. **Add personality files** — drop in SOUL.md and RULES.md from the Rosalinda CEO Bundle (sold separately — see the bundle at shoprosalinda.com)
2. **Set up heartbeats** — your AI checks in on you proactively via HEARTBEAT.md
3. **Try the multi-agent system** — delegate tasks to specialized sub-agents
4. **Publish your own skills** — list them on shopclawmart.com and earn revenue

---

*Questions? Reach out at rosa.solana2026@icloud.com*
*More guides at rosabuilds.com*

© 2026 Rosalinda Solana. All rights reserved.
