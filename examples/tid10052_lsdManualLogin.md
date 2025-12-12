# Manual Login Template

### Template config
```xml
<?xml-model href="https://www.LetsScrapeData.com/xsd/lsd_en.xsd" type="application/xml" schematypens="http://www.w3.org/2001/XMLSchema"?>
<template tid="10052" version="0.0.12" commited="true">
  <attrs>
    <attr name="name" value="Demo - manual login of capName lsd" />
    <attr name="desc"
      value="Demo - manual login of capName lsd, only cookies / localStorage / headers are needed. User data are also supported. Templates cannot directly access cookies /localStorage / headers for security reasons, but can use them as needed." />
    <attr name="domainId" value="10000" />
    <!-- manual login template of capability -->
    <attr name="templateCat" value="12" />
    <attr name="cfgShareLevel" value="120" />
  </attrs>
  <paras />
  <actions>
    <!-- intercept related request if http headers are needed -->
    <action_intercept_set>
      <response_cache url="^http:.*/api/schedule/" method="PUT" resourcetype="xhr" requestheaders="true" />
    </action_intercept_set>
    <!-- open the login page -->
    <action_goto url="http://127.0.0.1:8090/" wait="10000" />
    <!-- regularly check if you have logged in successfully -->
    <action_loopfor from="0" to="180" varname="varname">
      <action_misc>
        <misc_getstatedata cookies="none" headers="none" localstorage="new" />
      </action_misc>
      <action_setvar_get varname="secureData.token">
        <get_localstorage origin="http://127.0.0.1:8090" name="token" source="new" />
      </action_setvar_get>
      <action_ifelse>
        <condition_templstr>
          <templstr templ="${secureData.token}" />
          <transform>
            <fun_length />
            <fun_n_gt number2="0" />
          </transform>
          <action_misc>
            <!-- succeeded to log in -->
            <!-- by default, cookies and localStorage are included -->
            <misc_getstatedata headers="cachedRequestHeaders" />
          </action_misc>
          <action_exit errname="normal" />
        </condition_templstr>
        <condition_else>
          <action_wait_sleep minms="2000" maxms="2000" />
        </condition_else>
      </action_ifelse>
    </action_loopfor>
    <!-- failed to log in -->
    <action_exit errname="other" />
  </actions>
</template>
```

### Example of results
```javascript
```
