<!--
 * @Description: 
 * @Author: Joe
 * @Date: 2023-09-27 16:22:02
 * @LastEditTime: 2023-10-27 09:33:41
 * @LastEditors: Joe
 * @Reference: 
-->
<!--
 * @Description: 
 * @Author: Joe
 * @Date: 2023-09-27 16:22:02
 * @LastEditTime: 2023-09-27 16:50:24
 * @LastEditors: Joe
 * @Reference: 
-->

# Save / Add Template
The details of the template are saved in the following places:
Local text files: template config is saved in a XML file, template lang is save in many json files. These files are usually edited and saved in VSCode.
In APP database: the content in the APP database is for your own use only.
In server database: the content in the server database can be used by others.

### Steps to save / add / commit a template
Each step needs to meet the relevant specifications. If the relevant specifications are not met, an error is displayed.
* Save/Add Template Config: save the template config or the XML file into APP database. The template will be added if tid is 0, or template will be saved.
* Save Template Lang: generate tempalte lang and save them into APP database. Although a separate template lang is optional, this step is required.
* Commit Template Config & Lang: save template config & lang in APP database into server database so that others can search and use them.

Refer to the video on [how to design a template config#save](https://youtu.be/kFlZ0Ogg1PI).
