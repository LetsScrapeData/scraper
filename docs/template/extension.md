<!--
 * @Description: 
 * @Author: Joe
 * @Date: 2022-06-07 14:28:03
 * @LastEditTime: 2023-10-25 20:22:02
 * @LastEditors: Joe
 * @Reference: 
-->
# LetsScrapeData

LetsScrapeData extension allows you to add or edit template xml and related lang configs. For more information visit https://www.LetsScrapeData.com.

## Concept
A template(taskId) defines how to scrape the data from website of a domain(domainId) and then save the data into the table(tabname).

A template includes two parts: template config & template lang:
* Template config is a xml file, defines actions to scrape the data, and also contains the main language configuration.
* Template lang is only used for advanced language configuration.

## Main features
* Add Template Config: create a new XML file(tid=0), input and add "lsd" block (default: Ctrl + Alt + S).
* Save Template Config: edit XML file(tid>0) and save template (default: Ctrl + Alt + S).
* Save Template Lang: generate and save the lang config according to XML/json/html files, please refer to related document for details (default: Ctrl + Alt + L).
* Commit Template Config & Lang: validate template and lang configs, then commit them if correct(This command does not save configs!) (default: Ctrl + Alt + C).
* Get New Tabname: get a new data tablename used to save data from a domain.
* Search Domains: search domains according to some of domain name
* Search Templates: search my templates of domainId or all domainIds if domainId is empty
* Search Tabnames: search my tabnames of domainId or all domainIds if domainId is empty
* Get Template Config: get xml of a template by tid.
* Get Template Lang: get lang config of the current template(xml)
* Execute a template with parasstr(paras):
    - Execute All Actions: execute all actions of a template (defaut: Ctrl + Alt + A)
    - Execute Part Actions: execute part actions of a template (defaut: Ctrl + Alt + P)
    - Extract Some Columns: extract selected column (defaut: Ctrl + Alt + F, Shift + F in vim norml mode)
* Autocompletion when editing loc attribute(only CSS selector) of element tag(loc support CSS selector and Xpath):
    - ID selector: triggerCharacter("#"), such as loc="div#"
    - class selector: triggerCharacter("%"), such as loc="div%"
    - attribute selector(attribute name): triggerCharacter("["), such as loc="div[" or attrname="[" in elecontent_attr tag.
    - attribute selector(attribute value): triggerCharacter("!"), such as loc="a[href=!"
* Display outer XML of the first selected element:
    - Display outer XML of first element when focusing on a column line(refer to "Extract Some Columns")
    - Display outer XML of first elemennt when focusing on a element line or other line(parent element) (command "Show Parent Xml") (default: Ctrl + Alt + T, or Shift + T in vim normal mode)

## Related extensions
* <b style="color: red;">Dependent extension</b>: "XML"(by Red Hat)
* Suggested extension: "Vim"(by vscodevim), if you want to use keyboard shortcuts(shift + T, shift + F) in vim normal mode.

## How to add/update a template
1. First you must decide the domainId of template and tabname(s). Both template and tabname(s) must have the same domainId. You can get the domainId of domainName by command "Search Domains".
2. Get new tabname(s) of related domainId if needed, or reuse tabname(s) with other template if they save the SAME data.
3. Create or update a template and lang config.
4. Test template by executing a template.
5. Add/Save template: Add if tid is 0, or save the template if tid > 0.
6. Save template lang config.
7. Repeat steps 3 ~ 6 if needed.
8. Commit template and lang config.
