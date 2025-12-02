
# Web Page Rendering Methods
Based on how and where HTML is rendered, web pages are divided into three main types:

### Static Rendering (Static Site Generation or SSG)
All pages are pre-built into static HTML files during the build process.

###  Server-Side Rendering (SSR)
The server generates the full HTML for a page with each user request and sends it to the browser.

### Client-Side Rendering (CSR)
The server sends a minimal HTML file and a JavaScript bundle to the browser. The browser then runs the JavaScript to render the content.

### Comparison
* Static rendering is the fastest because pages are pre-built HTML files served from a CDN.
* Server-side rendering (SSR) generates pages on the server for each request, providing dynamic content with good SEO but higher server load.
* Client-side rendering (CSR) sends a minimal HTML file and JavaScript, which renders the page in the browser, ideal for highly interactive apps but with a slower initial load and potential SEO challenges. 

For content-intensive websites that are highly dependent on SEO (such as blogs, news, and e-commerce product pages), SSR or SSG should be given priority; otherwise, CSG should be given priority.

### Impact on Web Scraping
* For web pages rendered by SSG and SSR, the data to be scraped is only in the HTML.
* For web pages rendered by CSR, the data to be scraped is in both the API response and the HTML.

