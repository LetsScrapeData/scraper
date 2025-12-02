
# Browser Automation vs API Request
Browser automation and API requests are distinct approaches to interacting with web applications and services, each with its own advantages and suitable use cases.

### Browser automation
Browser automation involves controlling a web browser programmatically to simulate user interactions. This typically utilizes tools like Selenium, Playwright, or Puppeteer.

### API request
API requests involve direct communication with a server's Application Programming Interface (API) to send and receive data. This is typically done using libraries or tools like Postman, cURL, or requests in Python.

### How to choose
##### Main Cost of scraping data
* Program development and maintenance costs
  * If reverse engineering is required to calculate API request parameters, the development and maintenance costs of API request methods are generally much higher than those of browser automation.
  * In other scenarios, the two are not significantly different.
* Network proxy costs:
  * The proxy cost of browser automation is far greater than that of API requests.
  * If browser automation is used, images, css and other files can be blocked; if you need to download images, etc., you can mostly use low-cost data center proxies.
* Host resource costs: The cost of using cloud servers will be much higher than local deployment; using API will significantly reduce this cost.
  * The host cost of browser automation is far greater than that of API requests.
* Scraping maintenance costs: program deployment, timely detection of anomalies, re-scraping of abnormal data, etc.
  * It mainly depends on whether the scraping tool has features such as automatic retry, the number of deployments, and its variability.

##### Main influencing factors
* Anti-bot: website anti-bot features
* Amount: the number of data to be scraped
* Timeliness: in most cases, the timeliness requirement for scraping data is relatively low
* Variability: liability to vary or change
  * API request parameters (including encrypted parameters)
  * HTML structure

##### Which method to use
* If timeliness is very important, generally only API requests can be used.
* If the amount of scraped data is vary large, API requests are strongly recommended.
* If the amount of scraped data is small, browser automation are prefered.
* If API request parameters have high variablity, browser automation are prefered.
* If the residential proxies must be used, API requests are prefered.
* In other scenarios, choose the familiar method.

Apart from the first two scenarios, the choice of which method to use generally doesn't make a significant difference in other scenarios.

### More related
* [How to Acquire Original Data](/topics/acquisition)
* [How to Scrape Data by Browser Automation](/topics/browser)
* [How to Scrape Data Using API](/topics/api)
