# openclaw-trakt

🎬 Trakt.tv integration skill for OpenClaw - Track and recommend TV shows and movies

## Overview

This OpenClaw skill integrates with [Trakt.tv](https://trakt.tv) to provide:

- 📺 **Personalized recommendations** based on your watch history
- 📊 **Watch history tracking** (synced automatically with Trakt Pro)
- 📝 **Watchlist management** 
- 🔍 **Search** for shows and movies
- 📈 **Trending content** discovery

## Features

- ✅ Simple PIN-based authentication
- ✅ Native Trakt recommendation API
- ✅ Access to watch history, watchlist, and trending content
- ✅ Full search functionality
- ✅ Automatic token storage and refresh
- ✅ CLI interface for testing

## Installation

### 1. Install Dependencies

```bash
pip3 install requests --break-system-packages

# OR use a virtual environment (recommended)
python3 -m venv ~/.openclaw-venv
source ~/.openclaw-venv/bin/activate
pip install requests
```

### 2. Create Trakt Application

1. Go to <https://trakt.tv/oauth/applications>
2. Click "New Application"
3. Fill in:
   - **Name:** OpenClaw Assistant
   - **Redirect URI:** `urn:ietf:wg:oauth:2.0:oob`
4. Save and copy your **Client ID** and **Client Secret**

### 3. Set Environment Variables

```bash
export TRAKT_CLIENT_ID="your_client_id_here"
export TRAKT_CLIENT_SECRET="your_client_secret_here"
```

Add to your shell profile (`~/.zshrc`, `~/.bashrc`) to persist.

### 4. Authenticate

```bash
# Get PIN URL
python3 scripts/trakt_client.py auth

# Visit the URL, authorize, copy PIN, then:
python3 scripts/trakt_client.py auth <YOUR_PIN>
```

Authentication tokens are saved to `~/.openclaw/trakt_auth.json`

## Usage

### Get Recommendations
```bash
python3 scripts/trakt_client.py recommend
```

### Watch History
```bash
python3 scripts/trakt_client.py history
```

### Watchlist
```bash
python3 scripts/trakt_client.py watchlist
```

### Search
```bash
python3 scripts/trakt_client.py search "Breaking Bad"
```

### Trending
```bash
python3 scripts/trakt_client.py trending
```

## How OpenClaw Uses It

When you ask your OpenClaw assistant:

- **"What should I watch?"** → Runs `recommend` command
- **"What have I been watching?"** → Runs `history` command
- **"What's trending?"** → Runs `trending` command
- **"Search for Breaking Bad"** → Runs `search` command

The skill automatically triggers when Trakt-related queries are detected.

## Skill Structure

```
openclaw-trakt/
├── SKILL.md              # OpenClaw skill documentation
├── scripts/
│   └── trakt_client.py   # Full Trakt API client
├── references/
│   └── api.md            # Trakt API reference
└── requirements.txt      # Python dependencies
```

## Requirements

- Python 3.7+
- `requests` library
- Trakt.tv account (Pro subscription recommended for auto-tracking)
- Trakt API application credentials

## API Reference

See [references/api.md](references/api.md) for detailed Trakt API endpoint documentation.

## Troubleshooting

### "Module 'requests' not found"
```bash
pip3 install requests --break-system-packages
```

### "Authentication failed"
- Double-check `TRAKT_CLIENT_ID` and `TRAKT_CLIENT_SECRET`
- Ensure PIN is copied exactly (case-sensitive)
- Verify your Trakt application has proper permissions

### "No recommendations"
- You need watch history on Trakt first
- Trakt Pro subscription required for auto-tracking
- Try rating some shows on Trakt to improve recommendations

## Technical Details

- **Auth Method:** PIN-based OAuth
- **API Version:** Trakt API v2
- **Storage:** `~/.openclaw/trakt_auth.json`
- **Rate Limits:** 1000 requests per 5 minutes (authenticated)

## Links

- 🌐 [Trakt.tv](https://trakt.tv)
- 📚 [API Documentation](https://trakt.docs.apiary.io)
- 🔑 [Create App](https://trakt.tv/oauth/applications)
- 🦞 [OpenClaw](https://openclaw.ai)

## License

MIT

---

Built for OpenClaw | February 2026
