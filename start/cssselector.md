<!--
 * @Description: 
 * @Author: Joe
 * @Date: 2023-09-26 09:49:47
 * @LastEditTime: 2023-10-27 09:41:01
 * @LastEditors: Joe
 * @Reference: 
-->

# CSS Selectors Auto-prompt

### Introduction to CSS Selectors
[CSS (Cascading Style Sheets)](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/CSS_basics) is the code that styles web content. In LetsScrapeData, selectors are patterns used to match, or select, the elements from which you want to extract the data. There are many different types of selectors, such as:
* [Attribute Selector](https://developer.mozilla.org/en-US/docs/Web/CSS/Attribute_selectors)
* [Class Selector](https://developer.mozilla.org/en-US/docs/Web/CSS/Class_selectors)
* [ID Selector](https://developer.mozilla.org/en-US/docs/Web/CSS/ID_selectors)

### Use the class selector auto-prompt
The charactor that triggers the class selector auto-prompt is "%", such as loc="div%" in element tag.
```
<element loc="#container > div%" />
```

### Use the ID selector auto-prompt
The charactor that triggers the ID selector auto-prompt is "#", such as loc="#" in element tag.
```
<element loc="#" />
```

### Use the attribute selector auto-prompt
The charactor that triggers the attribute selector(attribute name) auto-prompt is "[", such as loc="div[" in element tag, or attrname="[" in elecontent_attr tag.
```
<element loc="div[" />
<elecontent_attr attrname="[">
```
The charactor that triggers the attribute selector(attribute value) auto-prompt is "=!", such as loc="a[href=!" in element tag.
```
<element loc="div[data-type=!" />
```


Refer to the video on [how to design a template config](https://youtu.be/kFlZ0Ogg1PI).
