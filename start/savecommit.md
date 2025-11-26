<!--
 * @Description: 
 * @Author: Joe
 * @Date: 2023-09-27 16:22:02
 * @LastEditTime: 2023-10-27 09:33:41
 * @LastEditors: Joe
 * @Reference: 
-->

# Add / Save / Commite Template

### Components of a template
A template consists of two components:
* Template Config: a XML file that defines attributes, parameters, actions and basic lang information of template.
* Template Lang: many json files that define multilingual information for template, parameters, tabnames.

### Where to save
The details of the template are saved in the following places:
* Local text files: template config is saved in a XML file, template lang is saved in many json files. These files are usually edited and saved in VSCode.
* APP database: the content in the APP database is for your own use only.
* Server database: the content in the server database can be used by other users, which should be correct.

### How to save / add / commit a template
After you have finished editing and debugging the template in VSCode, Run the following command to save / add  / commit the template.
* Save/Add Template Config: Save the template config or the XML file into APP database. The template will be added if tid is 0, or template will be saved.
* Save Template Lang: Generate tempalte lang and save them into APP database. Although a separate template lang is optional, this step is required.
* Commit Template Config & Lang: First, check the validity of the Config & Lang, and then commit the Config & Lang to server daatabase simultaneously. Only after the commit can other users access the updated template.

Refer to the video on [how to design a template config#save](https://youtu.be/kFlZ0Ogg1PI).
