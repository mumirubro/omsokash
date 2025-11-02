# Deploy to Render - Complete Guide for 24/7 Uptime

This guide shows you how to deploy your Telegram bot to Render as a **Web Service** and keep it running 24/7 using UptimeRobot - all for FREE!

## Why Web Service (Not Background Worker)?

Render's free **Background Workers** sleep after 15 minutes. By using a **Web Service** instead, we can:
- Keep the bot awake with UptimeRobot pings
- Run 24/7 on free tier
- Still have full bot functionality

## Step 1: Upload to GitHub

### Create GitHub Repository

1. Go to https://github.com/new
2. Name your repository (e.g., "telegram-shopify-bot")
3. Choose "Public" or "Private"
4. **DO NOT** initialize with README (we already have one)
5. Click "Create repository"

### Push Your Code

Open your terminal and run these commands:

```bash
git init
git add .
git commit -m "Ready for Render deployment - Web Service with 24/7 uptime"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
git push -u origin main
```

Replace `YOUR_USERNAME` and `YOUR_REPO_NAME` with your actual values.

## Step 2: Deploy on Render

### Create Render Account

1. Go to https://render.com
2. Click "Get Started" or "Sign Up"
3. **Sign up with GitHub** (recommended - easier integration)
4. Authorize Render to access your repositories

### Deploy Web Service

1. **Click "New +" button** (top right)
2. Select **"Web Service"** (NOT Background Worker!)
3. Click "Connect" next to your GitHub account (if needed)
4. Find and select your repository

### Configure Service

Fill in these fields:

**📋 Basic Settings:**

| Field | Value |
|-------|-------|
| **Name** | `telegram-shopify-bot` (or your choice) |
| **Language** | Python 3 |
| **Branch** | main |
| **Region** | Oregon (US West) or any region you prefer |
| **Root Directory** | Leave empty |

**⚙️ Build & Deploy:**

| Field | Value |
|-------|-------|
| **Build Command** | `pip install -r requirements.txt` |
| **Start Command** | `python main.py` |

**💰 Instance Type:**

- Select **"Free"** (perfect for testing and 24/7 operation)

**🔐 Environment Variables:**

Click "Add Environment Variable" and add:

| Key | Value |
|-----|-------|
| `TELEGRAM_BOT_TOKEN` | Your bot token from BotFather |

To get your bot token, see "Step 3" below.

**🚀 Deploy:**

Click **"Create Web Service"** button at the bottom.

## Step 3: Get Telegram Bot Token (If Needed)

If you don't have a bot token yet:

1. Open Telegram
2. Search for `@BotFather`
3. Send `/newbot` command
4. Follow the prompts:
   - Choose a name for your bot (e.g., "My Shopify Checker")
   - Choose a username (must end with 'bot', e.g., "myshopify_checker_bot")
5. **Copy the token** (looks like: `123456789:ABCdefGHIjklMNOpqrsTUVwxyz`)
6. Add this token to Render's environment variables

## Step 4: Wait for Deployment

### Deployment Progress

Render will now:
1. ✅ Clone your GitHub repository
2. ✅ Install Python 3.11
3. ✅ Install dependencies from requirements.txt
4. ✅ Start your bot with `python main.py`

This takes **2-5 minutes**.

### Check Deployment Status

Watch the deployment logs in real-time:
- You'll see installation progress
- Look for: `🚀 Starting Telegram Bot with Web Server...`
- Then: `🌐 Starting web server on port 5000...`
- And: `🤖 TOJI CHK Bot Starting...`
- Finally: `✅ Bot is running! Send /start to your bot to begin.`

### Get Your Service URL

Once deployed, Render gives you a URL like:
```
https://telegram-shopify-bot-abc123.onrender.com
```

**Copy this URL** - you'll need it for UptimeRobot!

## Step 5: Test Your Bot

1. Open Telegram
2. Search for your bot by username
3. Send `/start` command
4. **You should see the bot menu!** ✅

If the bot responds, deployment was successful!

## Step 6: Set Up 24/7 Uptime with UptimeRobot

**This is the crucial step to keep your bot online 24/7!**

### Why UptimeRobot?

Render's free tier sleeps after 15 minutes of inactivity. UptimeRobot pings your service every 5 minutes, keeping it awake continuously.

### Create UptimeRobot Account

1. Go to https://uptimerobot.com/
2. Click **"Sign Up Free"**
3. Enter email and create password
4. Verify your email

### Add Monitor

1. **Login to UptimeRobot dashboard**
2. Click **"+ Add New Monitor"** button
3. Fill in the form:

**Monitor Settings:**

| Field | Value |
|-------|-------|
| **Monitor Type** | HTTP(s) |
| **Friendly Name** | `Telegram Shopify Bot` |
| **URL (or IP)** | `https://your-app.onrender.com` |
| **Monitoring Interval** | 5 minutes |

Replace `https://your-app.onrender.com` with your actual Render URL from Step 4.

4. Click **"Create Monitor"**

### Verify UptimeRobot is Working

