# rss-dreamteam

## RSS Discord Webhook Bot

An automated bot that monitors RSS feeds and pushes new articles to Discord channels with multi-channel support.

## Key Features

- **Multi-Channel Routing**: Send feeds to different Discord channels
- **Multi-Feed Tracking**: Monitor unlimited RSS feeds (`feeds.json`)
- **Duplicate Prevention**: Persistent memory of processed articles (`last_posts.json`)
- **Scheduled Updates**: Configurable check frequency via GitHub Actions
- **Clean Formatting**: Optimized Discord message display

## Quick Start

1. **Clone the repository**:

   bash

   Copier

   ```
   git clone https://github.com/Gabryel666/rss-dreamteam.git
   cd rss-dreamteam
   ```

2. **Configure feeds**:
    Edit `feeds.json` with channel routing:

   json

   Copier

   ```
   {
     "Hugin & Munin": {
       "url": "https://example.com/feed.rss",
       "webhookKey": "news"
     },
     "Le Grog": {
       "url": "https://www.legrog.org/rss",
       "webhookKey": "gaming"
     }
   }
   ```

3. **Set up Discord webhooks**:

   - Create webhooks for each channel in Discord settings

   - Add them to GitHub Secrets as JSON:

     json

     Copier

     ```
     {
       "news": "https://discord.com/api/webhooks/...",
       "gaming": "https://discord.com/api/webhooks/..."
     }
     ```

   - Secret name: `DISCORD_WEBHOOKS`

## Technical Overview

mermaid

Copier

```
sequenceDiagram
    GitHub Actions->>+Script: Scheduled trigger
    Script->>+RSS Feeds: Fetch updates
    RSS Feeds-->>-Script: New articles
    Script->>+Discord: Route to appropriate channel
    Script->>GitHub: Update tracking database
```

## File Structure

Copier

```
.
├── .github/
│   └── workflows/
│       └── rss-check.yml    # Automation config
├── feeds.json               # Feed list with channel routing
├── last_posts.json          # Processed articles (auto-generated)
└── main.js                  # Core processing script
```

## Customization

### Change Check Frequency

Edit `.github/workflows/rss-check.yml`:

yaml

Copier

```
- cron: '*/30 * * * *'  # Every 30 minutes
```

### Available Intervals:

- `'*/15 * * * *'` - Every 15 minutes
- `'0 * * * *'` - Hourly
- `'0 0 * * *'` - Daily

## Release Notes

### v2.0 - Multi-Channel Support

- **New Feature**: Route feeds to different Discord channels

- Improved Configuration  :
  - Structured `feeds.json` with channel mapping
  - Single JSON secret for all webhooks

- Enhanced Error Handling  :
  - Better validation of webhook configuration
  - Detailed error logging

## 📄 License

MIT © [Gabryel666] - Free for use and modification
