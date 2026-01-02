
# How to Extract Data

### Types of original data
[The original data retrieved](/scraping/acquisition) includes HTML and API responses. The data formats include the following two types:
* HTML
* JSON
  * Response data of XHR type API request is mostly JSON data, occasionally text containing JSON data.
  * Sometimes JSON data is embedded in the HTML script section.

### VSCode extension is recommend for debugging
The [LetsScrapeData extension](https://marketplace.visualstudio.com/items?itemName=LetsScrapeData.letsscrapedata) supports features such as highlighting selected elements, selecting child elements from parent elements, and timely display of extracted data, which can effectively reduce debugging difficulty and improve debugging efficiency.

### How to extract data from HTML

##### Prefer CSS selectors
LetsScrapeData supports both CSS selectors and XPath. [CSS selector](/start/cssSelector) is recommended because [LetsScrapeData extension](https://marketplace.visualstudio.com/items?itemName=LetsScrapeData.letsscrapedata) supports automatic prompts for ID, class, and attribute selector.

##### Redundant locators
Use multiple CSS selectors or XPath to adapt to changes in the webpage structure. LetsScrapeData will try them one by one until the element is selected. For example:
```xml
<column_element colname="price">
  <!-- CSS Selector -->
  <element loc="div[data-type='price'] span.lsd-value" />
  <!-- XPath -->
  <element loc="./div[1]/span"></element>
</column_element>
```

##### Extracting data from HTML
Generally, the ***action_extract*** is used to extract data from HTML. For example:
```xml
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
</action_extract>
```

Example: [template 10001](/examples/tid10001_lsdOneList)

##### Extracting data from a table
The ***action_extract_table*** makes it easy to extract the data from a table. For example:
```xml
<action_extract_table tabname="dat_0000000000009941">
  <!-- locator of the table -->
  <element loc="div.d-none table.main-table" />
</action_extract_table>
```

Example: [template 10007](/examples/tid10007_extractHorizontalTable)

##### Switching element sources
Using the LetsScrapeData extension, extracting content from a browser webpage is more user-friendly during debugging, but the downside is lower performance and efficiency. If you need to extract large amounts of data from HTML, to improve efficiency, you can switch to extracting data from HTML text after debugging by changing the template attribute to "xml":
```xml
<!-- the default value is "browser" -->
<attr name="defaultElementSource" value="xml" />
```

Example: [template 10001](/examples/tid10001_lsdOneList)

##### How to extract data from iframes
Refer to [How to Scrape Data in Iframes](/topics/iframe) for details.

### How to extract data from JSON
##### Extracting data using extract_extract_array
In most cases, simply using ***action_extract_array*** is sufficient to extract the required data from JSON; sometimes it may be necessary to combine it with ***action_loopinstr***/***action_setvar_get***.

Example: [template 10008](/examples/tid10008_extractArray)

##### Extracting data using extract_extract_script
If the logic for extracting data is complex, you can use ***action_extract_script*** to extract the required data through a customized JavaScript script.

Example: [template 10009](/examples/tid10009_exractScript)


### Related data processing
##### Data decryption
Data extracted from some web pages is unreadable, but the content displayed on the page is readable, such as content displayed using custom TTF or SVG fonts. In other words, the data to be extracted is encrypted.

Refer to [How to Decrypt Encrypted Information](/topics/decrypt) for details.

##### Data validation
It is recommended to validate frequently changing websites and key data items to promptly identify exceptions and improve the template.

Refer to [How to Handle Exceptions](/topics/exception) for details.

##### Data completion
When retrieving data from a list, such as a table containing merged cells, if a field in a record is empty, the value of the corresponding field from the previous record can be used to complete the data.

To enable data completion, set the *completed* attribute of the ***column_xxx*** to true.

##### Data transformation / cleansing
Sometimes it's necessary to transform or clean the extracted original content to make it easier for users to understand, etc.

Refer to [How to Transform / Clean Data](/topics/transformation) for details.

### Data re-extraction
If the HTML page structure or JSON data structure changes, or if the user's expected data changes, the initially extracted data may be incorrect. To address this, the original HTML or JSON data can be saved during the data acquisition. Then, after updating the template to meet the data requirements, the data is extracted again. This extraction process can be repeated multiple times as needed.

##### Re-extracting data using an updated template
First, update the original template to extract the desired data, including correcting errors, and then re-export or re-synchronize the data. This method requires the template to support both the regular execution mode and the data re-extraction mode, supporting only one data extraction result at any given time, but the operation is simpler.

Example: [template TBD](/examples/tidTBD)

##### Re-extracting data using a new template
This method involves loading previously scraped original data and re-extracting it using a new template. This method is more flexible, supporting the extraction of different data results from the same original data, supplementing the data, and adding subtasks, etc., but the operation is slightly more complex.