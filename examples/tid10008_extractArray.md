
### Template config
```xml
<?xml-model href="https://www.LetsScrapeData.com/xsd/lsd_en.xsd" type="application/xml" schematypens="http://www.w3.org/2001/XMLSchema"?>
<template tid="10008" version="0.0.6" commited="true">
  <attrs>
    <attr name="name" value="Demo - extract data from an array"></attr>
    <attr name="desc" value="Demo - extract data from an array, such as array in the API response"></attr>
    <attr name="cfgShareLevel" value="120" />
    <attr name="domainId" value="1" />
    <attr name="domainNum" value="-1" />
  </attrs>
  <paras />
  <actions>
    <!-- the cached file "files/debug/tid10008_response.json" will contain the API response, only valid in debug mode -->
    <action_api url="https://httpbin.org/json" responseprefix="tid10008" varname="apiResponse" />
    <action_extract_array tabname="dat_0000000000009921" list="${apiResponse}" subkeys="slideshow.slides" keys="title,type" />
  </actions>
</template>
```
File "files/debug/tid10008_response.json" contains the API response:
```javascript
{
  "slideshow": {
    "author": "Yours Truly", 
    "date": "date of publication", 
    "slides": [
      {
        "title": "Wake up to WonderWidgets!", 
        "type": "all"
      }, 
      {
        "items": [
          "Why <em>WonderWidgets</em> are great", 
          "Who <em>buys</em> WonderWidgets"
        ], 
        "title": "Overview", 
        "type": "all"
      }
    ], 
    "title": "Sample Slide Show"
  }
}
```

### Example of results
```javascript
{
  "dat_0000000000009921": [
    {
      "title": "Wake up to WonderWidgets!",
      "type": "all"
    },
    {
      "title": "Overview",
      "type": "all"
    }
  ],
  "subtasks": []
}
```
