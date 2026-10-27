Extract historical creator timeline posts (`user_posts`) and detailed KOL account profiles (`user_profile`) from **Sina Weibo (新浪微博)** — **with 100% ZERO cookies or personal login required**.

# Weibo User Posts & KOL Profile Scraper (微博博主主页采集 — 100% No Cookie)

> 🚀 **Run Directly on Apify Cloud (Zero Login, No Personal Cookies Needed):**
> 👉 **[Launch Weibo User Posts & Profile Scraper on Apify Store](https://apify.com/axon-studio/weibo-user-posts-scraper)**

Built for **KOL influencer marketing due diligence, official brand account tracking, executive & celebrity monitoring, and AI/LLM corpus collection** (n8n, Make, Dify, Claude MCP). While traditional Weibo scrapers fail on creator timelines unless you supply your own personal `cookieString`, this Actor uses a **built-in managed session pool + PC/Mobile dual-engine fallback** on just **256 MB RAM**. Users on the **Apify Free plan ($5 monthly credit) can extract up to 1,111 Weibo creator posts or profiles per month for free**.

---

## What Can This Weibo User Posts & Profile Scraper Do? (Features)

| Weibo Creator Scraper Capability | Built-In Advantage |
| :--- | :--- |
| **100% Cookie-Free `user_posts` Extraction** | Extracts a creator's historical Weibo posts by numeric UID or profile URL via our managed session pool and dual PC (`/ajax/statuses/mymblog`) + Mobile (`containerid=107603`) fallback. |
| **Comprehensive `user_profile` Due Diligence** | Extracts follower count (`authorFollowers`), following count (`authorFollowing`), total lifetime posts (`statusesCount`), verification badge & reason (`authorVerifiedReason`), bio, and location. |
| **Full Text Expansion (`>140` chars)** | Automatically expands truncated long timeline posts (`...全文`) so you always receive the complete post body. |
| **Cascade Comment Harvesting (`scrapeComments`)** | Optionally extract top reader comments under every timeline post in the same run (with commenter IP province mapping). |
| **Date Window Filtering (`dateStart` / `dateEnd`)** | Filter a creator's timeline to a specific campaign period (`YYYY-MM-DD`); posts outside your window are dropped before delivery and never billed. |
| **Built-In Sentiment & Geolocation (`regionEn`)** | Tags every post with `sentiment` (`positive` / `negative` / `neutral`), `sentimentScore`, and standardized English IP province (`Guangdong`, `Beijing`, `Shanghai`). |

---

## How to Scrape Weibo User Posts & Profiles in 3 Easy Steps

1. **Select a `mode`** — Choose **`user_posts`** (to extract a creator's historical posts) or **`user_profile`** (to extract account follower and verification metrics).
2. **Paste Target UIDs or URLs (`userIds`)** — Enter one or more Weibo numeric UIDs (e.g., `1749127163`) or full profile URLs (`https://weibo.com/u/1749127163`).
3. **Click "Start"** — Download your creator data in **JSON, CSV, Excel, or Parquet**, or connect via REST API, n8n, Make, or Claude MCP.

---

## Weibo User Posts & Profile Scraper Use Cases

| Buyer Profile | Weibo Creator & KOL Intelligence Use Case |
| :--- | :--- |
| **Influencer & KOL Marketing Agencies** | Vet Weibo influencers by follower count, verification status (`黄V` / `蓝V`), historical post engagement (`attitudesCount`, `commentsCount`, `repostsCount`), and audience sentiment |
| **Competitive Intelligence & Brand Teams** | Monitor competitor official Weibo accounts (`官微`) for product launches, promotional campaigns, and announcement cadence |
| **Hedge Funds & Equity Analysts** | Track executive accounts (e.g., Lei Jun / Xiaomi, CEOs of Chinese EV & tech companies) and official corporate announcements in real time |
| **AI / LLM & Media Research Teams** | Build author-attributed Chinese social media corpora and track public figure discourse across provinces |

---

## Input

All parameters are documented in the **Input** tab. Below are the core fields and JSON input examples:

| Input Field | Type | Description |
| :--- | :--- | :--- |
| **`mode`** | `string` | `"user_posts"` (creator timeline posts) or `"user_profile"` (one profile summary row per UID). Default: `"user_posts"`. |
| **`userIds`** | `array` | List of Weibo numeric UIDs (`"1749127163"`) or profile URLs (`"https://weibo.com/u/1749127163"`). Duplicate UIDs are automatically deduplicated. |
| **`maxResults`** | `integer` | Maximum number of primary posts or profiles to return (`1` to `5,000`, default: `50`). |
| **`dateStart` / `dateEnd`** | `string` | Optional `YYYY-MM-DD` date window filter for `user_posts`. |
| **`fullText`** | `boolean` | Expands truncated long posts (`>140` chars, default: `true`). |
| **`sentimentAnalysis`** | `boolean` | Tags every post and comment with `sentiment` and `sentimentScore` (default: `true`). |
| **`scrapeComments`** | `boolean` | Cascade add-on: extracts up to `maxCommentsPerPost` comments under each creator post (billed as 1 item per comment row). |
| **`includeAuthorProfiles`** | `boolean` | Cascade add-on: emits a dedicated `user_profile` row alongside `user_posts` (billed as 1 item per unique creator). |
| **`deltaMode`** | `boolean` | Skips previously scraped post IDs across scheduled runs so you only pay for new posts. |

### 1. Scrape a Creator's Timeline Posts + Full Text (`user_posts`)
```json
{
  "mode": "user_posts",
  "userIds": [
    "1749127163",
    "https://weibo.com/u/1642634100"
  ],
  "dateStart": "2026-09-01",
  "maxResults": 100,
  "fullText": true,
  "sentimentAnalysis": true,
  "scrapeComments": false
}
```

### 2. Batch Extract KOL Account Profiles (`user_profile`)
```json
{
  "mode": "user_profile",
  "userIds": [
    "1749127163",
    "1642634100"
  ],
  "maxResults": 20
}
```

---

## Output

Below are the structured JSON outputs matching the `"1749127163"` (Lei Jun / 雷军) input examples above:

### 1. Creator Timeline Post Row (`mode: "user_posts"`)
```json
{
  "postId": "5356651029184421",
  "mblogid": "RnLKq8wB2",
  "mode": "user_posts",
  "text": "今天很高兴跟大家分享小米SU7最新的交付进展，感谢每一位车主朋友的信任与支持！",
  "sentiment": "positive",
  "sentimentScore": 0.85,
  "createdAt": "Fri Oct 24 10:15:00 +0800 2026",
  "createdAtIso": "2026-10-24T10:15:00+08:00",
  "authorId": "1749127163",
  "authorName": "雷军",
  "authorAvatar": "https://tvax4.sinaimg.cn/crop.0.0.1080.1080.180/...",
  "authorVerified": true,
  "authorVerifiedReason": "小米集团创始人、董事长兼CEO",
  "authorFollowers": 25180000,
  "attitudesCount": 45210,
  "commentsCount": 6890,
  "repostsCount": 3120,
  "regionName": "北京",
  "regionEn": "Beijing",
  "images": ["https://wx1.sinaimg.cn/large/..."],
  "isPromoted": false,
  "isRepost": false,
  "postUrl": "https://weibo.com/1749127163/RnLKq8wB2",
  "scrapedAt": "2026-10-24 16:40:12 UTC"
}
```

### 2. Creator Profile Row (`mode: "user_profile"`)
```json
{
  "mode": "user_profile",
  "authorId": "1749127163",
  "authorName": "雷军",
  "text": "雷军 - 小米集团创始人、董事长兼CEO",
  "sentiment": "neutral",
  "sentimentScore": 0.0,
  "authorAvatar": "https://tvax4.sinaimg.cn/crop.0.0.1080.1080.180/...",
  "authorVerified": true,
  "authorVerifiedReason": "小米集团创始人、董事长兼CEO",
  "authorFollowers": 25180000,
  "authorFollowing": 1390,
  "statusesCount": 16420,
  "authorDescription": "小米集团创始人、董事长兼CEO",
  "location": "北京",
  "regionEn": "Beijing",
  "scrapedAt": "2026-10-24 16:40:15 UTC"
}
```

---

## Automated Daily KOL & Competitor Monitoring (Schedules & Delta Mode)

Track when a list of Weibo creators publishes new posts automatically:
1. Go to **Apify Console → Schedules → Create new schedule** and select **`axon-studio/weibo-user-posts-scraper`**.
2. Set **`deltaMode: true`** in your input JSON. The Actor remembers up to 10,000 previously scraped post IDs in your Key-Value Store (`DELTA_SEEN_IDS`) and skips old posts on future runs—so you are only billed when a creator publishes a brand-new post.

### Python & Synchronous REST API Integration

```python
from apify_client import ApifyClient

client = ApifyClient("YOUR_APIFY_API_TOKEN")
run = client.actor("axon-studio/weibo-user-posts-scraper").call(run_input={
    "mode": "user_posts",
    "userIds": ["1749127163"],
    "maxResults": 50,
    "fullText": True,
})
for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item["postId"], item["authorName"], item["createdAtIso"], item["text"][:60])
```

```bash
curl -X POST "https://api.apify.com/v2/acts/axon-studio~weibo-user-posts-scraper/run-sync-get-dataset-items?token=YOUR_APIFY_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"mode":"user_posts","userIds":["1749127163"],"maxResults":25}'
```

---

## How Much Does It Cost to Scrape Weibo User Posts? (Pricing)

**$4.50 per 1,000 results (`$0.0045` per post or profile) + `$0.02` per Actor start (Pay-Per-Event)**

* **Free Plan Credits**: Every Apify account receives **$5.00 in free monthly credits**, covering up to **1,111 Weibo creator posts or profiles every month for free**.
* **Volume Discounts**: Automatic lower unit prices for Apify **Bronze / Starter**, **Silver / Scale**, and **Gold / Business** subscribers.
* **No Server Compute Fees**: Runs on just 256 MB RAM with platform usage fully included.
* **Typical Run Costs**: 50 KOL profiles (`user_profile`) = **`$0.245`** · 100 creator timeline posts (`user_posts`) = **`$0.47`** · 1,000 creator posts = **`$4.52`**.

---

## FAQ & Legal Compliance

### Why doesn't this scraper require my personal Weibo `cookieString` for `user_posts`?
We maintain a built-in managed cloud session pool paired with automatic PC Ajax and Mobile H5 (`containerid=107603`) fallback. You never have to extract or risk your own Weibo account cookies.

### Is it legal to scrape public Weibo creator timelines and profiles?
This Actor reads publicly visible Weibo profiles and timelines and cannot access private or locked posts. Public screen names, UIDs, bios, and IP province tags may constitute personal data under **GDPR** or **PIPL**; ensure you have a lawful basis for processing public social data. *Not affiliated with Sina Corporation or Weibo.*

---

## More Chinese Social Intelligence Scrapers by Axon Studio

* **[Weibo Scraper — All-in-One Search, Hot Trends, Comments & BlackCat](https://apify.com/axon-studio/weibo-scraper)** — 9-mode comprehensive Sina Weibo & BlackCat intelligence suite.
* **[BlackCat Scraper 黑猫投诉 — China Consumer Complaints API](https://apify.com/axon-studio/blackcat-scraper)** — Extract consumer disputes and brand complaints from `tousu.sina.com.cn`.
* **[Weibo Comments & Province Geolocation Scraper](https://apify.com/axon-studio/weibo-comments-scraper)** — Extract reader comment threads and English IP province locations (`regionEn`).
