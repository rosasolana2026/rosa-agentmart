# Pairing Your AI to Your Phone
## WhatsApp · Telegram · Discord — Complete Setup Guide

*Part of the Rosalinda CEO Bundle*

---

## Which Channel Should I Use?

| Channel | Best for | Setup time | Cost |
|---|---|---|---|
| **Telegram** | Speed, reliability, bots | 5 min | Free |
| **Discord** | Teams already on Discord | 10 min | Free |
| **WhatsApp** | Personal use, always on your phone | 3 min | Free |

**Our recommendation:** Start with Telegram. It's the most reliable and fastest to set up.

---

## Pairing Telegram (Recommended)

### Step 1: Create a Telegram Bot

1. Open Telegram on your phone
2. Search for `@BotFather` (official Telegram bot)
3. Send: `/newbot`
4. It asks for a name — type anything (e.g., "My CEO Assistant")
5. It asks for a username — must end in `bot` (e.g., `mycompany_ceo_bot`)
6. BotFather replies with your **bot token**: `1234567890:ABCdef...`
7. **Copy this token** — you'll need it in Step 3

### Step 2: Get Your Telegram Chat ID

1. In Telegram, search for `@userinfobot`
2. Send it any message (like "hello")
3. It replies with your **Chat ID** — a number like `987654321`
4. **Copy this number**

### Step 3: Configure OpenClaw

Open your terminal and run:

```bash
openclaw config set telegram.botToken "1234567890:ABCdef..."
openclaw config set telegram.chatId "987654321"
openclaw gateway restart
```

### Step 4: Test It

Open your Telegram bot (search for it by the username you created) and send: **"Hello"**

Your AI should respond within a few seconds. ✓

**Troubleshooting:**
- No response? Check `openclaw gateway status` — it should say "running"
- Wrong chat ID? Re-run `@userinfobot` — make sure you got your own ID, not the bot's

---

## Pairing Discord

### Step 1: Enable Developer Mode

In Discord: **User Settings** (bottom left gear) → **Advanced** → toggle **Developer Mode** ON

### Step 2: Create a Discord Application

1. Go to **https://discord.com/developers/applications**
2. Click **New Application** → name it (e.g., "My AI Assistant") → Create
3. Go to the **Bot** tab in the left sidebar
4. Click **Add Bot** → confirm
5. Under the bot's username, click **Reset Token** → **Copy** your bot token
6. Scroll down, enable:
   - **Message Content Intent** — toggle ON
   - **Server Members Intent** — toggle ON (optional)

### Step 3: Invite the Bot to Your Server

1. Go to **OAuth2** → **URL Generator** in the left sidebar
2. Under **Scopes**, check: `bot`
3. Under **Bot Permissions**, check:
   - Send Messages
   - Read Message History
   - View Channels
4. Copy the generated URL at the bottom
5. Open it in your browser → select your Discord server → Authorize

### Step 4: Get Your Channel ID

1. In Discord, right-click the channel where you want your AI to live
2. Click **Copy Channel ID** (you'll see this option because Developer Mode is on)
3. It copies a number like `1234567890123456789`

### Step 5: Configure OpenClaw

```bash
openclaw config set discord.token "YOUR_BOT_TOKEN_HERE"
openclaw config set discord.channelId "YOUR_CHANNEL_ID_HERE"
openclaw gateway restart
```

### Step 6: Test It

Go to your Discord channel and type: **"hello"**

Your AI should respond. ✓

**Troubleshooting:**
- Bot not responding? Check that Message Content Intent is enabled in the Discord Developer Portal
- Bot offline (gray dot)? Run `openclaw gateway restart`
- "Missing permissions"? Re-invite the bot using the OAuth2 URL Generator with correct permissions

---

## Pairing WhatsApp

WhatsApp uses a QR code scan — takes under 3 minutes.

### Step 1: Start the Pairing

In your terminal:

```bash
openclaw whatsapp login
```

A QR code appears in your terminal window. Keep this window open.

### Step 2: Scan from Your Phone

**iPhone:**
1. Open WhatsApp
2. Tap **Settings** (bottom right)
3. Tap **Linked Devices**
4. Tap **Link a Device**
5. Scan the QR code

**Android:**
1. Open WhatsApp
2. Tap the **three dots** menu (top right) or your avatar
3. Tap **Linked Devices**
4. Tap **Link a Device**
5. Scan the QR code

After scanning, the terminal shows: `✓ WhatsApp connected`

### Step 3: Test It

Send yourself a WhatsApp message from any contact (or use WhatsApp Web). Your AI intercepts it and responds.

**Note:** WhatsApp sessions expire after ~2 weeks of inactivity. Re-run `openclaw whatsapp login` to refresh.

---

## Using Multiple Channels at Once

You can have all three active simultaneously. OpenClaw routes messages from all channels to your AI and replies back on the same channel the message came from.

```bash
# Check all configured channels
openclaw config get

# Check which channels are active
openclaw gateway status
```

---

## Pro Tips

**Set a custom greeting:** When your AI connects to a new channel, it introduces itself. Customize this in your `SOUL.md`:

```markdown
## Greeting
When a new conversation starts, introduce yourself as [Name] and ask how you can help.
```

**Set quiet hours:** In `HEARTBEAT.md`, you can tell your AI not to message you between certain hours:

```markdown
## Quiet Hours
Do not proactively message CEO between 10pm and 7am ET.
```

**Multiple users on Discord:** You can allow trusted team members to interact with your AI in Discord by configuring sender allowlists in your OpenClaw config.

---

*Need help? Email rosa.solana2026@icloud.com or visit rosabuilds.com*

© 2026 Rosalinda Solana
