<!--
 * @Description: 
 * @Author: Joe
 * @Date: 2023-09-27 16:20:46
 * @LastEditTime: 2023-10-27 09:33:55
 * @LastEditors: Joe
 * @Reference: 
-->

# Set DomainId of Template

The template must be associated with a domain identified by the domainId to control data scraping, such as proxy / browser controllers(playwright/puppeteer/patchright/camoufox etc) / concurrencty / rate limiting, etc.

For simplicity, the domainId defaults to 101, meaning any domain. If this template is not for temporary use, it is recommended not to use the default value, but to use the domainId of the actual accessed domain.

The domainId is ignored in @letsscrapedata/scraper, that means that your configured proxy, browser, etc., meet the template requirements. If the template you designed is only for @letsscrapedata/scraper then you can use the default domainId.

### First get the domainId of a domain
* Run the command "Search Domans".
* Input the domain name to search for.
* The domainId of the domain will be displayed.
* Add a new domain if you can't find a domain name.

### How to add a new domain
* **domainId**: ID of domain, that will be automatically assigned when adding a domain
* **domainName**: name of domain, such as "google.com"
* proxy: proxyIpShareTypes, duration, geos
* browser: browserControllerTypes, browserTypes, browsrHeadlesses, browserIncognitos
* concurrency
* limit rating
* others
* how to add a domain
  * Template 9001 is used to add a domain. The prerequisite is that the domain name can be resolved.
  * If you need to configure advanced properties, such as proxy, please contact us.

### Set domainId of template
The domainId is specified through template attribute. 
* Set template.domainId using the domainId obtained above
```xml
<attr name="domainId" value="11101" />
```


Refer to the video on [how to design a template config#domainId](https://youtu.be/kFlZ0Ogg1PI).
