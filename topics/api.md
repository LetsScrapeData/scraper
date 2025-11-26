
# How to Use API

In LetsScrapeData, use the action ***action_api*** to send HTTP requests.

### API context
LetsScrapeData supports the following independent API contexts.
##### default
The default API context automatically simulates the fingerprints (HTTP headers) of a real browser user and tries to update to use the latest, undetectable HTTP request tools. Using the default API context is recommended whenever possible.
##### browser
The browser API context is associated with the BrowserContext and automatically manages and shares cookies. See [APIRequestContext](https://playwright.dev/docs/api/class-apirequestcontext) for more details.
##### standalone
The standalone API context, similar to a browser API context, but the two do not share state data. When only API requests are made and no browser is used, the logged-in state data is automatically injected into this standalone API context.
##### state
The API context for injecting state data will be automatically replaced with a browser or standalone API context, depending on the situation.
##### fetch
The fetch API context will directly use the fetch HTTP request tool in Node.js.

The *context* attribute of ***action_api*** determines the specific context used; the default value is "default".

### Request method
The *method* attribute of ***action_api*** specifies the request method, which defaults to "GET".

### Request URL
The *url* and *encodeuri* attributes of ***action_api*** specify the URL of the HTTP request.
When the *format* attribute of ***action_api*** is "params", the request data will be treated as [searchParams](https://developer.mozilla.org/en-US/docs/Web/API/URL/searchParams).

### Request headers
##### Common methods for generating request headers
First, if the state data contains request headers, generally use those headers first. Example: [template xxx](/examples/tidxxx).

Second, if some request headers are dynamically generated via JavaScript and can be reused, generally use the request headers intercepted in the browser.

Third, using the default API context will automatically generate request headers simulating a real browser user.

Finally, you can use ***action_setvar_get.get_httpheaders*** to generate the desired request headers.

If needed, you can replace or add additional request headers based on the above.

##### How to generate request headers in LetsScrapeData
The *headerssource* attribute of ***action_api*** determines how the initial request headers are obtained.
* **headers**: The value of the *headers* attribute is the initial value, which is usually empty or the result of ***action_setvar_get.get_httpheaders***.
* **origStateHeaders**: The headers of injected state data, refer to [When Login Is Required](/topics/login).
* **updatedStateHeaders**: The updated headers of the above origStateHeaders.
* **cachedRequestHeaders**: The cached headers of intercepted requests, refer to ***action_intercept_set.response_cache***.
* **updatedRequestHeaders**: The updated headers of the above cachedRequestHeaders.
* **cachedResponseHeaders**: The cached headers of intercepted requests, refer to ***action_intercept_set.response_cache***.
* **updatedResponseHeaders**: The updated headers of the above cachedResponseHeaders.

For security reasons, state headers and intercepted headers cannot be accessed directly through variables.

If needed, you can use `action_api.request_header` to replace or add additional request headers based on the above request headers.

##### Header content-length
If the request header contains content-length, its value is automatically replaced with a value calculated based on the content of the request data.

### Request data
The *data* and *datatype* of ***action_api*** determine the initial request data object, and then new object attributes can be added using ***object_key***.
If the request data is complex, it is recommended to use ***action_setvar_object*** to generate the request data first.
If the request data is a form or search parameter, you can set the *format* attribute to "form" or "params".

### How to use proxy
The ***action_api*** uses the assigned proxy by default when sending HTTP requests. If you do not want to use a proxy, you can set the *proxy* attribute to false.

### Status code of response
By default, ***action_api*** handles common status codes of response. You can also define how to handle different status codes by using ***response_statuscode***, such as proxylocked and capexpired(login is expired).

For more information, see [errname](/reference/errname).

### How to process the response data
If the API request is successful,  the response data needs to be saved so that the required content can be extracted later.
##### How to validate the response data
If the *valerrname* attribute is not "ignore", the updated response data is validated based on the *pattern* and *flags* attributes to ensure it meets expectations; otherwise, it is considered an exception specified by *valerrname*.
##### How to save the response data
* Cache response: If the *cache* attribute is true, similar to ***response_cache***, response data and other information will be temporarily cached in the data table.
* Save to data table: push the object { pageUrl, requestMethod, requestUrl, requestData, responseData, size } ( and requestHeaders in debug mode) into the data table if tabname is not "".
* Save to variables: 
  * First, get the value of response data, aka updated response data, if the *subkeys* attribute is not "".
  * Save the updated response data to variable if the *varname* attribute is not "".
  * Save the properties of the updated response data to variables if the *setkeys* attribute is not "", "*" means all keys of the object. (similar to destructuring)

### How to debug API using intercepted API request
This section is only valid in debug mode.

Before attempting to use an API, we typically open devTools in a browser, visit the webpage, find the desired API request, and then mimic that API request. The following configuration makes this process easier.
* First, intercept the API request using ***action_intercept_set.response_cache***.
* Then, mimic that API request using ***action_api***:
  * When the *requestprefix* attribute is not "", if there is an intercepted API request, its related data is saved to a local file; otherwise, it attempts to read previously saved data from the local file (the file name is requestprefix_request.json). This allows you to view the detailed content of the intercepted API request, and the interception can be used for repeated debugging later.
  * If the ***url*** attribute is "cachedRequestUrl", then ***url*** will be replaced with the url in the intercepted API request.
  * If the ***data*** attribute is "cachedRequestData", then ***data*** will be replaced with the request data in the intercepted API request.
  * If the ***headers*** attribute is "cachedRequestHeaders", then ***headers*** will be replaced with the headers in the intercepted API request.

Example: [template TBD](/examples/tidTBD)

### How to cache API response data during debugging
This section is only valid in debug mode.

When debugging API requests, it's necessary to view the specific content of the response. After a successful API request, it's necessary to repeatedly debug how to extract the expected data, all of which require caching the response data.

When the *responseprefix* attribute is not "", it first attempts to read the previously cached response data from the local file (the file name is responseprefix_response.json). If successful, no API request needs to be sent; otherwise, an API request is sent. After the API request is successful, the response data is saved to the local file.

Example: [template TBD](/examples/tidTBD)

### How to extract expected data later
In most cases, ***action_extract_array*** is sufficient to extract the desired data. Example: [template TBD](/examples/tidTBD)

For more complex data, ***action_extract*** can be used. Example: [template TBD](/examples/tidTBD)

For extremely complex data, ***action_extract_script*** can be used to extract the desired data using a script. Example: [template TBD](/examples/tidTBD)
