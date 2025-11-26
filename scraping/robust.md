<!-- 
### How to Build a Robust Web Scraping Tool
1. **Multiple Solutions**
  * For example, browser-based solutions are more stable, while API requests are more efficient; combining both is recommended, along with the latest undetectable tools.
2. **Redundancy**
* Use multiple CSS Selectors or XPaths to adapt to changes (AI-generated XPaths are not recommended as they are difficult to adapt to).
3. **Validation**
* Verify the validity of API status code and extracted data values.
4. **Monitoring**
* Promptly detect and report anomalies.
5. **Retry**
* Automatically retry all anomalies after correction.

For more related content, please refer to [How to Build a Robust Web Scraping Tool](https://letsscrapedata.github.io/scraper/#/scraping/robust)
 -->

### How to Build a Robust Web Scraping Tool
1. **Multiple Solutions**
* For example, browser-based solutions are more stable, while API requests are more efficient; combining both is recommended, along with the latest undetectable tools.
* Refer to [Common Web Scraping Solutions](/scraping/solution)
2. **Redundancy**
* Use multiple CSS Selectors or XPaths to adapt to changes (AI-generated XPaths are not recommended as they are difficult to adapt to).
* Refer to [CSS Selector / XPath Suggestions](/scraping/cssxpath)
3. **Validation**
* Verify the validity of API status code and extracted data values.
* Refer to action_api and patten/valerrname
4. **Monitoring**
* Promptly detect and report anomalies.
* Refer to [How to Monitor Web Scraping](/topics/monitor)
5. **Retry**
* Automatically retry all anomalies after correction.
* After the template is corrected, previously failed tasks will be automatically retried.