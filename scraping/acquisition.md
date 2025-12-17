
# How to Acquire Orignal Data

Original data can be acquired through browser automation and API requests. For details, please refer to [Browser Automation vs API Requests](/scraping/browserVsApi).

LetsScrapeData supports easy and flexible switching between different browser automation and API request tools, avoiding detection.

Depending on the [Webpage Rendering Method](/scraping/rendering), API responses mainly refer to the response data of xhr and document type requests.

The methods described below may require [login](/topics/login) before accessing website data; LetsScrapeData automatically injects and manages the login state data.

### Method 1: Browser Automation - HTML [browser]
* Open a webpage in a browser and perform related actions (such as searching for keywords, scrolling down, etc.).
* Obtain the rendered HTML content.

For instructions on automating browser operations, please refer to [Browser Automation](/topics/browser).

Example: [template 10001](/examples/tid10001_lsdOneList)

### Method 2: Browser Automation - API Responses [browser-interception]
* Enable interception of related API requests.
* Open a webpage in a browser and perform related actions (such as searching for keywords, scrolling down, etc.).
* Obtain the intercepted API response data.

<!-- Example: [template TBD](/examples/tidTBD) -->

### Method 3: Simple API Request - API Responses [API]
* Directly send API requests using an API request tool that automatically generates fingerprints and retrieve the API response data.

Example: [template 10008](/examples/tid10008_extractArray)

### Method 4: Browser Automation and API Request - API Responses [API-browser]
* Enable interception of related API requests.
* Open a page in a browser, etc.
* Obtain the HTTP headers of the intercepted API requests.
* Based on the intercepted HTTP headers, send an API request and retrieve the API response data (this step can be repeated).

<!-- Example: [template TBD](/examples/tidTBD) -->

### Method 5: State Data and API Request - API Responses [API-state]
* Use the injected state data, such as cookies and HTTP headers, to send an API request and retrieve the API response data.

Example: [template 10054](/examples/tid10054_lsdCapApi)

### Method 6: Complex API Request - API Responses [API-advance]
* Use reverse engineering to calculate relevant parameters such as HTTP headers.
* Based on the above parameters, send an API request and retrieve the API response data.

<!-- Example: [template TBD](/examples/tidTBD) -->
