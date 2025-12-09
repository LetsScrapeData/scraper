
### Template config
```xml
<?xml-model href="https://www.LetsScrapeData.com/xsd/lsd_en.xsd" type="application/xml" schematypens="http://www.w3.org/2001/XMLSchema"?>
<template tid="10009" version="0.0.6" commited="true">
  <attrs>
    <attr name="name" value="Demo - extract data using script"></attr>
    <attr name="desc" value="Demo - extract data using script, such as extracting data from the API response"></attr>
    <attr name="domainId" value="1"></attr>
    <attr name="cfgShareLevel" value="120" />
    <attr name="parasstr" value="TITLE::TYPE" />
  </attrs>
  <paras>
    <para paraname="para1" name="title" desc="title" />
    <para paraname="para2" name="type" desc="type" />
  </paras>
  <actions>
    <!-- The name here must be the same as scripts.script.name with the scenario "extract" -->
    <action_extract_script name="extractData" tabname="dat_0000000000009931" />
  </actions>
  <scripts>
     <!-- The script file scripts/extractData.js must exist and contain the script content. -->
    <script name="extractData" scenario="extract" version="v1.2.0">placeholder</script>
  </scripts>
</template>
```
scripts/extractData.js:
```javascript
// version: v1.2.0
// The default version is new Date().toISOString().
// description: extract data using script

// ExtractScriptInData: {vars, responses, execData, tabName, maxLoops, errName}
// vars: {inParas, xxx}
// execData: Record<tabname, Record<string, string>[]>
//   tabname of cached responses: refer to action_api & action_intercept_set.response_cache
//   record of cached responses: {pageUrl, requestUrl, requestMethod, requestData, responseData, size}[]
const inData = {
  vars: { inParas: { para1: "TITLE", para2: "TYPE" } },
  execData: {},
  tabName: "dat_0000000000009931",
  maxLoops: 0,
  errName: "ignore",
};

// start of script: The current line and lines above will be ignored.
function extract(inData) {
  const { vars, execData, tabName } = inData;

  let records = execData[tabName];
  if (!records) {
    records = [];
    execData[tabName] = records;
  }

  records.push({ title: vars.inParas.para1, type: vars.inParas.para2 });

  // ExtractScriptOutData: {execData, ?errName}
  // If this script is deemed invalid, please set errName to "cfginvalid".
  const outData = { execData };

  return JSON.stringify(outData);
}

// the last line must be a string or variable that holds a string or function that returns a string
// Do NOT use "return extract(inData);" !!!
extract(inData);

// end of script: The current line and the lines below will be ignored.
console.log(extract(inData));

```

### Example of results
```javascript
{
  "dat_0000000000009931": [
    {
      "title": "TITLE",
      "type": "TYPE"
    }
  ],
  "subtasks": []
}
```
