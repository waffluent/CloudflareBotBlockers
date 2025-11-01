# Cloudflare Bot Blockers

This repo provides categorized **Cloudflare Custom Security Rules** for blocking unwanted User-Agents.
The lists are grouped by bot type so you can enable/disable categories without touching the rest.

---

## Why Categories?

Splitting by category improves:

* **Granularity** — selectively block AI bots but allow SEO crawlers (or vice versa).
* **Maintainability** — each category list is shorter and easier to update.
* **Performance** — avoids Cloudflare’s per-rule expression length limits.

---

## Categories

We’ve grouped UA patterns into:

1. **AI / LLM Bots** — ChatGPT, Claude, Perplexity, Meta AI, and similar.
2. **General Scrapers / Libraries** — curl, requests, okhttp, nutch, etc.
3. **Headless Browsers / Automation** — PhantomJS, HeadlessChrome.
4. **Asian & Russian Search / Regional Bots** — Baidu, Yandex, Sogou, etc. (treated as bad).
5. **SEO / Marketing / Competitive Intelligence** — SerpApi, BrandVerity, Meltwater, etc.
6. **Miscellaneous / Unclassified** — bots that don’t neatly fit elsewhere.

---

## Installation in Cloudflare

You can add each category as a separate **Custom Rule** in Cloudflare’s WAF:

1. **Log in** to Cloudflare and select your zone.
2. Go to **Security → WAF → Custom rules** and click **Create rule**.
3. For **Rule name**, use the category name, e.g., `Block AI / LLM Bots`.
4. In the **Expression Editor**, paste the corresponding expression from this README.
5. Set **Action** to `Block` (or `Managed Challenge` if you prefer softer enforcement).
6. Deploy and repeat for each category you want to enforce.

> **Tip:** For case-insensitive matching, wrap the UA in `lower(...)`, e.g.:
>
> ```
> lower(http.user_agent) contains "curl"
> ```

---

## Category Expressions

### **1. AI / LLM Bots**

```
(
    (http.user_agent contains "AI21Labs") or
    (http.user_agent contains "AI2Bot") or
    (http.user_agent contains "Anthropic") or
    (http.user_agent contains "Applebot-Extended") or
    (http.user_agent contains "Bytespider") or
    (http.user_agent contains "CCBot") or
    (http.user_agent contains "ChatGPT") or
    (http.user_agent contains "ChatGPT-User") or
    (http.user_agent contains "Claude-Web") or
    (http.user_agent contains "ClaudeBot") or
    (http.user_agent contains "Cohere") or
    (http.user_agent contains "DuckAssistBot") or
    (http.user_agent contains "GPTBot") or
    (http.user_agent contains "Google-Extended") or
    (http.user_agent contains "MistralAI-User") or
    (http.user_agent contains "MetaAI") or
    (http.user_agent contains "MetaBot") or
    (http.user_agent contains "NeevaBot") or
    (http.user_agent contains "OAI-SearchBot") or
    (http.user_agent contains "OpenAI") or
    (http.user_agent contains "PerplexityBot") or
    (http.user_agent contains "Perplexity-User") or
    (http.user_agent contains "ReplikaBot") or
    (http.user_agent contains "You.com") or
    (http.user_agent contains "xAI") or
    (http.user_agent contains "Grok") or
    (http.user_agent contains "PhindBot") or
    (http.user_agent contains "KagiBot") or
    (http.user_agent contains "BingPreview") or
    (http.user_agent contains "Copilot") or
    (http.user_agent contains "ErnieBot") or
    (http.user_agent contains "BaiduSpider") or
    (http.user_agent contains "DeepMind") or
    (http.user_agent contains "cohere-ai")
)
```

---

### **2. General Scrapers / Libraries**

