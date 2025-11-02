# Telegram Shopify Checker Bot

A Telegram bot for checking Shopify store interactions with card validation features. Runs 24/7 on Render's free tier with UptimeRobot!

## Features

- Single card checking (`/sh`)
- Multiple card checking (`/msh`)
- Shopify URL management
- Proxy support with rotation
- Admin controls
- BIN lookup integration
- 24/7 uptime with free tier

## Quick Deploy to Render (Web Service + UptimeRobot)

### Step 1: Push to GitHub

```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin YOUR_GITHUB_REPO_URL
git push -u origin main
```

### Step 2: Deploy on Render

1. Go to [Render Dashboard](https://dashboard.render.com/)
2. Click "New +" → **"Web Service"** (important!)
3. Connect your GitHub repository
4. Configure:
   - **Name:** `telegram-shopify-bot` (or any name)
   - **Environment:** Python 3
   - **Build Command:** `pip install -r requirements.txt`
   - **Start Command:** `python main.py`
   - **Instance Type:** Free
5. Add environment variable:
   - **Key:** `TELEGRAM_BOT_TOKEN`
   - **Value:** Your bot token from [@BotFather](https://t.me/botfather)
6. Click "Create Web Service"
7. Wait for deployment (2-3 minutes)
8. Copy your service URL (e.g., `https://your-app.onrender.com`)

### Step 3: Keep It Online 24/7 with UptimeRobot

1. Go to [UptimeRobot.com](https://uptimerobot.com/) and sign up (free)
2. Click "Add New Monitor"
3. Configure:
   - **Monitor Type:** HTTP(s)
   - **Friendly Name:** Telegram Bot
   - **URL:** `https://your-app.onrender.com` (your Render URL)
   - **Monitoring Interval:** 5 minutes
4. Click "Create Monitor"
5. Done! Your bot now stays online 24/7 ✅

📖 **Detailed UptimeRobot Guide:** See [UPTIMEROBOT_SETUP.md](UPTIMEROBOT_SETUP.md)

## Environment Variables

Required environment variable in Render:

- `TELEGRAM_BOT_TOKEN` - Get this from [@BotFather](https://t.me/botfather) on Telegram

## How It Works

1. **Bot runs as a web service** on Render (port 5000)
2. **Web endpoints** respond to health checks:
   - Main page: `https://your-app.onrender.com/`
   - Health check: `https://your-app.onrender.com/health`
3. **UptimeRobot pings** every 5 minutes to keep it awake
4. **Telegram bot** runs in background thread (polling)
5. **Result:** 24/7 uptime on free tier! 🎉

## Local Development

1. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

2. **Set environment variable:**
   ```bash
   export TELEGRAM_BOT_TOKEN="your_bot_token_here"
   ```

3. **Run the bot:**
   ```bash
   python main.py
   ```

   The bot will start on `http://localhost:5000`

## Bot Commands

### User Commands
- `/start` - Show bot menu and available commands
- `/sh <card|mm|yy|cvv>` - Check a single card
- `/msh <card1> <card2> ...` - Check multiple cards (max 10)

### Admin Commands
- `/seturl <domain>` - Set global Shopify domain
- `/myurl` - Show current global domain
- `/rmurl` - Remove global URL
- `/addp <proxy>` - Add global proxy
- `/rp` - Remove global proxy
- `/lp` - List all proxies
- `/cp` - Check proxy status
- `/chkurl <domain>` - Test if a Shopify site works
- `/mchku` - Mass check multiple sites

## Project Structure

```
.
├── main.py                    # Main bot with Flask web server
├── shopify_auto_checkout.py   # Shopify checker logic
├── requirements.txt           # Python dependencies
├── pyproject.toml            # Python project configuration
├── render.yaml               # Render deployment configuration
├── README.md                 # This file
├── DEPLOY.md                 # Detailed deployment guide
├── UPTIMEROBOT_SETUP.md      # 24/7 uptime setup guide
└── .gitignore               # Git ignore rules
```

## Deployment Architecture

```
┌─────────────────┐
│  Render Free    │
│  Web Service    │  ← Hosts your bot
│  (Port 5000)    │
└────────┬────────┘
         │
         │ Pings every 5 min
         │
┌────────▼────────┐
│  UptimeRobot    │  ← Keeps it awake
│  Free Monitor   │
└─────────────────┘
         │
         │ Bot responds
         │
┌────────▼────────┐
│   Your Users    │  ← Use bot 24/7
│   on Telegram   │
└─────────────────┘
```

## Free Tier Limits

| Service | Cost | Limits |
|---------|------|--------|
| Render Web Service | $0 | 750 hours/month (enough for 24/7 with one service) |
| UptimeRobot | $0 | 50 monitors, 5-minute intervals |
| **Total** | **$0** | **24/7 bot uptime!** ✅ |

## Getting Your Telegram Bot Token

1. Open Telegram and search for [@BotFather](https://t.me/botfather)
2. Send `/newbot` command
3. Follow the prompts to create your bot
4. Copy the token provided (looks like: `123456789:ABCdef...`)
5. Add it as `TELEGRAM_BOT_TOKEN` environment variable in Render

## Troubleshooting

### Bot doesn't respond
- Check Render logs in dashboard
- Verify `TELEGRAM_BOT_TOKEN` is correct
- Make sure UptimeRobot monitor is active

### Service keeps sleeping
- Verify UptimeRobot is pinging your URL
- Check that monitor status is "Up" in UptimeRobot
- Ensure URL in UptimeRobot matches your Render URL

### First response is slow
- Normal for free tier (cold start ~30 seconds)
- UptimeRobot keeps it warm after first ping
- Users won't notice delays once warmed up

## Documentation

- 📘 [DEPLOY.md](DEPLOY.md) - Step-by-step deployment guide
- 🔄 [UPTIMEROBOT_SETUP.md](UPTIMEROBOT_SETUP.md) - Keep bot online 24/7

## Support

For issues or questions:
- Check Render documentation
- Review Telegram Bot API docs
- Consult UptimeRobot guides

---

**Made with ❤️ | Running 24/7 for FREE! 🚀**
