<!--
 * @Description: 
 * @Author: Joe
 * @Date: 2023-09-25 19:24:28
 * @LastEditTime: 2023-10-27 16:45:45
 * @LastEditors: Joe
 * @Reference: 
-->
# Quick Start - Template Design

The instructions in this section are only applicable when you design the template yourself. If you use an existing template to scrape data, refer to [how to scrape data](/readme).

We design templates using vscode and related extensions.

### Build a template design environment
* If you have not installed VSCode, please install [VSCode](https://code.visualstudio.com/). The following VSCode settings are recommended. Turn on word wrap and indent using 2 spaces.
```json
{
  "editor.wordWrap": "on",
  "editor.tabSize": 2,
  "editor.insertSpaces": true
}
```
* Install VSCode extensions:
  * XML, developed by Red Hat. The following VSCode setting are <b>highly </b>recommended, otherwise a maxOccurLimit error is likely to occur.
  ```json
  {
    "xml.symbols.maxItemsComputed": 500000
  }
  ```
  * LetsScrapeData, developed by LetsScrapeData.

### Basic concepts used by the template
* <b>attr</b>: attribute of template, such as template\.name
* <b>para</b>: parameter defines what data is scraped or controls web scraping process
* <b>action</b>: what to do for scraping data
* <b>domainId</b>: a template must be associated with a domainId identified domain, which is a attribute of template
* <b>tabname</b>: the name of the data table that stores the scraped data, and a template can have multiple data tables or not; the domainId associated with tabname must be the same as that of the template
* <b>loc</b>: [CSS Selector](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Selectors) or [XPath](https://developer.mozilla.org/en-US/docs/Web/XPath), which is used to select the elements from which to extract the desired data; [CSS selector](/start/cssSelector) is recommended because LetsScrapeData extension supports automatic prompts for ID, class, and attribute selector

### Components of a template
A template consists of two components:
* Template Config: a XML file that defines attributes, parameters, actions and basic lang information of template.
* Template Lang: many json files that define multilingual information for template, parameters, tabnames. It is optional because template config contains the basic lang information(name & description of template and parameters, nickname of data table's columns).


### Design a simple template
* Create an XML file, preferably in the domain directory.
* Insert a default initial template config by inputing lsd and press the Enter key.
* Input the URL of the web page you want to open: https://www.LetsScrapeData.com/pages/listexample1.html.
* Open the above url by running command "Execute All Actions(Ctrl + Alt + A)".
* In the web page, view the element properties that contain the list of exmple items. The div element with id container contains a list of example items.
* Add action_loopineles by inputing acle and press the Enter key, replace <b style="color: blue">loc</b>. You may use class / ID / attribute [CSS selector](/start/cssSelector) when inputting loc.
* If needed, check the above loc is correct:
  * Run command "Extract Some Columns(Ctrl + Alt + F, or shift + F in vim normal mode)" to check the loc: Selected elements will be hightlighted in web page and the outerHtml of the first selected element will be displayed.
* Add action_extract by inputing acex and press the Enter key.
* Add column_element by inputing coe and press the Enter key. The colname is the column name of the table (and also the field name of the synchronized database table). If you want to view the parent XML, run command "Show Parent Xml(Ctrl + Alt + T, or shift + T in vim normal mode)".
  * Parent XML: outerHTML of the first element selected by the <b style="color: blue">loc</b> defined in preceding action_loopineles 
* If needed, check the above loc is correct:
  * Run command "Extract Some Columns(Ctrl + Alt + F)" to check the extracted data.
* Add linkUrl, price, description by adding column_element.
* Test the template:
  * If the url has alread been openned, run command "Execute Part Actions(Ctrl + Alt + P)", which will skip all "operate" actions, such as goto/click/input/hover/select.
  * If the url has not been openned yet, run command "Execute All Actions(Ctrl + Alt + A)".
* [Add/Save/Commit template](/start/saveTemplate)
  * Run command "Save/Add Template Config(Ctrl + Alt + S)" to add a new template(tid=0), then tid is updated.
  <!-- * Run command "Save/Add Template Config(Ctrl + Alt + S)" to save the template config. -->
  * Run command "Save Template Lang(Ctrl + Alt + L)" to generate and save the template lang.
  * Run command "Commit Template Config & Lang(Ctrl + Alt + C)" to commit the template.

### Template config example
The following template has tid 10001, you can add a schedule with this template. [Video on youtube](https://youtu.be/kFlZ0Ogg1PI) shows how to design this template.
```xml
<?xml-model href="https://www.LetsScrapeData.com/xsd/lsd_en.xsd" type="application/xml" schematypens="http://www.w3.org/2001/XMLSchema"?>
<template tid="10001" version="0.0.80" commited="true">
  <attrs>
    <attr name="name" value="Demo - Get One List Example" />
    <attr name="desc"
      value="Demo - Get One List Example shows how to open a web page, use the automatic prompt of the ID/class/attribute selector, extract and save the desired data, save and commit the template. This example gets items of the nth(para1) list page." />
    <attr name="domainId" value="11101" />
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

### Next
* [Set domainId](/start/setDomainId)
* [Use regular data table](/start/datatable)
* [CSS Selectors](/start/cssSelector)
