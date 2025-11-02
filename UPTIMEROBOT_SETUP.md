# Keep Your Bot Online 24/7 with UptimeRobot (Free!)

Your bot is now set up as a **Web Service** on Render's free tier. By default, free services sleep after 15 minutes of inactivity. This guide shows you how to keep it awake 24/7 using UptimeRobot's free monitoring service.

## How It Works

1. Your bot runs as a web service on Render (listening on port 5000)
2. UptimeRobot pings your web URL every 5 minutes
3. This keeps your bot awake and running continuously
4. Everything stays within free tier limits! ✅

## Step 1: Deploy to Render First

Make sure you've already deployed your bot to Render as a **Web Service** (not Background Worker). If not, follow the DEPLOY.md guide first.

Once deployed, you'll have a URL like:
```
https://your-app-name.onrender.com
```

## Step 2: Set Up UptimeRobot

### Create an Account

1. Go to https://uptimerobot.com/
2. Click **"Sign Up Free"**
3. Enter your email and create a password
4. Verify your email address

### Add Your Bot as a Monitor

1. **Login to UptimeRobot Dashboard**
2. Click **"+ Add New Monitor"** button
3. Fill in the details:

   **Monitor Type:** `HTTP(s)`
   
   **Friendly Name:** `Telegram Shopify Bot` (or any name you like)
   
   **URL (or IP):** `https://your-app-name.onrender.com`
   *(Replace with your actual Render URL)*
   
   **Monitoring Interval:** `5 minutes` (maximum for free tier)
   
   Leave other settings as default.

4. Click **"Create Monitor"**

### Verify It's Working

1. Wait 5 minutes
2. Check UptimeRobot dashboard - you should see:
   - Status: **Up** (green checkmark)
   - Response Time: Usually 200-500ms
   - Uptime %: Should be close to 100%

3. Test your Telegram bot:
   - Send `/start` command
   - Bot should respond immediately! ✅

## Step 3: Monitor Your Bot

### Dashboard Overview

UptimeRobot dashboard shows:
- **Status**: Whether your bot is up or down
- **Uptime %**: Reliability percentage (aim for 99%+)
- **Response Time**: How fast your server responds
- **Last Check**: When UptimeRobot last pinged your bot

### Get Alerts (Optional)

Set up email/SMS alerts when your bot goes down:

1. Click on your monitor
2. Go to **"Alert Contacts"** section
3. Add your email or phone number
4. UptimeRobot will notify you if the bot goes offline

## How Your Bot Stays Online

Your bot now has two endpoints that UptimeRobot can ping:

1. **Main Page**: `https://your-app-name.onrender.com/`
   - Returns: "🤖 Telegram Bot is Running! ✅"
   
2. **Health Check**: `https://your-app-name.onrender.com/health`
   - Returns: `{"status": "healthy", "bot": "online"}`

UptimeRobot pings one of these every 5 minutes, keeping your Render service awake.

## Free Tier Limits

### Render Free Tier:
- ✅ 750 hours/month (enough for 24/7 with one service)
- ✅ Automatic deploys from GitHub
- ✅ HTTPS support
- ⚠️ Sleeps after 15 min of inactivity (solved by UptimeRobot!)
- ⚠️ Slower cold starts (~30 seconds)

### UptimeRobot Free Tier:
- ✅ Up to 50 monitors
- ✅ 5-minute intervals
- ✅ Email alerts
- ✅ Public status pages
- ✅ Unlimited checks

## Troubleshooting

### Bot doesn't respond after 15 minutes
**Problem:** UptimeRobot might not be working
- Check UptimeRobot dashboard - is monitor status "Up"?
- Verify URL is correct (no typos)
- Make sure interval is set to 5 minutes

### UptimeRobot shows "Down"
**Problem:** Your Render service might be stopped
- Check Render dashboard - is service "Live"?
- Check logs for errors
- Try manual deploy to restart

### Bot works but UptimeRobot says "Down"
**Problem:** Wrong URL or endpoint
- Make sure you're using the HTTPS URL from Render
- Try adding `/health` to the URL in UptimeRobot
- Check if URL is accessible in your browser

### Response time is very slow (>10 seconds)
**Problem:** Render free tier has slower cold starts
- This is normal for free tier
- First request after sleep takes 20-30 seconds
- Subsequent requests are fast
- UptimeRobot keeps it warm, so users won't notice

## Advanced Tips

### Use /health endpoint
For better monitoring, use the health check endpoint:
```
https://your-app-name.onrender.com/health
```
This returns JSON and is faster to check.

### Multiple Monitors
You can create 2 monitors for redundancy:
- Monitor 1: Main page (`/`)
- Monitor 2: Health page (`/health`)

Both will keep your bot alive!

### Check Logs
If something goes wrong, check logs:
1. Go to Render Dashboard
2. Click on your service
3. Click "Logs" tab
4. Look for errors

## Cost Summary

| Service | Cost | What You Get |
|---------|------|--------------|
| Render Free | $0/month | 750 hours, auto-deploy, HTTPS |
| UptimeRobot Free | $0/month | 50 monitors, 5-min checks |
| **Total** | **$0/month** | **24/7 bot uptime!** ✅ |

## That's It! 🎉

Your Telegram bot is now running 24/7 for free! 

**What happens now:**
1. Bot runs on Render
2. UptimeRobot pings every 5 minutes
3. Render stays awake
4. Your users can use the bot anytime!

**Need help?** Check the troubleshooting section above or ask in your support channel.

---

**Pro Tip:** If you need true 24/7 with faster response times and no cold starts, consider upgrading to Render's paid plan ($7/month for Starter tier).
