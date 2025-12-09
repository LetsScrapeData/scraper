
# How to Scrape Data by Browser Automation

LetsScrapeData uses the NPM package [@letsscrapedata/controller](https://www.npmjs.com/package/@letsscrapedata/controller) to automate browser operations, that facilitate switching between different types of browser controllers(such as Playwright, Patchright, Camoufox, Puppeteer, etc) and support for the new anti-bot browser controller without modifying existing programs or templates.

### Operate page or element
* ***action_click***：This method scrolls element into view if needed, and then uses Page.mouse to click in the center of the element.
* ***action_goto***：Navigates the page to the given *url*.
* ***action_hover***：This method scrolls element into view if needed, and then uses Page.mouse to hover over the center of the element.
* ***action_input***：Set a value to the input field.
* ***action_scroll_by***： Scroll an element by the given amount, such as a window height.
* ***action_scroll_intoview***：Scrolls the element into view using either the automation protocol client or by calling element.scrollIntoView.
* ***action_scroll_to***：Scroll to a particular set of coordinates inside a given element.
* ***action_select***：Triggers a change and input event once all the provided options have been selected.

### Loop through elements
* ***action_loopineles***: Loop through selected elements, using each element as the parent element, and optionally select child elements for the operation; for example, loop through a list of products.

### Extract data from elements
* ***action_extract.column_element***: Extract data from elements selected via CSS selector or XPath, such as text, html, attribute, etc
* ***action_extract_table***: Extract data from the table in the page

### Get content from page
The following getter in the ***action_setvar_get*** action can retrieve relevant content from the page:
* ***get_content***: Get the full HTML contents of the page.
<!-- * ***get_evaluate***:  -->
* ***get_mhtml***: Generates a MHTML of the page and save to file.
* ***get_pdf***: Generates a PDF of the page and save to file.
* ***get_screenshot***: Captures a screenshot of the page or element. Save to file if needed.
* ***get_title***: Get the title of the page.
* ***get_window***: get the value of subkeys of the page's window.

### Execute a script in page
* ***action_setvar_get.get_evaluate***: Execute JavaScript code in the page and return the result.

### Get the state data in page
* ***misc_getstatedata*** in ***misc_action***: Get the cookies, localStorage, HTTP headers of intercepted request, etc.

Note: action_setvar_get.get_cookie/get_localstorage retrieves relevant data from injected or newly acquired state data, not from the page.

### Intercept HTTP requests
* ***action_intercept_set***: Enable the interception of requests in the page. Save the responses to files if needed.
* ***action_intercept_clear***: Disable the interception of requests in the page.

### Hightlight selected elements
This is valid only in debug mode.

Refer to [LetsScrapeData extension](https://marketplace.visualstudio.com/items?itemName=LetsScrapeData.letsscrapedata) for more details.

### Use the CSS selector auto-prompt
This is valid only in debug mode.

Refer to [CSS Selectors Auto-prompt](/start/cssselecor) for more details.
