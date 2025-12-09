
### Template config
```xml
<?xml-model href="https://www.LetsScrapeData.com/xsd/lsd_en.xsd" type="application/xml" schematypens="http://www.w3.org/2001/XMLSchema"?>
<templ tid="10010" version="0.0.4" commited="true">
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
</templ
```
scripts/concat.js:
```javascript
// version: v2
// The default version is new Date().toISOString().
// description: concat two strings by '-'

// FunScriptInData: {origStr: string, arg1: string, arg2: string, arg3: string, arg4: string, arg5: string}
const inData = { origStr: "XXX", arg1: "YYY" };

// start of script: The current line and lines above will be ignored.
function concat(inData) {
  const { origStr, arg1 } = inData;
  const result = `${origStr}-${arg1}`;

  // If this script is deemed invalid, please return "cfginvalid".

  return result;
}

// the last line must be a string or variable that holds a string or function that returns a string
// Do NOT use "return concat(inData);" !!!
concat(inData);

// end of script: The current line and the lines below will be ignored.
console.log(concat(inData));
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
