
### Template config
```xml
<?xml-model href="https://www.LetsScrapeData.com/xsd/lsd_en.xsd" type="application/xml" schematypens="http://www.w3.org/2001/XMLSchema"?>
<template tid="10001" version="0.0.24" commited="true">
  <attrs>
    <attr name="name" value="Demo - Get One List Example" />
    <attr name="desc"
      value="Demo - Get One List Example shows how to open a web page, use the automatic prompt of the ID/class/attribute selector, extract and save the desired data, save and commit the template. This example gets items of the nth(para1) list page." />
    <attr name="domainId" value="11101" />
    <attr name="cfgShareLevel" value="120" />
    <attr name="parasstr" value="3" />
  </attrs>
  <paras>
    <para paraname="para1" name="pageNo" desc="Page number, from 1 to 9, such as 2 in 'https://www.letsscrapedata.com/pages/listexample2.html'" />
  </paras>
  <actions>
    <action_goto url="https://www.letsscrapedata.com/pages/listexample${inParas.para1}.html" />
    <action_loopineles>
      <element loc="#container > div.lsd-item" />
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
```json
{
  "dat_0000000200000004": [
    {
      "name": "Example301",
      "linkUrl": "https://www.letsscrapedata.com/pages/listexample1.html",
      "price": "$301",
      "description": "This is descrption of example301"
    },
    {
      "name": "Example302",
      "linkUrl": "https://www.letsscrapedata.com/pages/listexample2.html",
      "price": "$302",
      "description": "This is descrption of example302"
    },
    {
      "name": "Example303",
      "linkUrl": "https://www.letsscrapedata.com/pages/listexample3.html",
      "price": "$303",
      "description": "This is descrption of example303"
    },
    {
      "name": "Example304",
      "linkUrl": "https://www.letsscrapedata.com/pages/listexample4.html",
      "price": "$304",
      "description": "This is descrption of example304"
    },
    {
      "name": "Example305",
      "linkUrl": "https://www.letsscrapedata.com/pages/listexample5.html",
      "price": "$305",
      "description": "This is descrption of example305"
    },
    {
      "name": "Example306",
      "linkUrl": "https://www.letsscrapedata.com/pages/listexample6.html",
      "price": "$306",
      "description": "This is descrption of example306"
    },
    {
      "name": "Example307",
      "linkUrl": "https://www.letsscrapedata.com/pages/listexample7.html",
      "price": "$307",
      "description": "This is descrption of example307"
    },
    {
      "name": "Example308",
      "linkUrl": "https://www.letsscrapedata.com/pages/listexample8.html",
      "price": "$308",
      "description": "This is descrption of example308"
    },
    {
      "name": "Example309",
      "linkUrl": "https://www.letsscrapedata.com/pages/listexample9.html",
      "price": "$309",
      "description": "This is descrption of example309"
    }
  ],
  "subtasks": []
}
```
