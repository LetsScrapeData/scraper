
# Capability

### Concepts
* <b>state data</b>: data required to access a website is generally generated after logging in, including cookies / localStroage / HTTP headers / user data
* <b>capability</b>: credentials that is required when you need to log in to access website data
* <b>CapConfig</b>: config of a type of capability, which defines supported login methods, login templates, required proxies and browsers, network access restrictions, etc.

### for user of @letsscrapedata/scraper
* set the browser's state data to be injected
* start tasks that depends on the injected state data

### for user of LetsScrapeData APP
* add one or more capabilities
* add a schedule of a template depending on capability

### for designer
* design automatic login template
* design munual login template
* add CapConfig

### CapConfig
* **capName**: name of CapConfig
* **autoLoginTid**: automatic login template
* **manualLoginTid**: manual login template
* **domainId**
* **loginValidityPeriod**: in hours
* meta data of automatic login: such as username / password
* proxy: proxyIpShareTypes, duration, geos
* browser: browserControllerTypes, browserTypes, browsrHeadlesses, browserIncognitos
* concurrency
* limit rating
* how to add a CapConfig
  * Template 9002 is used to add a CapConfig.
  * If you need to configure advanced properties, such as meta data or proxy, please contact us.

### How to desgin an automatic login template
* set attr **templateCat** of template to 11: this is an automatic login template
* set attr **capId** of template: capability used for debugging this template
* open the login page
* solve captcha if needed
* input & submit: variable **authInfo** contains the contents of capability
* intercept HTTP headers if needed
* generate the user data if needed
* get state data that interest you
* example: [template 10051](/examples/tid10051_lsdAutoLogin)

### How to design a manual login template
* set attr **templateCat** of template to 12: this is an manual login template
* open the login page
* regularly check if you have logged in successfully
* if the login is successful, get state data that interest you
* if login fails, ignore the login attempt
* example: [template 10052](/examples/tid10052)

### How to use state data
* capName: state data is automatically injected into context
* cookies: automatic use in browser; get_cookie in API
* localStorage: automatic use in browser; get_storage in API
* HTTP headers: mainly used for [APIs](/toppics/api)
* user data: other session data that can be used to controll data scraping
* examples:
  * how to use state data in browser: [template 10053](/topics/tid10053)
  * how to use state data in API: [template 10054](/topics/tid10054)
