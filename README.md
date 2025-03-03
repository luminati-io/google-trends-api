# Google Trends Scraper API

[![Promo](https://github.com/luminati-io/LinkedIn-Scraper/blob/main/Proxies%20and%20scrapers%20GitHub%20bonus%20banner.png)](https://brightdata.com/products/serp-api/google-search/trends)

This repository provides two approaches for collecting Google Trends data:

1. **Free Scraper:** A lightweight solution for small-scale projects, testing, personal research, and educational purposes.
2. **[Bright Data Google Trends Scraper API](https://brightdata.com/products/serp-api/google-search/trends):** A robust, high-volume solution for enterprise-level, scalable, and reliable data extraction.

## Table of Contents
- [Free Scraper](#free-scraper)
  - [Setup](#setup)
  - [Quick Start](#quick-start)
  - [Sample Output](#sample-output)
  - [Limitations](#limitations)
- [Bright Data Enterprise Solution](#bright-data-enterprise-solution)
  - [Getting Started](#getting-started)
  - [Direct API Access](#direct-api-access)
  - [Native Proxy-Based Access](#native-proxy-based-access)
- [Advanced Features](#advanced-features)
  - [Widgets](#widgets)
  - [Geographic Filtering](#geographic-filtering)
  - [Localization](#localization)
  - [Time Range](#time-range)
  - [Category Filtering](#category-filtering)
  - [Search Type](#search-type)
- [Support & Resources](#support--resources)

## Free Scraper

<img width="700" alt="bright-data-google-trends-api-screenshot-google-trends-page" src="https://github.com/luminati-io/google-trends-api/blob/main/images/418445062-2168a20d-a588-454e-a682-a6bba3e4e460.png" />

A simple Google Trends scraper for small-scale data collection projects.


### Setup

**Requirements:**
- Python 3.9+
- Playwright (for browser automation)

**Installation:**
```bash
pip install playwright
playwright install
```

> **New to web scraping?** Follow our [beginner's guide to web scraping with Python](https://brightdata.com/blog/how-tos/web-scraping-with-python)
>

### Quick Start
1. Edit these variables in [google-trends-scraper.py](https://github.com/luminati-io/Google-Trends-Scraper-API/blob/main/google-trends-scraper/google-trends-scraper.py):
```python
query = "cryptocurrency"  # Your search term
geo = "US"                # Country code
hl = "en-US"              # Language code
```
2. Run the script

💡 **Pro Tip:** Set `HEADLESS = False` to reduce detection by Google's anti-scraping systems.

### Sample Output
```json
{
    "geoCode": "US-DC",
    "geoName": "District of Columbia",
    "value": [100],
    "formattedValue": ["100"],
    "maxValueIndex": 0,
    "hasData": [true],
}
```

👉 See the [full JSON output](https://github.com/luminati-io/Google-Trends-Scraper-API/tree/main/google-trends-results).


### Limitations
Free Scraper comes with limitations:
- High risk of IP blocks
- Limited request volume
- Frequent CAPTCHAs
- Unreliable for large-scale scraping

For reliable, large-scale scraping, you'll need a more advanced solution.

## Bright Data Enterprise Solution
[Bright Data's Google Trends API](https://brightdata.com/products/serp-api/google-search/trends) provides structured Google Trends data with customizable search parameters. Built on the same advanced technology as the [SERP API](https://brightdata.com/products/serp-api), it provides:

- **Global Location Accuracy:** Tailor results to any location
- **Pay-Per-Success Model**: Only pay for successful requests
- **Real-Time Data**: Retrieve up-to-date search results in seconds
- **Scalability**: Handle unlimited requests with no volume restrictions
- **Cost Efficiency**: Save on infrastructure and maintenance costs
- **Highest Reliability**: Consistent performance with built-in anti-blocking measures
- **Technical Support**: Expert assistance available when needed


### Getting Started

1. **Prerequisites**:
    - Create a [Bright Data account](https://brightdata.com/) (new users get $5 credit)
    - Obtain your [API key](https://docs.brightdata.com/general/account/api-token)
2. **Setup**: Follow our [step-by-step guide](https://github.com/luminati-io/Google-Trends-Scraper-API/blob/main/setup-serp-api-guide.md) to integrate the API
3. **Implementation Methods**:
    - Direct API Access
    - Native Proxy-Based Access


### Direct API Access

Make a direct request to the API endpoint:

**cURL Example:**

```bash
curl https://api.brightdata.com/request \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer API_TOKEN" \
  -d '{
        "zone": "ZONE_NAME",
        "url": "https://trends.google.com/trends/explore?q=coffee&geo=GB&brd_trends=timeseries,geo_map&brd_json=1",
        "format": "raw"
      }'

```

**Python Example:**

```python
import requests
import json

url = "https://api.brightdata.com/request"
headers = {"Content-Type": "application/json", "Authorization": "Bearer API_TOKEN"}

payload = {
    "zone": "ZONE_NAME",
    "url": "https://trends.google.com/trends/explore?q=coffee&geo=GB&brd_trends=timeseries,geo_map&brd_json=1",
    "format": "raw",
}

response = requests.post(url, headers=headers, json=payload)

with open("serp_direct_api.json", "w") as file:
    json.dump(response.json(), file, indent=4)

print("Response saved to 'serp_direct_api.json'.")

```

👉 See the [full JSON output](https://github.com/luminati-io/Google-Trends-Scraper-API/blob/main/google-trends-api-results/serp_direct_api.json).

> **Note:** Use `brd_json=1` for parsed JSON. Additional parameters such as `geo` and `brd_trends` are explained in the Advanced Features section below.
> 

### Native Proxy-Based Access

You can also use our proxy routing method:

**cURL Example:**

```bash
curl -i \
  --proxy brd.superproxy.io:33335 \
  --proxy-user "brd-customer-<customer-id>-zone-<zone-name>:<zone-password>" \
  -k \
  "https://trends.google.com/trends/explore?q=coffee&geo=GB&brd_trends=timeseries,geo_map&brd_json=1"

```

**Python Example:**

```python
import requests
import urllib3

urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)

host = "brd.superproxy.io"
port = 33335
username = "brd-customer-<customer-id>-zone-<zone-name>"
password = "<zone-password>"
proxy_url = f"http://{username}:{password}@{host}:{port}"

proxies = {"http": proxy_url, "https": proxy_url}
url = "https://trends.google.com/trends/explore?q=coffee&geo=GB&brd_trends=timeseries,geo_map&brd_json=1"
response = requests.get(url, proxies=proxies, verify=False)

with open("serp_native_proxy.json", "w", encoding="utf-8") as file:
    file.write(response.text)

print("Response saved to 'serp_native_proxy.json'.")

```

👉 See the [full JSON output](https://github.com/luminati-io/Google-Trends-Scraper-API/blob/main/google-trends-api-results/serp_native_proxy.json).

> **Note:** For production environments, load Bright Data's SSL certificate as described in our [SSL Certificate Guide](https://docs.brightdata.com/general/account/ssl-certificate).
>

## Advanced Features

### Widgets
<img width="700" alt="bright-data-google-trends-api-screenshot-timeseries-and-geomap" src="https://github.com/luminati-io/google-trends-api/blob/main/images/418487699-20fd3ec5-b152-4e70-bee3-b093b7d78b86.png" />

Google Trends provides different widgets to extract meaningful insights. You can specify which widgets you want using the `brd_trends` parameter:

**Available Widgets:**

- `timeseries` → Interest over time
- `geo_map` → Interest by subregion

**Using Multiple Widgets:**

You can combine multiple widgets by separating them with a comma:

```bash
curl --proxy brd.superproxy.io:33335 \
  --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
  -k "https://trends.google.com/trends/explore?q=ChatGPT&geo=US&brd_trends=timeseries,geo_map&brd_json=1"
```


### Geographic Filtering
The `geo` parameter allows you to filter search trend data for a specific country (e.g., `geo=US` for the United States). If omitted, the API defaults to global trends.

**Example:**

```bash
curl --proxy brd.superproxy.io:33335 \
  --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
  -k "https://trends.google.com/trends/explore?q=coffee&geo=GB&brd_trends=timeseries,geo_map&brd_json=1"
```

### Localization
<img width="700" alt="bright-data-google-trends-api-screenshot-set-language" src="https://github.com/luminati-io/google-trends-api/blob/main/images/418515025-d68f07f2-8a6a-46ef-942a-38b2813268dd.png" />

The `hl` parameter allows you to retrieve search trend data in a specific language:

- It accepts a language code (e.g., `en-US`, `fr-FR`)
- This affects the language of the returned data, not the actual search results

**Example:**

```bash
curl --proxy brd.superproxy.io:33335 \
  --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
  -k "https://trends.google.com/trends/explore?q=coffee&hl=fr-FR&brd_trends=timeseries,geo_map&brd_json=1"
```

### Time Range

The `date` parameter defines a specific time range for retrieving trend data:

| **Value** | **Time Range** |
| --- | --- |
| now 1-H | Past 1 hour |
| now 4-H | Past 4 hours |
| now 1-d | Past day (24 hours) |
| now 7-d | Past 7 days |
| today 1-m | Past 30 days |
| today 3-m | Past 90 days |
| today 12-m | Past 12 months (Default) |
| today 5-y | Past 5 years |
| YYYY-MM-DD YYYY-MM-DD | Custom date range |

**Example for Past 30 Days:**

```bash
curl --proxy brd.superproxy.io:33335 \
  --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
  -k "https://trends.google.com/trends/explore?q=coffee&date=today+1-m&brd_trends=timeseries,geo_map&brd_json=1"
```

**Example for Custom Date Range:**

```bash
curl --proxy brd.superproxy.io:33335 \
  --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
  -k "https://trends.google.com/trends/explore?q=coffee&date=2025-01-02+2025-03-03&brd_trends=timeseries,geo_map&brd_json=1"
```

### Category Filtering

The `cat` parameter allows you to narrow down search trends within a specific category:

- By default, Google Trends searches across all categories
- Categories are represented by numeric IDs
- You can find the full list of category IDs on [Google Trends](https://trends.google.com/trends/api/explore/pickers/category?lang=en-US&tz=240)

Example – Fetch trends for “Bitcoin” in the Business & Industrial category (cat=12):

```bash
curl --proxy brd.superproxy.io:33335 \
  --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
  -k "https://trends.google.com/trends/explore?q=bitcoin&cat=12&brd_trends=timeseries,geo_map&brd_json=1"
```

### Search Type

The `gprop` (Google Property) parameter filters search trends by specific Google services:

| **Value** | **Google Property** |
| --- | --- |
| images | Google Images |
| news | Google News |
| froogle | Google Shopping |
| youtube | YouTube Search |

If omitted, it defaults to a web search.

**Examples:**

1. **Image Search Trends (gprop=images):**

```bash
curl --proxy brd.superproxy.io:33335 \
  --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
  -k "https://trends.google.com/trends/explore?q=nft+art&gprop=images&brd_trends=timeseries,geo_map&brd_json=1"
```

2. News Search Trends (gprop=news):

```bash
curl --proxy brd.superproxy.io:33335 \
  --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
  -k "https://trends.google.com/trends/explore?q=AI+advancements&gprop=news&brd_trends=timeseries,geo_map&brd_json=1"

```

3. YouTube Search Trends (gprop=youtube):

```bash
curl --proxy brd.superproxy.io:33335 \
  --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
  -k "https://trends.google.com/trends/explore?q=python+tutorials&gprop=youtube&brd_trends=timeseries,geo_map&brd_json=1"

```

## Support & Resources

- **Documentation**: [SERP API Docs](https://docs.brightdata.com/scraping-automation/serp-api/)
- **SEO Use Cases**: [SEO Tracking and Insights](https://brightdata.com/use-cases/serp-tracking)
- **Additional Guides**:
    - [SERP API](https://github.com/luminati-io/serp-api)
    - [Google Search API](https://github.com/luminati-io/google-search-api)
    - [Web Unlocker API](https://github.com/luminati-io/web-unlocker-api)
    - [Google News Scraper](https://github.com/luminati-io/Google-News-Scraper)
- **Technical Articles**:
    - [Best SERP APIs](https://brightdata.com/blog/web-data/best-serp-apis)
    - [Build a RAG Chatbot with SERP API](https://brightdata.com/blog/web-data/build-a-rag-chatbot)
    - [How to Scrape Google Trends with Python](https://brightdata.com/blog/web-data/how-to-scrape-google-trends)
- **Technical Support**: [Contact Us](mailto:support@brightdata.com)
