# Automatic Login Template

### Template config
```xml
<?xml-model href="../../lsd.xsd" type="application/xml" schematypens="http://www.w3.org/2001/XMLSchema"?>
<template tid="10051" version="0.0.10" commited="true">
  <attrs>
    <attr name="name" value="Demo - automatic login of capName lsd" />
    <attr name="desc"
      value="Demo - automatic login of capName lsd, only cookies / localStorage / headers are needed. User data are also supported. Templates cannot directly access cookies /localStorage / headers for security reasons, but can use them as needed." />
    <attr name="domainId" value="10000" />
    <!-- automatic login template of capability -->
    <attr name="templateCat" value="11" />
    <attr name="cfgShareLevel" value="120" />
    <!-- The following capacity is only used to test this template, which must be disabled to prevent it from being used by other tasks -->
    <attr name="capId" value="200000005" />
  </attrs>
  <paras />
  <actions>
    <!-- intercept related request if http headers are needed -->
    <action_intercept_set>
      <response_cache url="^http:.*/api/schedule/" method="PUT" resourcetype="xhr" requestheaders="true" />
    </action_intercept_set>
    <action_goto url="http://127.0.0.1:8090/" wait="2000" />
    <!-- The variable authInfo contains the information of the account to be logged in -->
    <action_input content="${authInfo.username}" wait="1000">
      <element loc="div.qs-nologin-middle form.el-form > div:nth-child(1) input" />
    </action_input>
    <action_input content="${authInfo.password}" wait="1000">
      <element loc="div.qs-nologin-middle form.el-form > div:nth-child(2) input" />
    </action_input>
    <action_click wait="2000">
      <element loc="div.qs-nologin-middle form.el-form > div:nth-child(4) button" />
    </action_click>
    <!-- Check if login failed -->
    <action_ifelse>
      <condition_element>
        <element loc="#app div.qs-menu-container ul[role]" />
        <elecontent_length />
        <transform>
          <fun_n_eq number2="0" />
        </transform>
        <!-- failed to log in -->
        <action_exit errname="other" />
      </condition_element>
    </action_ifelse>
    <action_misc>
      <!-- by default, cookies and localStorage are included -->
      <misc_getstatedata headers="cachedRequestHeaders" />
    </action_misc>
  </actions>
</template>
```

### Example of results
```json
```
