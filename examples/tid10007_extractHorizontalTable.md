
### Template config
```xml
<?xml-model href="https://www.LetsScrapeData.com/xsd/lsd_en.xsd" type="application/xml" schematypens="http://www.w3.org/2001/XMLSchema"?>
<template tid="10007" version="0.0.8" commited="true">
  <attrs>
    <attr name="name" value="Demo - extract data from a horizontal table" />
    <attr name="desc" value="Demo - extract data from a horizontal table" />
    <attr name="domainId" value="1" />
    <attr name="cfgShareLevel" value="120" />
    <attr name="parasstr" value="https://countrycode.org/::div.d-none table.main-table" />
  </attrs>
  <paras>
    <para paraname="para1" name="url" desc="url" />
    <para paraname="para2" name="tableLoc" desc="tableLoc" />
  </paras>
  <actions>
    <action_goto url="${inParas.para1}" />
    <action_extract_table tabname="dat_0000000000009941" maxloops="5">
      <element loc="${inParas.para2}" />
    </action_extract_table>
  </actions>
</template>
```

### Example of results
```json
{
  "dat_0000000000009941": [
    {
      "country": "Afghanistan",
      "countryCode": "93",
      "isoCodes": "AF / AFG",
      "population": "29,121,286",
      "areaKm2": "647,500",
      "gdpUsd": "20.65 Billion"
    },
    {
      "country": "Albania",
      "countryCode": "355",
      "isoCodes": "AL / ALB",
      "population": "2,986,952",
      "areaKm2": "28,748",
      "gdpUsd": "12.8 Billion"
    },
    {
      "country": "Algeria",
      "countryCode": "213",
      "isoCodes": "DZ / DZA",
      "population": "34,586,184",
      "areaKm2": "2,381,740",
      "gdpUsd": "215.7 Billion"
    },
    {
      "country": "American Samoa",
      "countryCode": "1-684",
      "isoCodes": "AS / ASM",
      "population": "57,881",
      "areaKm2": "199",
      "gdpUsd": "462.2 Million"
    },
    {
      "country": "Andorra",
      "countryCode": "376",
      "isoCodes": "AD / AND",
      "population": "84,000",
      "areaKm2": "468",
      "gdpUsd": "4.8 Billion"
    }
  ],
  "subtasks": []
}
```
