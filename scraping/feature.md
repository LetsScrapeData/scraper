
# Main Features of Web Scraping Tool

### Scheduling
* Expected Scraping Time
  * Once: now or in future
  * Regularly: such as 8 o'clock every day
* Actual Scraping Time
  * Deduplication
  * Proxy: residential / data center / ISP / mobile, geo, duration, etc
  * State Data: cookies / localStorage / HTTP headers / session data; login
  * Concurrency
  * Times: such as 1000 times / hour
  * Controller: such as patchright or camoufox
  * Browser: such as chromium or chrome
  * System Resources: CPU / Memory
  * Priority
  * Retry

### Data Acquisition
* Method
  * Browser Automation
  * API Request
* Bypass Bot Detection
  * Fingerprints: HTTP headers(UA etc), Borwser fingerprints, TLS fingerprints
  * Undetectable Browser: patchright, camoufox, playwright, puppeteer
  * Undetecable HTTP Agent
  * Captcha: Recaptcha, Cloudflare Turnstile, GeeTest, etc
  * IP Access Restriction: such as residential proxy, rotating
  * Rate Limiting
  * Data Encryption: such as TTF / SVG fonts, text in images (OCR)
  * Encrypted Parameters: reverse engineering needed

For more information, please refer to [How to Acquire Orignal Data](/scraping/acquisition).

### Data Extraction
* from HTML
  * Sources: dynamic or static
  * CSS Selector
  * XPath
* from API Responses
* Data Cleaning

For more information, please refer to [How to Extract Data](/topics/extraction).

### Monitoring
* Proxy Error
* Failed Reasons
* Unexpected or Wrong Data
* Expired Login
* Blocked
* etc

For more information, please refer to [How to Monitor Web Scrping](/topics/monitoring).

### Data Management
* Data Export: Excel, JSON, etc
* Data Synchronization: relational DB
* Data Push: API
* Data Processing: data re-extraction
* Data Retrieval: API

### Summary
* The Most Difficult: bypass bot detection
* The Most Complex: scheduling and monitoring
* The Most Tedious: data extraction
* The Ultimate Goal: low cost and stability


Only 'Encrypted Parameters' requires programming. The others can be implemented without programming.

For more information, see https://github.com/LetsScrapeData/scraper