```
(http.user_agent contains "Apache-HttpClient") or
(http.user_agent contains "curl") or
(http.user_agent contains "Wget") or
(http.user_agent contains "python-requests") or
(http.user_agent contains "Python-urllib") or
(http.user_agent contains "libwww-perl") or
(http.user_agent contains "httpunit") or
(http.user_agent contains "okhttp") or
(http.user_agent contains "http.rb") or
(http.user_agent contains "AHC/") or
(http.user_agent contains "Jetty/") or
(http.user_agent contains "HttpUrlConnection") or
(http.user_agent contains "axios") or
(http.user_agent contains "zgrab") or
(http.user_agent contains "crawler4j") or
(http.user_agent contains "nutch") or
(http.user_agent contains "SimpleCrawler") or
(http.user_agent contains "newspaper/") or
(http.user_agent contains "http_get") or
(http.user_agent contains "CapsuleChecker") or
(http.user_agent contains "MetaURI") or
(http.user_agent contains "cXensebot") or
(http.user_agent contains "SMTBot") or
(http.user_agent contains "Gluten Free Crawler") or
(http.user_agent contains "Sonic/") or
(http.user_agent contains "Sysomos") or
(http.user_agent contains "deadlinkchecker") or
(http.user_agent contains "check_http") or
(http.user_agent contains "BDCbot") or
(http.user_agent contains "EZID") or
(http.user_agent contains "ICC-Crawler") or
(http.user_agent contains "ArchiveBot") or
(http.user_agent contains "magpie-crawler") or
(http.user_agent contains "ScoutJet") or
(http.user_agent contains "sentry/") or
(http.user_agent contains "seoscanners") or
(http.user_agent contains "MauiBot") or
(http.user_agent contains "AlphaBot") or
(http.user_agent contains "SBL-BOT") or
(http.user_agent contains "adscanner") or
(http.user_agent contains "acapbot") or
(http.user_agent contains "Domain Re-Animator Bot") or
(http.user_agent contains "discobot") or
(http.user_agent contains "BLEXBot") or
(http.user_agent contains "ExtLinksBot") or
(http.user_agent contains "SurveyBot") or
(http.user_agent contains "Miniflux") or
(http.user_agent contains "Feedspotbot") or
(http.user_agent contains "tracemyfile") or
(http.user_agent contains "Seekport Crawler") or
(http.user_agent contains "ZoomBot") or
(http.user_agent contains "MoodleBot") or
(http.user_agent contains "jpg-newsbot/")
```

---

### **3. Headless Browsers / Automation**

```
(http.user_agent contains "PhantomJS") or
(http.user_agent contains "HeadlessChrome")
```

---

### **4. Asian & Russian Search / Regional Bots**

```
(http.user_agent contains "Baidu") or
(http.user_agent contains "Baiduspider") or
(http.user_agent contains "Baidu-YunGuanCe") or
(http.user_agent contains "YisouSpider") or
(http.user_agent contains "Sosospider") or
(http.user_agent contains "HaosouSpider") or
(http.user_agent contains "YodaoBot") or
(http.user_agent contains "ToutiaoSpider") or
(http.user_agent contains "Sogou") or
(http.user_agent contains "YandexBot") or
(http.user_agent contains "YandexWebmaster") or
(http.user_agent contains "Mail.RU_Bot") or
(http.user_agent contains "Yeti/") or
(http.user_agent contains "Daum/") or
(http.user_agent contains "coccoc") or
(http.user_agent contains "imagecoccoc") or
(http.user_agent contains "ichiro") or
(http.user_agent contains "Y!J")
```

---

### **5. SEO / Marketing / Competitive Intelligence**

```
(http.user_agent contains "AwarioBot") or
(http.user_agent contains "DataForSeoBot") or
(http.user_agent contains "Diffbot") or
(http.user_agent contains "ProRataInc") or
(http.user_agent contains "Quora Link Preview") or
(http.user_agent contains "SemanticScholarBot") or
(http.user_agent contains "SerpApi") or
(http.user_agent contains "TelegramBot") or
(http.user_agent contains "TinEye-bot") or
(http.user_agent contains "TweetmemeBot") or
(http.user_agent contains "Twitterbot") or
(http.user_agent contains "ZyteSmartProxy") or
(http.user_agent contains "archive.org_bot") or
(http.user_agent contains "meta-externalfetcher") or
(http.user_agent contains "webmeup-crawler") or
(http.user_agent contains "VelenPublicWebCrawler") or
(http.user_agent contains "Twurly") or
(http.user_agent contains "botify") or
(http.user_agent contains "BrandVerity") or
(http.user_agent contains "BLP_bbot") or
(http.user_agent contains "BomboraBot") or
(http.user_agent contains "Companybook-Crawler") or
(http.user_agent contains "Genieo") or
(http.user_agent contains "MeltwaterNews") or
(http.user_agent contains "Moreover") or
(http.user_agent contains "StorygizeBot") or
(http.user_agent contains "OutclicksBot") or
(http.user_agent contains "W3C_Validator") or
(http.user_agent contains "Validator.nu") or
(http.user_agent contains "W3C-checklink") or
(http.user_agent contains "W3C-mobileOK") or
(http.user_agent contains "W3C_I18n-Checker") or
(http.user_agent contains "FeedValidator/") or
(http.user_agent contains "W3C_CSS_Validator") or
(http.user_agent contains "W3C_Unicorn")
```

