# 📰 NewsFlow-AI · n8n Template

**NewsFlow-AI** is an automated news aggregation system built with [n8n](https://n8n.io). It collects news from RSS feeds and public APIs (GNews, NewsAPI), processes and summarizes it using AI, and publishes the result to a Telegram channel in a clean, readable format.

## 🚀 Features

- Fetches news from popular sources (e.g. KrebsOnSecurity, SecurityLab, TheHackerNews, and others)
- Supports GNews and NewsAPI via HTTP requests
- Merges, filters, sorts, and transforms news data
- Edits and restructures content via LLM (OpenRouter integration)
- Automatically posts both images and formatted text to Telegram  
  *(image hosted on [postimages.org](https://postimages.org/))*
- Scheduled publication (e.g. at 9:00 and 21:00)

---

## 🛠️ Requirements

- A running [n8n](https://docs.n8n.io/) instance (self-hosted or cloud)
- Telegram account + bot with API token
- API keys for:
  - [GNews API](https://gnews.io/)
  - [NewsAPI](https://newsapi.org/)
  - [OpenRouter (for LLM)](https://openrouter.ai/)
- A public image URL (e.g. hosted via [postimg.cc](https://postimg.cc/))

---

## 📦 Setup

1. Download the file `NewsFlow-AI-v1.json`.

2. In n8n:

   - Go to the **Workflows** section
   - Click `Import`
   - Upload the `template.txt` file from this repository

3. Edit the following nodes:

   - 🟡 `Fetch GNews articles` and `Fetch NewsAPI articles`:  
     Insert your personal API keys

   - 🔵 Telegram nodes (`SendSummaryTtoTelegram`, `Send summary to Telegram`, etc.):  
     Set your `chatId` and ensure the bot is added to the channel with admin rights  
     How to get `chatId`:  
     [https://api.telegram.org/bot<YOUR_BOT_TOKEN>/getChat?chat_id=<CHAT_ID>](https://api.telegram.org/bot<YOUR_BOT_TOKEN>/getChat?chat_id=@yourchannel)

   - 🧠 AI nodes (`OpenRouter ChatModel`, `RSS`, `API`):  
     Make sure your OpenRouter endpoint is active and responding

4. Review the scheduled triggers:  
   These define when the news is published:
   - `9AM AND 9PM` — triggers the RSS workflow
   - `10AM AND 10PM` — triggers API-based news collection

5. Enable the workflow by toggling the “Active” switch (top right corner)

---

## ⚙️ Workflow Logic

### 🧩 Data Sources:

- RSS feeds: `krebsonsecurity`, `securitylab`, `feeds.feedburner`
- APIs: `Fetch GNews articles`, `Fetch NewsAPI articles`

### 🛠️ Data Processing:

- `Merge`, `Set`, `Filter by date`, `Sort by date` — parsing and filtering
- `Transform new to MD` — Markdown formatting
- `RSS` / `API` nodes — AI-based news summarization for Telegram

### 🤖 AI Integration:

- Uses OpenRouter via `lmChatOpenRouter`
- The LLM creates a concise list of headlines and links (max 1000 characters total)

### 📤 Telegram Posting:

- `SendSummaryTtoTelegram`, `Send summary to Telegram`, `SendPhoto` — send formatted text and preview image to the Telegram channel

---

## 💡 Sample Output

```

🧠 VeilStack AI NEWS
• [CISA orders urgent SharePoint patch](https://thehackernews.com/...)
• [Europol arrests XSS forum admin after 12 years](https://thehackernews.com/...)
• [US sanctions North Korean IT firm](https://thehackernews.com/...)

```

---

## 📎 Useful Links

- [n8n Documentation](https://docs.n8n.io/)
- [Telegram Bot API](https://core.telegram.org/bots/api)
- [GNews.io](https://gnews.io/)
- [NewsAPI.org](https://newsapi.org/)
- [OpenRouter.ai](https://openrouter.ai/)

---

## 📬 Feedback & Support

If you have questions or suggestions, feel free to contact us on Telegram:  
👉 [https://t.me/veilstack](https://t.me/veilstack)  
You can also open an Issue or submit a Pull Request on GitHub.

---

## 🧠 License

MIT License — free to use, modify, and distribute with attribution.
