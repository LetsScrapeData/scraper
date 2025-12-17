<!--
 * @Description: 
 * @Author: Joe
 * @Date: 2023-09-27 16:21:03
 * @LastEditTime: 2023-10-27 09:41:13
 * @LastEditors: Joe
 * @Reference: 
-->

# Datatable
The scraped data is stored in datatables, each uniquely identified by a **tabname** (such as "dat_0000000000008001") and a corresponding numerical value called **datatableId** (such as 8001). Datatables are divided into two main categories:

### Types of datatable
* **JSONL datatable**: datatableId < 10000, directly referenced by any template (no application required). Data records are treated as JSONL (This category of datatable, after synchronization or export, only has one column "jsonl".), and no multi-language configuration is needed. This category is further subdivided into three types:
  * **Visible JSONL datatable**: 8000 <= datatableId < 10000; Stores data, visible to the user (exportable and synchronizable).
  * **Hidden datatable**: 7000 <= datatableId < 8000; Stores data, not visible to the user; primarily used for scenarios where raw data is obtained first, and then extracted later.
  * **Temporay datatable**: 6000 <= datatableId < 7000; Does not store data, not visible to the user; primarily used to store temporary data, from which the required data is immediately extracted.
* **Regular datatable**: datatableId > 10000; It must be applied for first and can only be used to store data corresponding to the domainId. Multilingual configuration must be defined.

For simplicity, the default tabname is a JSONL datatable. However, regular datatables are more user-friendly. If the template is used by many users, it is recommended to use a regular datatable for the datatable that is visible to users. This way, when users export or synchronize data, they will see a table with detailed fields, and it also supports multiple languages.

### How to use regular datatable
A template can have multiple regular datatables or not. The regular datatables and template must be associated with the same domainId.

##### First get a new tabname
* Run the command "LSD:Get New Tabname" in VsCode.
* Enter the domainId associated with the template.
* The new tabname be displayed.

##### Then set domainId of template
* Update the tabname in XML template config.

Refer to the video on [how to design a template config#tabname](https://youtu.be/kFlZ0Ogg1PI).
