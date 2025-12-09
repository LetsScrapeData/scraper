
# How to Use Variables
1. Scope of variables: Variables in the template are valid throughout the task context.
2. Data type of variables: The data type of variable values ​​is always string, but may be serialized strings of object, array, number, or boolean value types.

### How to get the value of variable
Use [string template](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals) to get the value of a variable, such as \`xxx${variable}yyy\`.

### How to set the value of variable
* *varname*: Specifies the variable name through the varname attribute, and the corresponding value will be assigned to that variable.
* *setkeys*: Similar to object destructuring, assigns the values ​​of certain keys of an object to the corresponding variables.

### Types of variables
##### Normal variables
Normal variables are those that are not of the following types, such as "productId".

pageHtml: When extracting data from HTML text, if the data source is not set, the value of this variable will be automatically set to the HTML content of the page when accessing the value.

##### inParas
The input parameters for the task are read-only, such as "inParas.para1".
The task's input parameters, such as "inParas.para1", are read-only.

##### authInfo
Only valid in the automatic login template.

The detailed information of the capability(aka credentials) , such as "authInfo.username" and "authInfo.password", is used for the automatic login template and is read-only.

For more information, please refer to [When Login Is Required](/topics/login).

##### userData
Custom session data in the state data, such as "userData.lastUpdateTime".

##### secureData
Secure data that can be accessed during task execution but not by the user, such as cookies or localStorage data, like "secureData.token".
