
### Template config
```xml
<?xml-model href="https://www.LetsScrapeData.com/xsd/lsd_en.xsd" type="application/xml" schematypens="http://www.w3.org/2001/XMLSchema"?>
<template tid="10021" version="0.0.6" commited="true">
  <attrs>
    <attr name="name" value="Demo - save webpage into a mhtml file" />
    <attr name="desc" value="Demo - save webpage into a mhtml file" />
    <attr name="domainId" value="1" />
    <attr name="cfgShareLevel" value="120" />
    <attr name="parasstr" value="https://www.LetsScrapeData.com" />
  </attrs>
  <paras>
    <para paraname="para1" name="url" desc="url of web page" />
  </paras>
  <actions>
    <action_goto url="${inParas.para1}" wait="5000" />
    <!-- Scroll to the bottom of the page to load the full page content (including lazy loaded images) -->
    <action_scroll_by maxtimes="5" interval="3000"></action_scroll_by>
    <action_setvar_get varname="content">
      <!-- By default, save the web page content to an mhtml file named "title of page" -->
      <get_mhtml />
    </action_setvar_get>
  </actions>
</template>
```

### Example of results
```json
```
