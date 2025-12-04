<!-- 
### How to Build a Robust Web Scraping Tool
1. **Multiple Solutions**
  * For example, browser-based solutions are more stable, while API requests are more efficient; combining both is recommended, along with the latest undetectable tools.
2. **Redundancy**
* Use multiple CSS Selectors or XPaths to adapt to changes (AI-generated XPaths are not recommended as they are difficult to adapt to).
3. **Exception Handling**
* Handle common execptions in web scraping actions
* Validate the API response data and extracted data to meet expectations
* Hanlde different status codes of API response
* Handle other specific exceptions
4. **Monitoring**
* Promptly detect and report anomalies.
5. **Retry**
* Automatically retry all anomalies after correction.

For more related content, please refer to [How to Build a Robust Web Scraping Tool](https://letsscrapedata.github.io/scraper/#/scraping/robust)
 -->

### How to Build a Robust Web Scraping Tool
1. **Multiple Solutions**
* For example, browser-based solutions are more stable, while API requests are more efficient; combining both is recommended, along with the latest undetectable tools.
* Refer to [How to Acquire Original Data](/scraping/acquisition)

2. **Redundancy**
* Use multiple CSS Selectors or XPaths to adapt to changes (AI-generated XPaths are not recommended as they are difficult to adapt to changes).
<!-- * Refer to [CSS Selector / XPath Suggestions](/scraping/cssxpath). -->
* LetsScrapeData supports multiple CSS Selectors or XPaths, and will try them one by one until the element is selected.

3. **Exception Handling**
* Handle common execptions in web scraping actions
* Validate the API response data and extracted data to meet expectations
* Hanlde different status codes of API response
* Handle other specific exceptions
* Refer to [How to Handle Exceptions](/topics/exception) for details.

4. **Monitoring**
* Promptly detect and report anomalies.
* Refer to [How to Monitor Web Scraping](/topics/monitoring)

5. **Retry**
* Automatically retry all anomalies after correction.
* After the template is corrected, previously failed tasks will be automatically retried.
