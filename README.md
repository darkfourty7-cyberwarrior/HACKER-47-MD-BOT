# HACKER 47 — WhatsApp MD Bot

A self-hosted WhatsApp multi-device bot with a Railway web dashboard and phone-number pairing flow.

## Deploy your own copy

1. Create a new **empty GitHub repository** named `HACKER-47-MD-BOT`.
2. Upload the contents of this project (the files inside this folder, not the outer ZIP folder) to the repository.
3. In Railway, create a project → **Deploy from GitHub Repo** → select your repository.
4. Add the variables below in Railway → Service → Variables.
5. Deploy. Open the generated Railway domain to view the pairing dashboard.

## Required Railway variables

| Variable | Value |
|---|---|
| `PHONE_NUMBER` | `923359095714` (digits only; change if needed) |
| `MONGODB_URI` | Your MongoDB Atlas connection URI |
| `DB_NAME` | `hacker47_bot` |
| `BOTNAME` | `HACKER 47` |
| `OWNERS` | `923359095714;HACKER 47` |
| `PORT` | Railway supplies this automatically; do not hardcode it |

**MongoDB is required.** Create a free MongoDB Atlas cluster, create a database user, allow Railway's outbound IP access (or use Atlas's documented network access option), and paste the connection string into `MONGODB_URI`. Replace the username/password placeholders. Never commit `.env` or publish database credentials.

## Pair WhatsApp

Open the Railway public domain. The dashboard displays the pairing code after the bot requests it. On the WhatsApp account for `PHONE_NUMBER`, go to **Linked devices → Link a device → Link with phone number instead**, then enter the displayed code. Keep the number in international format without `+`, spaces, or punctuation.

## API endpoints

- `GET /` — HACKER 47 pairing dashboard
- `GET /pairing-status` — JSON pairing code, connection state, and available stats
- `GET /bot-stats` — bot statistics (returns HTTP 503 until available)

## Local development

```bash
npm install
cp .env.example .env
# Fill in MONGODB_URI before starting
npm start
```

Node.js 20 or newer is recommended. The project installs `jimp` directly because the selected `baileys-pro` build imports it for media utilities.
