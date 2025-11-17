<!--
 * @Description: 
 * @Author: Joe
 * @Date: 2023-09-27 16:20:46
 * @LastEditTime: 2023-10-27 09:33:55
 * @LastEditors: Joe
 * @Reference: 
-->

# Set domainId of Template

The template must be associated with a domain identified by the domainId to control data scraping, such as proxy / browser controllers(playwright/puppeteer/patchright/camoufox etc) / concurrencty / rate limiting, etc.

For simplicity, the domainId defaults to 101, meaning any domain. If this template is not for temporary use, it is recommended not to use the default value, but to use the domainId of the actual accessed domain.

### First get the domainId of a domain
* Run the command "Search Domans".
* Input the domain name to search for.
* The domainId of the domain will be displayed.
* Add a new domain if you can't find a domain name.

### How to add a new domain

### Set domainId of template
The domainId is specified through template attribute. 
* Set template.domainId using the domainId obtained above
```xml
<attr name="domainId" value="11101" />
```


Refer to the video on [how to design a template config#domainId](https://youtu.be/kFlZ0Ogg1PI).