1. Wait 5-10 minutes
2. Check UptimeRobot dashboard:
   - **Status:** Should show "Up" (green)
   - **Response Time:** Usually 200-1000ms
   - **Uptime %:** Should be close to 100%

3. Open your Render URL in browser:
   - You should see: **"🤖 Telegram Bot is Running! ✅"**

### You're Done! 🎉

Your bot is now:
- ✅ Deployed on Render
- ✅ Running 24/7 on free tier
- ✅ Kept awake by UptimeRobot
- ✅ Ready for users!

## Step 7: Set Up Alerts (Optional but Recommended)

Get notified if your bot goes down:

1. In UptimeRobot, click your monitor
2. Go to **"Alert Contacts"** section
3. Add your email or SMS number
4. Enable alerts
5. Click "Save"

Now you'll get instant notifications if something goes wrong!

## What to Fill in Render (Quick Reference)

When you see the Render configuration screen, here's exactly what to enter:

**Choose "Web Service"** (not Background Worker!)

```
Name: telegram-shopify-bot
Language: Python 3
Branch: main
Region: Oregon (US West)
Build Command: pip install -r requirements.txt
Start Command: python main.py
Instance Type: Free

Environment Variables:
  TELEGRAM_BOT_TOKEN = <your token from BotFather>
```

## Troubleshooting

### "TELEGRAM_BOT_TOKEN not found" error
**Problem:** Environment variable not set
- Go to Render dashboard → Your service → Environment
- Add `TELEGRAM_BOT_TOKEN` with your bot token
- Click "Save Changes"
- Service will auto-redeploy

### Bot doesn't respond after deployment
**Problem:** Check the logs
1. Go to Render dashboard
2. Click your service
3. Click "Logs" tab
4. Look for errors in red

Common issues:
- Token is incorrect → Get new token from BotFather
- Dependencies failed to install → Check requirements.txt
- Port 5000 not accessible → Render handles this automatically

### Service keeps sleeping even with UptimeRobot
**Problem:** Monitor not configured correctly
- Verify URL in UptimeRobot matches Render URL exactly
- Make sure interval is set to 5 minutes (not higher)
- Check monitor status is "Up" and green

### "Service Unavailable" when accessing URL
**Problem:** Service might be starting (cold start)
- Wait 30-60 seconds and refresh
- This is normal for free tier after inactivity
- Once UptimeRobot starts pinging, this won't happen

### Response time is very slow
**Problem:** Normal for free tier cold starts
- First request after sleep: 20-30 seconds
- Subsequent requests: Very fast
- UptimeRobot keeps it warm, users won't notice

## Updating Your Bot

When you make changes to your code:

1. **Push to GitHub:**
   ```bash
   git add .
   git commit -m "Your update message"
   git push
   ```

2. **Automatic Deploy:**
   - Render detects the push
   - Automatically rebuilds
   - Deploys new version
   - Takes 2-5 minutes

3. **No UptimeRobot changes needed** - it keeps working!

## Cost Breakdown

| Service | Plan | Cost | What You Get |
|---------|------|------|--------------|
| **Render** | Free | $0/month | 750 hours (enough for 24/7), auto-deploy, HTTPS |
| **UptimeRobot** | Free | $0/month | 50 monitors, 5-min checks, email alerts |
| **Telegram** | Free | $0/month | Bot API, unlimited messages |
| **GitHub** | Free | $0/month | Code hosting, version control |
| **TOTAL** | - | **$0/month** | **Complete 24/7 bot!** ✅ |

## Architecture Diagram

```
┌──────────────────────────────────────────┐
│           Your GitHub Repo               │
│   (Code updates trigger auto-deploy)     │
└──────────────┬───────────────────────────┘
               │ Auto-deploy on push
               ▼
┌──────────────────────────────────────────┐
│         Render Web Service (Free)        │
│  ┌────────────────────────────────────┐  │
│  │  Flask Web Server (Port 5000)      │  │
│  │  - GET / → "Bot is Running!"       │  │
│  │  - GET /health → JSON status       │  │
│  └────────────────────────────────────┘  │
│  ┌────────────────────────────────────┐  │
│  │  Telegram Bot (Background Thread)  │  │
│  │  - Polls Telegram for messages     │  │
│  │  - Responds to commands            │  │
│  └────────────────────────────────────┘  │
└──────────────┬───────────────────────────┘
               │
               ▼
┌──────────────────────────────────────────┐
│       UptimeRobot Monitor (Free)         │
│  Pings https://your-app.onrender.com     │
│  Every 5 minutes → Keeps service awake   │
└──────────────────────────────────────────┘
               │
               ▼
        [Your Bot Users]
    Use bot 24/7 on Telegram!
```

## Need More Help?

- 📘 Full UptimeRobot guide: See [UPTIMEROBOT_SETUP.md](UPTIMEROBOT_SETUP.md)
- 📖 Project README: [README.md](README.md)
- 🔧 Render Docs: https://render.com/docs
- 🤖 Telegram Bot API: https://core.telegram.org/bots/api

---

**Congratulations! Your bot is now running 24/7 on the free tier! 🎉🚀**