---

### **6. Miscellaneous / Unclassified**

```
(http.user_agent contains "360Spider") or
(http.user_agent contains "Amazonbot") or
(http.user_agent contains "Bytespider") or
(http.user_agent contains "Go-http-client") or
(http.user_agent contains "Java/") or
(http.user_agent contains "Node/simplecrawler") or
(http.user_agent contains "Pinterestbot") or
(http.user_agent contains "DareBoost") or
(http.user_agent contains "Datafeedwatch") or
(http.user_agent contains "WordupInfoSearch") or
(http.user_agent contains "WebDataStats") or
(http.user_agent contains "Pcore-HTTP") or
(http.user_agent contains "Upflow") or
(http.user_agent contains "Mastodon/") or
(http.user_agent contains "DnyzBot") or
(http.user_agent contains "007ac9") or
(http.user_agent contains "BehloolBot")
```

# Stealth / Impersonating AI Crawlers

These rules detect and block **stealth AI crawlers** that impersonate legitimate search engine bots (e.g., Perplexity pretending to be Googlebot) but operate from unauthorized networks.
They combine **User-Agent string checks** with **verified IP range validation** so you can block only the imposters while still allowing the real bots.

---

## ⚠️ Important Caveat

Search engine and bot providers **regularly change their IP ranges**.
You **must** keep these IP/CIDR lists up to date or you risk blocking legitimate crawlers.

### Recommended Update Frequency

* **Monthly** minimum for high-traffic sites.
* **Before major site launches** or changes to SEO strategy.
* After **receiving reports from Google Search Console** or similar tools about crawler access issues.

Reference official IP lists:

