# YNC Assistant - Quick Troubleshooting

## Bot Not Responding? Check These 5 Things

### 1. Check Railway Logs
- Go to Railway → Your Project → Select the service
- Click the **"Logs"** tab
- Look for:
  - ✅ `"VENICE_API_KEY loaded: True"` - Key is there
  - ✅ `"TELEGRAM_BOT_TOKEN loaded: True"` - Token is there
  - ❌ If you see `False` - variable name is wrong

### 2. Check Variable Names in Railway
In Railway → Variables tab, make sure you have:

| Variable Name (EXACT) | Value |
|----------------------|-------|
| `TELEGRAM_BOT_TOKEN` | Your BotFather token |
| `VENCE_API_KEY` | `VENICE_INFERENCE_KEY_xxxxx...` |
| `OWNER_USER_ID` | Your Telegram user ID |

**Common mistake:** `VENCE_API_KEY` vs `VENICE_API_KEY` - use **VENCE_API_KEY** (5 letters)

### 3. Check for "Conflict" Error
- Error: `Conflict: terminated by other getUpdates request`
- **Fix:** In Railway, Variables → Add a space to any variable → Save
- This forces a new deployment and kills the old instance

### 4. Check Venice API Response
- In Railway Logs, look for: `Venice API response: 200`
- If you see `401` - Your Venice key is wrong/expired
- If you see `429` - You hit rate limit (wait 5 min)
- If you see `500` - Venice API is down (try again later)

### 5. Test /reset First
- Sometimes old conversation history is corrupted
- Send `/reset` in Telegram before asking questions

---

## What You Should See in Logs (Happy Path)

```
INFO: VENICE_API_KEY loaded: True
INFO: TELEGRAM_BOT_TOKEN loaded: True
INFO: Calling Venice AI for chat_id: 123456789
INFO: Venice API response: 200
INFO: Got reply from Venice AI: Cpn take a lil time to build to hit banks...
```

---

## Still Not Working?

1. **Push fresh code to GitHub** - Drag all files again
2. **Delete old deployment in Railway** - Settings → Terminate Deployment
3. **Add a space to VENCE_API_KEY** - Forces new deployment
4. **Wait 2 minutes** - Give Railway time to fully start
5. **Test again** - Send `/reset` first

---

## Debugging Tips

- Check Railway Events tab for deployment status
- Check Railway Variables - no trailing spaces!
- Test your Venice key at: https://api.venice.ai/docs (if they have a playground)
- Check Telegram BotFather - make sure bot is active