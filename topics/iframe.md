
# How to Scrape Data in Iframes
To access or extract data from iframes, simply use the ***iframe*** within the ***element***. For example:
```xml
<element loc="#container > div.lsd-item">
  <iframe loc="#childframe01" />
  <iframe srcprefix="https://www.letsscrapedata.com/pages/listexample2.html" />
</element>
```

Example: [template 10003 ](/examples/tid10003_lsdIframes)