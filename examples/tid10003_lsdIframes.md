
### Template config
```xml
<?xml-model href="https://www.LetsScrapeData.com/xsd/lsd_en.xsd" type="application/xml" schematypens="http://www.w3.org/2001/XMLSchema"?>
<template tid="10003" version="0.0.10" commited="true">
  <attrs>
    <attr name="name" value="Demo - Get the content in iframes" />
    <attr name="desc" value="Demo - Get the content in one or many iframes" />
    <attr name="domainId" value="11101" />
    <attr name="cfgShareLevel" value="120" />
    <attr name="skippedDatatableIds" value="200000004" />
  </attrs>
  <paras />
  <actions>
    <action_goto url="https://www.letsscrapedata.com/pages/frame.html" />
    <action_loopineles>
      <element loc="#container > div.lsd-item">
        <iframe loc="#childframe01" />
        <iframe srcprefix="https://www.letsscrapedata.com/pages/listexample2.html" />
      </element>
      <action_extract tabname="dat_0000000200000004">
        <column_element colname="name">
          <element loc="a" />
        </column_element>
        <column_element colname="linkUrl">
          <element loc="a" />
          <elecontent_attr attrname="href" absolute="true" />
        </column_element>
        <column_element colname="price">
          <element loc="div[data-type='price'] span.lsd-value" />
        </column_element>
        <column_element colname="description">
          <element loc="div[data-type='desc'] span.lsd-value" />
        </column_element>
      </action_extract>
    </action_loopineles>
  </actions>
</template>
```

### Example of results
```javascript
{
  "dat_0000000200000004": [
    {
      "name": "Example201",
      "linkUrl": "https://www.letsscrapedata.com/pages/listexample1.html",
      "price": "$201",
      "description": "This is descrption of example201"
    },
    {
      "name": "Example202",
      "linkUrl": "https://www.letsscrapedata.com/pages/listexample2.html",
      "price": "$202",
      "description": "This is descrption of example202"
    },
    {
      "name": "Example203",
      "linkUrl": "https://www.letsscrapedata.com/pages/listexample3.html",
      "price": "$203",
      "description": "This is descrption of example203"
    },
    {
      "name": "Example204",
      "linkUrl": "https://www.letsscrapedata.com/pages/listexample4.html",
      "price": "$204",
      "description": "This is descrption of example204"
    },
    {
      "name": "Example205",
      "linkUrl": "https://www.letsscrapedata.com/pages/listexample5.html",
      "price": "$205",
      "description": "This is descrption of example205"
    },
    {
      "name": "Example206",
      "linkUrl": "https://www.letsscrapedata.com/pages/listexample6.html",
      "price": "$206",
      "description": "This is descrption of example206"
    },
    {
      "name": "Example207",
      "linkUrl": "https://www.letsscrapedata.com/pages/listexample7.html",
      "price": "$207",
      "description": "This is descrption of example207"
    },
    {
      "name": "Example208",
      "linkUrl": "https://www.letsscrapedata.com/pages/listexample8.html",
      "price": "$208",
      "description": "This is descrption of example208"
    },
    {
      "name": "Example209",
      "linkUrl": "https://www.letsscrapedata.com/pages/listexample9.html",
      "price": "$209",
      "description": "This is descrption of example209"
    }
  ],
  "subtasks": []
}
```
