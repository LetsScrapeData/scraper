
### Template Config
```xml
<?xml-model href="https://www.LetsScrapeData.com/xsd/lsd_en.xsd" type="application/xml" schematypens="http://www.w3.org/2001/XMLSchema"?>
<template tid="10002" version="0.0.16" commited="true">
  <attrs>
    <attr name="name" value="Demo - Get Many List Examples" />
    <attr name="desc" value="Demo - Get Many List Examples shows how to add subtasks. This example gets items in the first number(para1) of list pages." />
    <attr name="domainId" value="11101" />
    <attr name="cfgShareLevel" value="120" />
    <attr name="domainNum" value="0" />
    <attr name="parasstr" value="5" />
  </attrs>
  <paras>
    <para paraname="para1" name="listNum" desc="number of list pages, from 1 to 9" />
  </paras>
  <actions>
    <action_loopfor from="1" to="${inParas.para1}" varname="listIdx">
      <action_subtask>
        <subtask tid="10001" parasstr="${listIdx}" />
      </action_subtask>
    </action_loopfor>
  </actions>
</template>
```

### Example of results
```json
{
  "subtasks": [
    {
      "tid": 10001,
      "parasstr": "1"
    },
    {
      "tid": 10001,
      "parasstr": "2"
    },
    {
      "tid": 10001,
      "parasstr": "3"
    },
    {
      "tid": 10001,
      "parasstr": "4"
    },
    {
      "tid": 10001,
      "parasstr": "5"
    }
  ]
}
```
