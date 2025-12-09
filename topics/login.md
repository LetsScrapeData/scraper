
# When Login Is Required

### Concepts
* <b>state data</b>: data required to access a website is generally generated after logging in, including cookies / localStroage / HTTP headers / user data
* <b>capability</b>: credentials that is required when you need to log in to access website data
* <b>CapConfig</b>: config of a type of capability, which defines supported login methods, login templates, required proxies and browsers, network access restrictions, etc.

### for user of @letsscrapedata/scraper
* get the state data, such as executing the manual login template in VSCode or other methods
* set the browser's state data to be injected
* start tasks that depends on the injected state data

### for user of LetsScrapeData APP
* add one or more capabilities
* trigger manual login if it is a manual login
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
* others
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
* example: [template 10052](/examples/tid10052_lsdManualLogin)

### How to use state data
If login is required, you need to set the capName of the template. Before executing the template, the state data of the corresponding capability will be automatically injected into the browser and API context.
* cookies: automatically takes effect in browser context; refer to action_setvar_get.get_cookie in API context
* localStorage: automatically takes effect in browser context; refer to action_setvar_get.get_storage in API context
* HTTP headers: used for [API](/toppics/api) request in API context
* user data: other session data that can be used to controll data scraping, that can be accessed through the [variable userData](/topics/variable)
* examples:
  * how to use state data in browser: [template 10053](/topics/tid10053_lsdCapBrowser)
  * how to use state data in API: [template 10054](/topics/tid10054_lsdCapApi)
