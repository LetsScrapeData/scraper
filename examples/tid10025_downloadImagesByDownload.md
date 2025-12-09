
### Template config
```xml
<?xml-model href="https://www.LetsScrapeData.com/xsd/lsd_en.xsd" type="application/xml" schematypens="http://www.w3.org/2001/XMLSchema"?>
<template tid="10025" version="0.0.6" commited="true">
  <attrs>
    <attr name="name" value="Demo - download image by interception" />
    <attr name="desc" value="Demo - download image by interception" />
    <attr name="domainId" value="1" />
    <attr name="cfgShareLevel" value="120" />
    <attr name="parasstr" value="https://www.ebay.com/sch/i.html?_nkw=iphone%2015%20case::ul.srp-list > li div.s-item__image-wrapper > img" />
  </attrs>
  <paras>
    <para paraname="para1" name="pageUrl" desc="pageUrl, url of web page to be opened" />
    <para paraname="para2" name="imageLoc" desc="imageLoc, CSS selector or XPath that selects the img elements" />
  </paras>
  <actions>
    <!-- Solution 2 - get url and filename of images, then downlod and save them -->
    <action_intercept_set>
      <request_abort />
    </action_intercept_set>
    <action_goto url="${inParas.para1}" wait="5000" />
    <action_scroll_by maxtimes="0" interval="3000" />
    <action_loopineles maxloops="5">
      <element loc="${inParas.para2}" />
      <action_setvar_element varname="imageUrl">
        <element loc="." />
        <elecontent_attr attrname="src" absolute="true" />
      </action_setvar_element>
      <action_setvar_get varname="imageContent">
        <get_file url="${imageUrl}" />
      </action_setvar_get>
    </action_loopineles>
  </actions>
</template>
```

### Example of results
```json
```
