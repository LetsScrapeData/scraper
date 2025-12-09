
### Template Config
```xml
<?xml-model href="https://www.LetsScrapeData.com/xsd/lsd_en.xsd" type="application/xml" schematypens="http://www.w3.org/2001/XMLSchema"?>
<template tid="10010" version="0.0.4" commited="true">
  <attrs>
    <attr name="name" value="defaultName"></attr>
    <attr name="desc" value="defaultDescription"></attr>
    <attr name="domainId" value="1"></attr>
    <attr name="cfgShareLevel" value="120" />
    <attr name="domainNum" value="0" />
    <attr name="parasstr" value="XXX::YYY" />
  </attrs>
  <paras>
    <para paraname="para1" name="paraStr1" desc="paraStr1" />
    <para paraname="para2" name="paraStr2" desc="paraStr2" />
  </paras>
  <actions>
    <action_extract tabname="dat_0000000000009911">
      <column_templstr colname="paraStr1">
        <templstr templ="${inParas.para1}" />
      </column_templstr>
      <column_templstr colname="paraStr2">
        <templstr templ="${inParas.para2}" />
      </column_templstr>
      <column_templstr colname="concatStr">
        <templstr templ="${inParas.para1}" />
        <transform usevar="true">
          <fun_script name="concat" arg1="${inParas.para2}" />
        </transform>
      </column_templstr>
    </action_extract>
  </actions>
  <scripts>
    <script name="concat" scenario="fun" version="v2">placeholder</script>
  </scripts>
</template>
```

### Example of results
```json
{
  "dat_0000000000009911": [
    {
      "paraStr1": "XXX",
      "paraStr2": "YYY",
      "concatStr": "XXX-YYY"
    }
  ],
  "subtasks": []
}
```