* Googlebot: [https://developers.google.com/search/docs/crawling-indexing/Verifying-googlebot](https://developers.google.com/search/docs/crawling-indexing/Verifying-googlebot)
* Bingbot: [https://www.bing.com/toolbox/bingbot.json](https://www.bing.com/toolbox/bingbot.json)
* Applebot: [https://support.apple.com/en-us/HT204683](https://support.apple.com/en-us/HT204683)
* Baiduspider: [https://help.baidu.com/question?prod\_en=master\&class=360\&id=1000979](https://help.baidu.com/question?prod_en=master&class=360&id=1000979)
* DuckDuckBot: [https://help.duckduckgo.com/duckduckgo-help-pages/results/duckduckbot/](https://help.duckduckgo.com/duckduckgo-help-pages/results/duckduckbot/)

---

## **1. Googlebot Imposters**

**Expression:**

```
  (http.user_agent contains "Googlebot" and not ip.src in {
    192.178.4.0/27 192.178.4.128/27 192.178.4.160/27 192.178.4.192/27 192.178.4.32/27 192.178.4.64/27 192.178.4.96/27
    192.178.5.0/27 192.178.6.0/27 192.178.6.128/27 192.178.6.160/27 192.178.6.192/27 192.178.6.224/27 192.178.6.32/27 192.178.6.64/27 192.178.6.96/27 
    192.178.7.0/27 192.178.7.128/27 192.178.7.160/27 192.178.7.32/27 192.178.7.64/27 192.178.7.96/27 
    34.100.182.96/28 34.101.50.144/28 34.118.254.0/28 34.118.66.0/28 34.126.178.96/28 34.146.150.144/28 
    34.147.110.144/28 34.151.74.144/28 34.152.50.64/28 34.154.114.144/28 34.155.98.32/28 34.165.18.176/28 
    34.175.160.64/28 34.176.130.16/28 34.22.85.0/27 34.64.82.64/28 34.65.242.112/28 34.80.50.80/28 
    34.88.194.0/28 34.89.10.80/28 34.89.198.80/28 34.96.162.48/28 35.247.243.240/28 
    66.249.64.0/27 66.249.64.32/27 66.249.64.64/27 66.249.64.96/27 66.249.64.128/27 66.249.64.160/27 66.249.64.192/27 66.249.64.224/27
    66.249.65.0/27 66.249.65.32/27 66.249.65.64/27 66.249.65.96/27 66.249.65.128/27 66.249.65.160/27 66.249.65.192/27 66.249.65.224/27
    66.249.66.0/27 66.249.66.32/27 66.249.66.64/27 66.249.66.96/27 66.249.66.128/27 66.249.66.160/27 66.249.66.192/27 66.249.66.224/27
    66.249.67.0/27 66.249.68.0/27 66.249.68.32/27 66.249.68.64/27 66.249.68.96/27 66.249.68.128/27 66.249.68.160/27 66.249.68.192/27
    66.249.69.0/27 66.249.69.32/27 66.249.69.64/27 66.249.69.96/27 66.249.69.128/27 66.249.69.160/27 66.249.69.192/27 66.249.69.224/27
    66.249.70.0/27 66.249.70.32/27 66.249.70.64/27 66.249.70.96/27 66.249.70.128/27 66.249.70.160/27 66.249.70.192/27 66.249.70.224/27
    66.249.71.0/27 66.249.71.32/27 66.249.71.64/27 66.249.71.96/27 66.249.71.128/27 66.249.71.160/27 66.249.71.192/27 66.249.71.224/27
    66.249.72.0/27 66.249.72.32/27 66.249.72.64/27 66.249.72.96/27 66.249.72.128/27 66.249.72.160/27 66.249.72.192/27 66.249.72.224/27
    66.249.73.0/27 66.249.73.32/27 66.249.73.64/27 66.249.73.96/27 66.249.73.128/27 66.249.73.160/27 66.249.73.192/27 66.249.73.224/27
    66.249.74.0/27 66.249.74.32/27 66.249.74.64/27 66.249.74.96/27 66.249.74.128/27 66.249.74.160/27 66.249.74.192/27 66.249.74.224/27
    66.249.75.0/27 66.249.75.32/27 66.249.75.64/27 66.249.75.96/27 66.249.75.128/27 66.249.75.160/27 66.249.75.192/27 66.249.75.224/27
    66.249.76.0/27 66.249.76.32/27 66.249.76.64/27 66.249.76.96/27 66.249.76.128/27 66.249.76.160/27 66.249.76.192/27 66.249.76.224/27
    66.249.77.0/27 66.249.77.32/27 66.249.77.64/27 66.249.77.96/27 66.249.77.128/27 66.249.77.160/27 66.249.77.192/27 66.249.77.224/27
    66.249.78.0/27 66.249.78.32/27 66.249.78.64/27 66.249.78.96/27 66.249.78.128/27
    66.249.79.0/27 66.249.79.32/27 66.249.79.64/27 66.249.79.96/27 66.249.79.128/27 66.249.79.160/27 66.249.79.192/27 66.249.79.224/27
  })
```

Blocks traffic claiming to be Googlebot but not from Google’s official IP ranges.

---

## **2. Bingbot Imposters**

**Expression:**

```
(http.user_agent contains "bingbot" and not ip.src in {13.66.139.0/24 13.66.144.0/20 13.104.0.0/14 13.105.0.0/16 13.107.0.0/16 40.77.167.0/24 40.77.169.0/24 40.77.170.0/23 40.77.172.0/22})
```

Blocks traffic claiming to be Bingbot but not from Microsoft’s official IP ranges.

---

## **3. Other Known Spoofs**

**Expression:**

```
(http.user_agent contains "DuckDuckBot" and not ip.src in {20.191.0.0/16 40.88.21.0/24 40.88.22.0/23}) or
(http.user_agent contains "Applebot" and not ip.src in {17.0.0.0/8}) or
(http.user_agent contains "Baiduspider" and not ip.src in {180.76.0.0/16})
```

Blocks traffic claiming to be DuckDuckBot, Applebot, or Baiduspider but coming from non-authorized ranges.
